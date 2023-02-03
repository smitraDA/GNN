# GNN:Graph Neural Network

Title: 
To compare different algorithm for link prediction in real world complex network with Neighborbased Method , Network Embedding Method(Deepwalk & Node2Vec) and Advance Network Embedding Method(Graph Neural Network Model).

              Abstract with Application :
Real world complex networks grow over time. An important concern about complex network is Link Prediction.This Link prediction is used to infer if a link is likely to be formed in future.
(Suggesting collaborations between researchers based on co-authorship)
(Recommending new friends in online social networks)
(Query suggestions for search engines)
(Predicting new protein interactions)
(Predicting connections between members of terrorist organizations who have not been directly observed to work together)

            Keywords:
Link Prediction, Grapth Theory,Neighborbased, Network Embedding, Deep Walk, Node2Vec, GNN

(IMRAD)
Introduction:
For this project I have used co-author network datasets which has 5,242 nodes and 11,696 edges. This is a undirected graph and each author has about 4 co-authors(neighbors). 
Training set: all positive:11,496 edges (I,e linked pair of node). Can add some negative link 1:1 to 10. 
Validation set:100+10,000=10,100(1+:100-); Known lebel
Test set:100+10,000=10,100; hide lebel  until percentage scoring done. 
My objective is to  rank the unlabeled edges in the test set. For each pair of nodes in the test set, my program has computed a proximity score. I have ranked the 10,100 pairs of nodes according to the computed proximity score in descending order and output the Top-100 edges (or pairs of nodes) with the highest proximity score.

 Neighborbased Method:

Step1:  To find the neighbours of all nodes(train+test+validation)
Step2: Calculate the proximity score of all nodes with Jacarrad similarity

Score(u,v)= N(u)∩ N(v)/ N(u) υ N(v)

Step3: Apply the step 2 to test data and sort the top 100 by descending order.

Discussion:
This method returned only 40% accuracy rate. This method didn’t need train any model and hence also needed not validation.
Even there are different methods for link prediction, Neighborhood based method provided a intuitive result for the computed predictions with it’s simplicity.

Network Embedding Method(Deep Walk & Node2Vec):

Step1(Relating with word2vec): 
The Network embedding works same way as word2vec skip-gram model of NLP. In word2vec skip-gram model , Given a specific word in the middle of a sentence (the input word), the network will tell us the probability for every word in our vocabulary of being the “nearby word” that we chose. For example, if you gave the trained network the input word “Soviet”, the output probabilities are going to be much higher for words like “Union” and “Russia” than for unrelated words like “watermelon” and “kangaroo”.
Here the sentence is already a corpus and thus by default can embed graph  with all word as ‘Nodes’ and connection to next word is ‘link’.

 

 


But in Node2Vec we will have to make the corpus by tweakable (by hyperparameters, (for deepwalk no tweak possible)) sampling strategy( generating random walks from each node of the graph).
            
        


Step 2(Goal and process outline):

 

 
1.	Encoder= DeepWalk,Node2vec
2.	Node similarity function= dot product or cosine similarity(smaller angular distance is close,cos0=1)
3.	
 
 

 
Step3(Process ):
 

 
Negative sampling or Hiararchical Softmax used for optimization
 

 
Step 4 :(Node2vec’s tweak parameter)
Node2vec  sampling strategy, accepts 4 arguments:
— Number of walks: Number of random walks to be generated from each node in the graph
— Walk length: How many nodes are in each random walk
---P controls the probability to go back to <t> after visiting <v>.
---Q controls the probability to go explore undiscovered parts of the graphs. This is somewhat like the perplexity parameter in tSNE, it allows to emphasize the local/global or DFS/BFS structure of the graph.
Also the weight of the edges.
And also the standard skip-gram parameters (context window size, number of iterations etc.)
Using the sampling strategy, node2vec will generate “sentences” (the directed subgraphs) which are will be used for embedding just like text sentences are used in word2vec.

  Discussion:
This method returned  64% accuracy rate with walk length 20 and random starting with each node 5.
With Node2vec there are additional two default parameter as P and Q, by which we can fine tune and get some better performance.

Advance Embedding method(Graph Convolutional Network):

More flexibility in terms of fine tuning and hence better performance.

