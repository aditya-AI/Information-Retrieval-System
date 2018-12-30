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
       <li>Then, finally I added a MaxPool1D layer just after the embedding layer output to capture important features instead of directly passing the embedding layer output to conv or lstm layers. This further improved my performance and I finally achieved a training accuracy of around 98-99% and validation accuracy of around 80-81% approximately.</li>
       </li>
  </ul>
<p align="center">
  <img src="https://github.com/aditya-AI/Top-3-Question-Suggestions-For-A-Given-Query/blob/master/pipeline.png">
</p>
