---
layout: post
title: Recommendation System for Researchers based on Research Proposals
subtitle: Using topic modeling and multiple selection algorithms to recommend a suitable cluster of candidates
cover-img: 
thumbnail-img: 
share-img: /assets/img/path.jpg
tags: [topic models, naive bayes, recommendation, sublinear algorithms, nlp]
---

## Introduction
One of the main challenges in a collaborative research are finding researchers that would like to collaborate and are also compatible based on their experience in certain domains. Due to the multidisciplinary approach, researchers are bound to leave their area of research in order to find collaborators. As they may en- ter less known areas or even unknown ones, the search for collaborators can become increasingly difficult. Most often, collaborators are found by the network of super- visors and co-authors, causing the network not to be ex- tended to its full potential and authors sticking to their known hub. This can cause a decrease research quality, as most probably the researchers won’t collaborate with the needed experts in the fields.

By automating the process of finding collaborations, this problem can be solved efficiently. New collaborations can be proposed by a recommender system, and ideally, can be applied to Maastricht University. With such a system, it saves the researchers the time that they oth- erwise would have spent on finding collaborators by hand or waiting for collaborators to come to them, while now they can focus on doing research instead. This leads to the following research questions: 
1. Can a recommender system be built by publicly available data? 
2. Can a recommender system be automatically up- dated when new data is available? 
3. Can a recommender system suggest useful research collaborations for UM, despite the limited amount of data available from the UM?

### Model
By combining an architecture consisitng of various topic models to construct a weighted graph of each of the researchers publication backgroung we can establish a system that would rank the researchers based on their compatibility.

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/recommendation-model.png" width="500">
