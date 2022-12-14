## Scraping Web Data for Academic Literature

Done in collaboration with Dr. Emiliano Valdez[^1], University of Connecticut

### Goals

How obvious are actual trends in academic literature and how can we easily gather academic literature metadata? The purpose of the exploratory study was to develop and analyze different methods of data retrieval from multiple sources.

Given a text search within context, we should be able to retrieve a list of articles that contain that segment of text. This closely aligns with my [current research](/research/nlpsearch). Similar to that, we are also searching in the actuarial science domain. With a corpus of metadata, we are able to observe large trends in this field that would be unbeknownst to an outsider. This also allows us to capture the big picture and direct future research for acutaries in an innovative manner.

### Tools

- Python was the main tool used in this exploration. We chose Python because of the vast amount of libraries available.
- The data was stored in Excel format (.xlsx). Looking back on it, this form of data required parsing and processing every time the database had to be cached in local memory. This was due to the Excel format not supporting abstract data types (ADTs) such as lists or dictionaries and instead stored string representations.
- The data was pulled from the ScienceDirect database which holds an extensive of respoitory of academic literature in a wide span of fields. The scraping and methodology is discussed later.

### Discussion

One may ask, how do we know that our queries yield representative results. One important assumption that we experiment under is that if an author wanted their article to be representative, then the query would have those keywords in the text.

We were able to connect to and interact with the databases with something known as an Application Programming Interface (API). With an API wrapper for ScienceDirect[^2], we are able to effortlessly interface with the database service and perform a variety of operations such as data retrieval. This proves to be useful when querying massive amounts of data. Because we are an university-affiliated organization, we are not bound to the data retrieval limits that regular users have.

With such a dataset, there can be many different opportunities to generate meaningful insights. One that comes to mind is tracking the frequency of articles within a proposed timeframe. Does there seem to be an increase of articles relating to financial risk modeling as we become as more people venture into various financial markets? Another valuable insight are the keywords that come along with the articles. Do certain keywords appear in a certain time context? (i.e. 'recession' and 'markets' may correlate with the financial crisis of 2007-08)

To summarize, there may be many hidden trends within academia that researchers may not be aware of. By exploiting massive amounts of data, we are able to extrapolate various patterns within that give us insight into current trends and where future research may be headed. Additionally, this method doesn't have to be limited solely to the field of actuarial science; the methods developed in this study can be generalized to other fields too. The only requirement is the creativity to glean meaningful insights from the data.
[^1]: [Dr.Emiliano Valdez](http://www2.math.uconn.edu/~valdez/)
[^2]: [PyScopus](http://zhiyzuo.github.io/python-scopus/)

[Back to writing](../../blog)
