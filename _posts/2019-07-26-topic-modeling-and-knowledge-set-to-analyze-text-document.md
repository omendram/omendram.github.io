---
layout: post
title: Document Comprehension using Machine Learning
subtitle: Use topic models and wikipedia knowledge set to build a document comprehension chatbot
cover-img: 
thumbnail-img: 
share-img: /assets/img/path.jpg
tags: [topic models, gaussian, aws, machine learning, text]
---

### Background

Extracting information from unstructured digital document is a well known problem in the field of Natural Language Processing and Machine Learning. Traditionally, this process involves various methods such as topic modelling and sentiment analysis. They rely on modeling the text based on statistical or probabilistic model and provide insight about the data that may not have been available directly. In this project, the possibility to build an architecture through the means of combining several machine learning models for text, which can parse text documents and then infer added valuable information based on an available knowledge set such as articles was investigated. 
    
It was found that for a given text document, if there is already an information available regarding the nature of the document e.g.  if it is a technical CV, a form etc, it is possible to classify and group text content after classifying them individually per line. The classification algorithms used were Softmax Regression  or Naive Bayes Classification. They can be further subjected to multiple learning models to extract information that relates to the text, but is not present in the text of the given document. The extracted information from models can be further examined through a similarity measure using word2vec models. Word2Vec  models make is possible to measure the similarity distance of the different text instances, moreover in the current work they are used to label the words extracted simultaneously using the calculated probabilistic weights. Using these set of models it can be demonstrated that they can be set up as an engine for a chatbot which will answer the queries related to the text document in question. The probabilistic modeling of the words extracted from the overall proposed model can be used to select information based on individual probabilities of the words. A prototype application has been created to partially demo the aforementioned claims.

### Classification Algorithms

### Model
