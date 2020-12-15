



### Introduction

In this particular case, the novel in use is called “And Then There Were None” from the famous author Agatha Christie. Mystery novels provide a good use-case of events extraction and also co-reference resolution, as all the information is formatted in a way that would be entertaining to the readers. One of the main challenges in terms of mining structured information from a story is how to build the right model and a classifier, to identify the important chunks of text from a large text wall. Stories, specifically in case of mysteries and thrillers, do not necessarily follow a linear pattern as many authors use nonlinear storytelling as one of the plot devices, so it poses an interesting question on how can we determine a correct timeline of events. There is a lot of information that is given which serves as a distraction element rather than actually stating a fact in a story. How can we mine a fact that is not blatantly stated, or can we actually extract that information? In this case, there are a lot of dynamics going on which can make it hard to predict things based on simple mathematical models, however there is still quite a bit that can be extracted just by discarding the chunks of text which are not providing a significant turn in a story. In the following sections, we will take a look at all the techniques applied to extract information from the story by the means of text mining.

### Dataset and Workflow

The process will start by extracting tokens from the text file. These tokens can then be used to apply TF-IDF to the novel, which will be used to extract relevant subsections. After thresholding, part of speech tagging will be applied to the set of most relevant documents. Using this part of speech tagging entities can be extracted based on their tags. Further extraction will take place to retrieve only the relevant characters of the novel. Afterwards a Naive Bayes classifier and a Support Vector Machine will be applied to classify sentences of the retrieved subsections of the novel to extract sentences where a murder might have taken place. Two classifiers will be implemented to compare classifying results and to find the classifier which works best for this task. Finally, we use co-reference resolution to retrieve specific information from the sentences which were classified as sentences where a murder happened.

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/workflow.png" width="500">

### Event Timeline

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/timeline.png" width="500">


### SVM and Naive Bayes Classifiers


### Coreference Resolution
After retrieving the meaningful sentences with the help of the classifiers above, the information and events, need to be associated to the individual entities. Which, poses the question of co-reference resolution, as there are descriptions involving multiple events(murders) on the single sentences. In order to do this, a grammar rule was applied on the tagged datasets. 

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/coref1.png" width="500">


This rule helped in dividing the sentences, extracting entities, and 8 extracting events for those entities, which also contained the locations and the circumstances of their murders. The grammar rule was applied by using the chunking methods provided by NLTK. We designed it to extract, group of people, the events and also if they shared an event.

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/coref2.png" width="500">

### Results

|Entities | Last alive | Method |
| :------ |:--- | :--- |
| Mrs. Rogers | DocNr: 43 | Overdose of chloral |
| Anthony Marston | DocNr: 59 | Cyanide poisoning |
| General Macarthur | DocNr: 112 | Skull was fractured |
| Mr. Rogers | DocNr: 156 | Head was split open with a chopper |
| Miss Brent | DocNr: 173 | Cyanide poisoning |
| Justice Wargrave | DocNr: 190 | Shot through the head |
| Armstrong | DocNr: 201 | Drowned |
| Blore | DocNr: 226 | Head was crushed in |
| Philip Lombard | DocNr: 240 | Shot through the heart |
| Vera Claythorne | DocNr: 244 | Hanged |

#### Naive Bayes vs SVM
On the test set Naive Bayes gave an accuracy of 90% while the Support Vector Machine gave an accuracy 92.1%. The classifiers are better at recognizing the Non-Murder sentences, which could because we needed to build the murder dataset by hand, so there is a chance that the classifiers would perform even better with a larger dataset.

<img src="https://github.com/omendram/omendram.github.io/raw/master/assets/img/nbvssvm.png" width="300">

### 
