# Machine learning

## Precision, recall, F1 score
￼￼
F1 score, which tells you how well you’re doing on finding the ground truth anomalies given a certain threshold. Compute the resulting F1 score by computing how many examples the current threshold classifies correctly and incorrectly.
The F1 score is computed using precision (prec) and recall (rec):

* tp is the number of *true positives*: the ground truth label says it’s an anomaly and our algorithm correctly classified it as an anomaly.
* fp is the number of *false positives*: the ground truth label says it’s not an anomaly, but our algorithm incorrectly classified it as an anomaly.
* fn is the number of *false negatives*: the ground truth label says it’s an anomaly, but our algorithm incorrectly classified it as not being anomalous.

## Octave/Matlab code
```
pred = (pval < epsilon);
    
# spravne uhodnute anomalie podle yval
tp = sum((yval & pred));
    
# neni to anomalie, ale algoritmus rika ze jo
fp = sum((yval == 0 & pred == 1));
    
# je to anomalie, ale algoritmus rika ze neni
fn = sum((yval == 1 & pred == 0));
    
precision = tp/(tp+fp);
recall = tp/(tp+fn);
    
F1 = (2*precision*recall)/(precision+recall);
```

## Photo OCR

(Photo optical character recognition)


### Problem description and Pipeline

1. Text detection
2. Character segmentation
3. Character classification
4. Spelling correction

### Photo OCR pipeline
Image → Text detection → Character segmentation → Character recognition

### Sliding Windows
(Pedestrian detection)

Text detection → Expansion 



## Přednáška Jiřího Materny a další zápisky

Capsule neural network

https://en.wikipedia.org/wiki/Capsule_neural_network

LSTM

http://colah.github.io/posts/2015-08-Understanding-LSTMs/

Stacked long Short-Term memory networks

https://machinelearningmastery.com/stacked-long-short-term-memory-networks/

Introduction to recurrent neural networks

https://deeplearning4j.org/lstm.html

Bayes' theorem

https://en.wikipedia.org/wiki/Bayes%27_theorem

Další

https://github.com/terryum/awesome-deep-learning-papers#optimization--training-techniques
