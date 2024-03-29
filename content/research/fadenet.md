## FaDe-Net [[Writeup]](/research/fade.pdf)

David An - AP Research Project

### Abstract

The rapid development of social media and online news outlets has accelerated the spread of fake news across the internet. The accessibility and convenience of social media has further driven the drastic change of information consumption. As a consequence, fake news has become a significant concern because of 1) its inevitable exposure to large populations and 2) the potential to cause significant damage in modern society. Fake news most commonly utilizes extreme examples to catch a reader’s attention [1]. The current trend is utilizing deep leaning techniques and pipeline methods to create an effective way to discriminate fake news. In the paper, we propose a model named CNN-BAM (Convolutional Neural Network with Bahdanau Attention Mechanism network) that can detect between fake and authentic news utilizing CNNs and an attention mechanism. The proposed approach is staged in three parts. The first stage is a data preprocessing stage. The second is adapting a convolutional neural network architecture for the problem. The last stage is testing the model. All of this comes together for a Fake Detection Network, or FaDe-Net. In order to validate and benchmark our results, we performed a series of metric tests on the MIT Fake News Dataset[^1] and achieved a precision rate of 90.31% as well as an accuracy rate of 88.56%. Our experiments indicate the model is more effective at fake news detection. However, this model still has a significant amount of room to improve in future research.

[^1]: [MIT Fake news Dataset](http://fakenews.mit.edu)

[Back to writing](../../blog)
