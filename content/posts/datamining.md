---
title: Pandas and Data Mining
---

# A Discussion on Pandas and Data Mining

At the beginning of any data analytics/data science project, the most usual case is utilizing Pandas to load the data into a object called a DataFrame and perform preprocessing tasks on it. While the Pandas library is convenient and comes with a trove of useful analytic tools, it does have some inefficiencies, many due to the nature of Python. To investigate this, let's look at how Pandas actually works on top of Python. But first, some discussion on Python and C.

Python itself is known as a high level and interpreted language. An interpreted language is one where a different program, _called the interpreter_ reads and executes the code. A high level language means that it is easy to read and maintain. In fact, this is obvious from some commands inside the language. For example, printing a statement in Python is done as:
`print('hello world')` while in Java, it is `System.out.println("hello world")` and one has to keep track of class names and packages as well. This also makes the case that Python is a nice language to start out with, with a relatively low learning curve. Because it is easy to read and implement, it also has some disadvantages as well.

Since Python is an interpreted language, it uses an interpreter known as Cython, a Python interpreter written in C and translates Python into bytecode, a readable format for the Python Virtual Machine. This process of interpreting the Python code at runtime adds on a bit of overhead that contributes to the reason of why Python generally runs slower than C. Simply speaking, when we run a Python file, a program called a tokenizer first converts the .py into a sequence of tokens, also known as a token stream. Then, a lexical analyzer dissects that stream and performs syntax analysis and checking on it. After that, a byte code generator generates the bytecode. In Python, this is also the .pyc files. Finally, the bytecode interpreter interprets that stream of bytecode and runs the program.

However, being a interpreted language, there are some things Python implements that sacrifices speed. These three things are a built in garbage collector, something called the 'global interpreter lock' (GIL), and dynamic typing. The garbage collector is responsible for managing and freeing up memory that is not used for the machine. The GIL is essentially a mutex which only allows one thread to have control of the Python interpreter. What this means for the developer is that they need to keep in mind when designing their programs is the complexity. Since the GIL only allows single threaded applications, it can prove to become a burden in performance for code that is designed to be CPU-bound and multi-threaded. These are some reasons why Python performs slower than C in most cases.

When we run a Python program, we now know that the code is interpreted into bytecode (.pyc) at runtime. However, often times when you run a program subsequently after making changes, you may notice that the code still performs like the previous version. This phenomenon is due to something known as bytecode caching. When the Python interpreter runs, it caches the bytecode. This significantly reduces the overhead needed upon each execution cycle. If you delete the .pyc files before execution, this is similar to clearing out the bytecode cache and makes the interpreter reinterpret the program. However, while this behavior may convince developers to disable it or turn it off, it is usually wiser to keep it on as 1) it runs in the background, undetected; and 2) it improves interpretation performance by a significant amount--especially when programs get larger.

Now, when we run Pandas, many more things happen under the hood. Pandas itself is a wrapper of NumPy. NumPy itself is a wrapper for C. Because of this relationship, the performance of Pandas depends on the performance of C. We can also find out that since Pandas is essentially a wrapper for C, it is not subject to some of the performance issues that come from Python (i.e. there is no GIL to constrain processing which allows for multi-core processing). However, since NumPy runs in C, that means all Python objects need to be translated into C. Thus, it's important that a data scientist should keep in mind that they should operate on types that can be interpreted as C types. Usually, this is not a problem as more often than not, data is in numeric form (int, double, float), or lexical form (str, char). In the cases where you are working with custom data types, and it is not translatable into C, the process remains in Python where the GIL is unlocked after the current process.

Now, we discuss how NumPy exactly interprets data. In NumPy, the base "building block" is known as a N-dimensional array or ndarray. This also happens to serve as the bridge between Python and C. Also, one should note that the ndarrays inside of NumPy are homogenous meaning that they all need to have a uniform type. Since this is in C, the arrays do not allow for dynamic typing, hence why ndarrays need homogenous types. Inside the array, something known as a dtype specifies the type of element in the array as well as other information as well. Some of this information includes size of the data, byte order, structure, and more. For example, we have a simple data type of a 32 bit endian integer shown below:

