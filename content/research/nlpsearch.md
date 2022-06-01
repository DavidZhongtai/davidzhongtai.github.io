## Building an NLP-Powered Repository for Cyber Risk Literature [[Poster]](/research/draft1.pdf)
David An, Linfeng Zheng, Zhiyu (Frank) Quan
### Abstract
With the large and growing body of cyber risk literature, we see three major challenges faced by the actuarial research community: there is no context aware tool for finding cyber literature, no central repository of cyber risk resources, and a lack of accounting of literature trends. To address the abovementioned challenges, we propose to build a repository of cyber-risk articles with an NLP powered search tool that can easily be used by researchers to find relevant materials. We cover a high level overview of this ongoing research project

### Goals
- Apply natural language processing (NLP) techniques to classify and group cyber-risk and cybersecurity related academic literature. Using this information, we want to construct a tool for academics and researchers to use to identify trends and new technologies in cyber-risk and cybersecurity.

- For example, given a text query, a researcher would be able to obtain relevant pieces of literature and topics to use as well as visualize trends and different topic groupings.

- In addition to that, researchers would be able to suggest and add new pieces of literature into the database as well. This would become a growing repository that will continuously update with time.

### Some Takeaways
In the real world, data is never clean. The ideal is perfectly shaped data, the dimensions adjusted to our specification, and no missing values. However, reality is far from ideal. Data goes missing in transmission, findings don't turn out quite right, and sometimes, values are just forgotten about. When these accumulate, we end up with a variety of problems such as imbalanced data, missing critical values, or values that aren't representative of our actual situation. For us, we had everything from missing titles and abstracts to lists of keywords. In some cases, such as keywords, we are able to perform different methods to extract keywords. However, for larger data fields where high precision is needed (i.e. abstracts and titles), these entries would need to be deleted. These problems show the need for a unifying system for academic literature. 

Semantic representation is hard. Really hard. Being able to represent 'meaning' in a way that computers can understand still remains a challenge to cutting edge researchers to this day. The challenge for us was being able to generate a semantic representation of various keyword phrases accurately. One simple example demonstrates such challenges. Consider the word bank. What comes to mind first is a financial institution that accepts deposits from the public. Another definition is the land alongside of a sloping river or lake. However, a computer wouldn't necessarily be able to distinguish between these differences. If we gave a computer two sentences:

1. I camped by the river bank.
2. I made a deposit at the bank.

It would be a significant challenge to discern the differences in the text. A computer would ask itself, "does the river store money?," "is the bank by the lake?" and such. This simple example is just the tip of the iceberg. As we develop increasingly complex systems, with more and more parameters, these are the smallest problems we need to consider in the future.

All problems set aside, this continuous project has been a wonderful experience to get started with undergraduate research and have the freedom to explore various topics. In addition to that, working on this project has allowed me to learn skills across a wide spectrum such as data processing methods, exploratory data analysis, as well as developing models and pipelines. As this project enters the late stages of Summer and Fall, I'm excited to see where it takes us and what the tool becomes.
