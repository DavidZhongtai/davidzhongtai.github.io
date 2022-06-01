## Scraping Web Data for Academic Literature
Done in collaboration with Dr. Emiliano Valdez, University of Connecticut

### Goals
How obvious are actual trends in academic literature and how can we easily gather academic literature metadata? The purpose of the exploratory study was to develop and analyze different methods of data retrieval from multiple sources. 

Given a text search within context, we should be able to retrieve a list of articles that contain that segment of text. This closely aligns with the [current research](/research/nlpsearch) I am doing. Similar to that, we are also searching in the actuarial science domain. With a corpus of metadata, we are able to observe large trends in this field that would be unbeknownst to an outsider. This also allows us to capture the big picture and direct future research for acutaries in an innovative manner. 

### Tools 
- Python was the main tool used in this exploration. We chose Python because of the vast amount of libraries available. 
- The data was stored in Excel format (.xlsx). Looking back on it, this form of data required parsing and processing every time the database had to be cached in local memory. This was due to the Excel format not supporting abstract data types (ADTs) such as lists or dictionaries and instead stored string representations. 
- The data was pulled from the ScienceDirect database which holds an extensive of respoitory of academic literature in a wide span of fields. The scraping and methodology is discussed later. 

### Discussion
One may ask, how do we know that our queries yield representative results. One important assumption that we experiment under is that if an author wanted their article to be representative, then the query would have those keywords in the text. 

We were able to connect to and interact with the databases with something known as an Application Programming Interface (API). With an API wrapper for ScienceDirect [^1], we are able to effortlessly interface with the database service and perform a variety of operations 

[^1]: [PyScopus](http://zhiyzuo.github.io/python-scopus/)