```py
dt = np.dtype('>i4')
>>> dt.byteorder
'>'
>>> dt.itemsize
4
>>> dt.name
'int32'
>>> dt.type is np.int32
True
```

Now, we also see that CPython provides an C-API that allows one to release the GIL mentioned earlier. Numpy utilizes many of these macros in order to speed up processing. For example, NumPy utilizes `NPY_BEGIN_THREADS`[^1] as well as `NPY_END_THREADS` to denote and acquire the ability to operate and release without the GIL. Now, math operations that require intense compute power are now able to break up and implement multi-threaded computations in C, which is a significant performance improvement itself. Now, that concludes a basic, probably messy synopsis on the relationship between C, Python, and Pandas. Now, onto the more fun data science stuff.

<Maybe add more things on Pyth>

Recently, I covered some of my research as well as briefly mentioning unification within academia and digital cataloging. Data mining itself has become a valuable field due to the commercialization opportunities it holds. Companies can now use these different algorithms to glean valuable insights into customers and trends. However, the challenge itself is the extensive computing power many of these algorithms use. With billions of data points, the cost to continuously train, evaluate, and deploy these algorithms only goes up as data becomes more and more available to us. When working with small datasets, the performance of Python is barely negligible. However, as datasets grow larger and larger, the performance impact is noticable. In most data science related workflows, the common method manipulate data is done with a structure known as a DataFrame. We did mention previously how pandas wraps around NumPy which wraps around C, and thus the performance of DataFrames is heavily dependent on the performance of C.

Because of how Pandas was written, it was done for ease of use instead of focusing heavily on the optimization part of it. In addition to that, because of the flexible nature of it, many paths lead to the same road, i.e. there are many ways to perform such operations and obtain the same result. For small datasets (<100,000 rows), this is not a problem as the hardware performance negates this effect. However, the larger you go, the more significant these issues become. I will cover two different ways to do the same operation, showing how we can take advantage of the things we discussed previously.

One of the most common operations inside of a DataFrame is deriving a new row based on the results of another row. For example, if we wanted to see the result over many different rows, we can sum up all of the entries in the associated row and appended it into a new column. The first approach involves using `.iterrows()` to go through each row and sum it up. In code, that is shown as:

```python
[np.sum(row[0], row[1]) for _, row in df.iterrows()]
```

This becomes terribly inefficient as `.iterrows()` is effectively creating a for loop and going through the whole dataset. Imagine if there were millions of entries and having to go through each one. This is not to mention all of the overhead created to do type magic mentioned above and converting between numpy and C. However, we can get rid of that overhead by commanding the interpreter to only use raw values instead.

```python
df.apply(lambda row: sum_square(row[0], row[1]), raw=True, axis=1 )
```

By using the parameter `raw=True`, we are able to bypass all the conversion and tell Python to directly map the types instead of converting them. By doing so, we achieve a significant improvement in memory usage and a decrease in overhead. Now, these are simply ways to do so in using Pandas methods. Note that this was just a very brief overview of such methods; there still lies more ways to optimize for large datasets. For cases where some methods aren't applicable, what you can do is compile in Cython or utilize runtime compilers like Numba[^2]. Utilizing parallel processing is also another option; however, you have to be cognizant of the applications of it. There can be two main reasons where it cannot be more efficient and instead can perform the same, if not worse than traditional methods. These reasons are generating overhead and CPU vs. I/O bound applications. For the reader's sake, I will be saving these topics for a future discussion. The main takeaway is that we barely scratched the surface of Python and its implementations and how it relates back to applications in data science. That, will be saved for a future exploration.

[Back to writing](../../blog)

[^1]: [nd-array Reference](https://numpy.org/doc/stable/reference/c-api/array.html)
[^2]: [Numba Reference](https://numba.readthedocs.io/en/stable/user/5minguide.html)
