Graphlet Counting and Node Embedding for Graph Classification؛
In our study, we focus on computing the count number of graphlets for each subgraph in our dataset, totaling 756 unique subgraphs. We explore three different approaches for graphlet counting and compare their execution time and accuracy: 

-Exact Counting: 
We implement a function to precisely count the number of graphlets for each subgraph, varying the graphlet length. Multiple lengths are considered to assess their impact. 

-ESU Algorithm: 
To approximate the graphlet count, we employ the ESU algorithm, aiming to enhance time complexity. In our experiments in one of our personal systems(Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz -  Intel Corporation UHD Graphics 620), for length 3 graphlets, the exact counting method took 4 minutes and 47 seconds, while the ESU algorithm achieved this in only 1 second, showcasing a substantial improvement in execution time. The accuracy of the ESU estimates closely aligns with the real numbers. For each approach, the results are stored in a text file, following the format of our original dataset. Each line corresponds to a subgraph, denoting the number of graphlets. 

-Cyclic Graphlets:
We implement a function to count only cyclic graphlets. However, results were not satisfactory, especially for cycles of length 3 or 4, where most counts were zero. For longer cycles (length 6 or higher), counts hovered around 2 or 3, providing limited predictive value. 

Color-Coding Approach: 
An alternative approach, utilizing color-coding to approximate the number of graphlets, was explored. Despite faster execution compared to exact counting, the significant gap between correct and approximate counts rendered this method less suitable for our prediction task. 

Node2Vec for Node Embeddings: 
Employing the Node2Vec algorithm, we learn node embeddings in a graph.To capture meaningful representations of nodes in the graph, the Node2Vec algorithm is employed with specific configuration parameters: 
Number of Walks (num_walks): The graph is traversed multiple times to generate random walks. In this case, num_walks is set to 10, determining the number of walks per node. 
Walk Length (walk_length): Each walk consists of a sequence of nodes. The walk_length parameter, set to 30, determines the length of each individual walk.

To implement this approach, we employ a virtual node technique. We consider each graph as a node and create a new graph with 756 nodes. For each edge, we evaluate the similarity between two graphs as a weight. Then, we split our dataset into training and testing sets to train and learn our model. We test different similarities, such as the number of edges, nodes, cycles with length 6, and exact and approximate graphlets with lengths 3 and 4 in each graph. Also, for classifiers, we use Logistic Regression, which is a good classifier for binary classification tasks. When we run this technique, the best results (accuracy 63%) occur when we use the exact number of graphlets with length 3 for the similarity function. 

At the end we implement our classification using PyTorch and a two-layer neural network model.
The neural network is defined as a class named TwoLayerModel that inherits from nn.Module. It consists of two fully connected layers (nn.Linear) with a ReLU activation function in between. The forward method defines the forward pass through the layers.The loss function (nn.CrossEntropyLoss), optimizer (Stochastic Gradient Descent), and learning rate(0.01) are defined and trained for 100 epochs.
The result was almost similar to the previous method (60%) BUT a little bit less.
