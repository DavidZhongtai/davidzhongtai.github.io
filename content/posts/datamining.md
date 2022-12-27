---
title: Pandas and Data Mining
---

# A Discussion on Pandas and Data Mining (WIP)

At the beginning of any data analytics/data science project, the most usual case is utilizing Pandas to load the data into a object called a DataFrame and perform preprocessing tasks on it. While the Pandas library is convenient and comes with a trove of useful analytic tools, it does have some inefficiencies, many due to the nature of Python. To investigate this, let's look at how Pandas actually works on top of Python. But first, some discussion on Python and C.

Python itself is known as a high level and interpreted language. An interpreted language is one where a different program, _called the interpreter_ reads and executes the code. A high level language means that it is easy to read and maintain. In fact, this is obvious from some commands inside the language. For example, printing a statement in Python is done as:
`print('hello world')` while in Java, it is `System.out.println("hello world")` and one has to keep track of class names and packages as well. This also makes the case that Python is a nice language to start out with, with a relatively low learning curve. Because it is easy to read and implement, it also has some disadvantages as well.

Since Python is an interpreted language, it uses an interpreter known as Cython, a Python interpreter written in C and translates Python into bytecode, a readable format for the Python Virtual Machine. This process of interpreting the Python code at runtime adds on a bit of overhead that contributes to the reason of why Python generally runs slower than C. Simply speaking, when we run a Python file, a program called a tokenizer first converts the .py into a sequence of tokens, also known as a token stream. Then, a lexical analyzer dissects that stream and performs syntax analysis and checking on it. After that, a byte code generator generates the bytecode. In Python, this is also the .pyc files. Finally, the bytecode interpreter intereprets that stream of bytecode and runs the program.

However, being a interpreted language, there are some things Python implements that sacrafices speed. These three things are a built in garbage collector, something called the 'global interpreter lock' (GIL), and dynamic typing. The garbage collector is responsible for managing and freeing up memory that is not used for the machine. The GIL is essentially a mutex which only allows one thread to have control of the Python interpreter. What this means for the developer is that they need to keep in mind when designing their programs is the complexity. Since the GIL only allows single threaded applications, it can prove to become a burden in performance for code that is designed to be CPU-bound and multi-threaded.

When we run a Python program, we now know that M<WRITE ABT PYC files>

Now, when we run Pandas, many more things happen under the hood. Pandas itself is a wrapper of NumPy. NumPy itself is a wrapper for C. Because of this relationship, the performance of Pandas depends on the performance of C.
<Maybe add more things on Pyth>

Recently, I covered some of my research as well as briefly mentioning unification within academia and digital cataloging. Data mining itself has become a valuable field due to the commercialization opportunities it holds. Companies can now use these different algorithms to glean valuable insights into customers and trends. However, the challenge itself is the extensive computing power many of these algorithms use. With billions of data points, the cost to continuously train, evaluate, and deploy these algorithms only goes up as data becomes more and more available to us. When working with small datasets, the performance of Python is barely negilgable. However, as datasets grow larger and larger, the performance impact is noticable. <relation between pandas and data mining, mention spark, parquet >

[Back to writing](../../blog)
