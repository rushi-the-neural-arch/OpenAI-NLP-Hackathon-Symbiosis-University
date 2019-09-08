# OpenAI-NLP-Hackathon-Symbiosis-University
This repository is made in lieu of submission towards the solution of problem statement 2 of the OPEN AI NLP hackathon. The objective here is to classify the voice recordings of a call center proceeding by treating them as consumer complaints into the said categories of the automotive industry
# Consumer-Complaint-Classification-OPEN-AI
This repository is made in lieu of submission towards the solution of problem statement 2 of the OPEN AI NLP hackathon. The objective here is to classify the voice recordings of a call center proceeding by treating them as consumer complaints into the said categories of the automotive industry. 

## Dataset 

https://www.kaggle.com/dushyantv/consumer_complaints

## Methodology

### Pre-Training 

* Batching complaints from the common pool as a pair with SQUAD like format. 
* Evaluation model for pre-training used is: [SQUAD 2.0 dev](https://rajpurkar.github.io/SQuAD-explorer/explore/v2.0/dev/)

### 2D Feature Space Generation 

* For each pair from the pre-trained pool, a 2d vector is plotted on the feature space.
* The resultant magnitude of that vector is taken as a sentence embeddinng.
* This embedding is validated using the gensim wordmodel, to create the sentence level representations. 
* These representations are further clustered by *biased c-means* to find the average number of classes.
* Further, the number of classes is mapped against the existing classes of consumer complaints. 

### Model Training

* A 6 layer, 32 node wide CNN is created with the node weights initialized with the sentence level representations. 
* This network is trained on the basis of *end-member uniqueness* for each class, to define the boundary of each class of complaints. 

### Model Evaluation / Testing 

* The results are evaluated using a reverse TF-IDF matrix, mapping it with the original class matrix.
* The dot product of these matrices determines the correctness of the model:
    1. a dense matrix represents high variance and hence low accuracy 
    2. a sparse matrix represents a low variance and high accuracy.

## References 

* SQUAD 2.0 pre-training was referenced from the sequel paper on SQUAD 2.0 dataset and training strategy. 

```
Rajpurkar, Pranav, Robin Jia, and Percy Liang. “Know What You Don’t Know: Unanswerable Questions for SQuAD.” Proceedings of the 56th Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers), 2018. https://doi.org/10.18653/v1/p18-2124.
```

* Also, a shoutout to [supreetkt](https://github.com/supreetkt/Consumer-Complaints-Classification/blob/master/src/consumer_complaints.py) for providing a foundation for consumer complaints classification on text based responses! 
