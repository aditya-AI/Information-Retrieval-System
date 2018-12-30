# Top-3 Question Suggestions For A Given Query

<p align="center">
  <b><h2><ins>Motivation</ins></h2></b><br>
</p>  

In the following steps, I will discuss how I approached the problem of quora question pairs and the motivation for coming up with an architecture like Siamese network.

<b><ins>How and why I chose the Siamese based network?</ins></b>
<ul>
  <li>Having worked on computer vision in domains like medical imaging, biometrics, and document image super-resolution, I approached the problem of deciding the architecture for the quora question pairs dataset based on specifically biometrics.</li>
   <li>While I was working on medical imaging at IIT Mandi, I also worked on a bit of biometrics domain wherein I had palm & knuckle print images of the left & right hand. Similar to that, in this problem I had question 1 & question 2 as an input. Hence, I went with the best possible approach of using a <b>Siamese based network.</b></li>
   <li>Even though the task was to find from a pool of questions which top-3 questions are closer to the user inputted question, to solve this problem, classifying given two questions are they similar or dissimilar was essential. The dataset had same questions repeated multiple times against different set of questions, so the network learned meaningful and discriminative features which eventually helped in solving the prime task of finding top-3 suggestions.</li>
   <li>A siamese network had two inputs and it works on a phenomenon of sharing weights. The network’s input was question 1 and question 2 as tokenized vectors each of length 103, label being 0 or 1.
</li>
   <li>I tried a variety of architectures for the siamese network. Note that there are three functions in my network namely Embedding, Siamese, Predict. Following are some of architectural changes I made in my siamese function:
     <ul>
       <li>Fully Conv1D siamese network which gave a validation accuracy of around 75%. This had multiple combinations of conv1D layers.</li>
       <li>Conv1D + LSTM + Dense (In sequence) along with MaxPool1D layer which gave me a 2% boost in validation accuracy (~78%).</li>
       <li>Then, finally I added a MaxPool1D layer just after the embedding layer output to capture important features instead of directly passing the embedding layer output to conv or lstm layers. This further improved my performance and I finally achieved a training accuracy of around 98-99% and validation accuracy of around 80-81% approximately. The final architecture is simple and smaller in size consisting of just one maxpooling, lstm and dense layer in the Siamese function.
</li>
       </li>
  </ul>
<p align="center">
  <img src="https://github.com/aditya-AI/Top-3-Question-Suggestions-For-A-Given-Query/blob/master/pipeline.png">
</p>

<b><ins>Finding the top-3 closest match for the given query question</ins></b>

<ul>
  <li>Since the goal of this task was to find from a pool of questions (training data) which top-3 questions are closer to the user inputted question (validation data).
</li>
   <li>In order to accomplish this, I broke my siamese network and created a new model which had just two functions namely Embedding and Siamese functions.
</li>
   <li>At test time the input was fed to the embedding layer and further extracted features from the Siamese function that had a Dense layer outputting 128 features maps. (Input being training and validation questions fed one at a time).
</li>
   <li>Finally, saved these features representations to the disk especially the training feature maps so that I did not have to compute the predictions again and again.
</li>
   <li>This process of extracting features was computationally efficient as I got features for all the training data (~650K) by processing them only and only once.
</li>
   <li>The feature maps were further reshaped to get a two-dimensional array in which the first dimension was all the training questions (1 & 2) and the second dimension was the size of the feature map (128).
</li>
  </ul>
  





