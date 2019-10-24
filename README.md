## CAS Project 
### Presented David Xiong and Helen Bai. 
### This IBDP CAS Prjecet with its IP are assets of Air Sealand Inc.
#### ALL RIGHTS RESERVES ©

### Encryption
Every data in the database requires encrypt, otherwise the security for information won't exist anymore. We all know that there are encryption algorithms, but how do them work? This python programming will illustrate it. To be specfic, this programming illustates how AES, a kind of asymmetirc encryption algorithms, works. Inside the algorithm, there is the utilization of further math works as Euler Theorem. 

[illustation_for_AES](codings/IllustrationForAES.py)

![AES_algorithm](pictures/AES_illustation.png)

sample program is shown below
```ruby
import time as t
PrivateKey1=eval(input("Choose one:"))
PrivateKey2=eval(input("Choose another:"))
ClockNumber=eval(input("The size of the clock:"))
BaseNumber=eval(input("Base:"))

def getPPN(P1,P2,CN,BN):
    PPN1=((BN)**(P1))%CN
    PPN2=((BN)**(P2))%CN
    return PPN1,PPN2

def getShared(PPN,PK,CN):
    Remain=PPN%CN
    i=1
    while i < PK:
        Remain=(PPN*Remain)%CN
        i+=1
    return Remain
start=t.clock()
PPN1,PPN2=getPPN(PrivateKey1,PrivateKey2,ClockNumber,BaseNumber)
timeneed=t.clock()-start
print("PPN1,PPN2:",PPN1,PPN2)
print("timeneed:",round(timeneed,4))
print(getShared(PPN1,PrivateKey2,ClockNumber))
print(getShared(PPN2,PrivateKey1,ClockNumber))
```
### Compression

### Graph Theory

In mathematics, graph theory is the study of graphs, which are mathematical structures used to model pairwise relations between objects. A graph in this context is made up of vertices which are connected by edges. A graph can be directed or undirected, weighted or unweighted. 

#### 1.Minimum Spanning Tree

A minimum spanning tree (MST) is a subset of the edges if a connected, edge-weighted undirected graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight. The graph below is a planar graph and its minimum spanning tree. Each edge is labeled with its weight so this is a weighted graph. 

![Planar Graph](pictures/600px-Minimum_spanning_tree.png)

##### a.Kruskal Algorithm

##### b.Prim's Algorithm

##### c.Dijstra Algorithm

Someone said Dijstra creates this algorithm using just 20 minutes. However, I learned how to code using greedy far more than 20 minutes. 
[result_of_programming](codings/Dijkstra_v1.py)
![Dijstra_Graph](pictures/Dijkstra_illustration.png)

```ruby
import networkx as nx
import matplotlib.pyplot as plt

def Dijkstra(G, start, end):
    RG = G.reverse()
    dist = {}
    previous = {}
    for v in RG.nodes():
        dist[v] = float('inf')
        previous[v] = 'none'
    dist[end] = 0
    u = end
    while u != start:
        u = min(dist, key=dist.get)
        distu = dist[u]
        del dist[u]
        for u, v in RG.edges(u):
            if v in dist:
                alt = distu + RG[u][v]['weight']
                if alt < dist[v]:
                    dist[v] = alt
                    previous[v] = u
    path = (start,)
    last = start
    while last != end:
        nxt = previous[last]
        path += (nxt,)
        last = nxt
    return path
```

#### 2.Chinese Postman Theorem

### PageRank

Pagerank is really important when you want to search something in the searching engine. Imagine billions of results with the same key words jumping out at the same instant. Unrelated information will decrease the efficiency to even zero or negative. So here it is, pagerank. It involves in the thought of modeling and simulation. Plus, possiblities! There is even an animation of it! Have a look! [result_of_programming](codings/PageRank_test.py)
![A_Graph](pictures/PageRank_illustation.png)

### Perceptron

Do you know what a neural network is? Well, basically, it's artificial intelligence. It's cool. So what is it made of? Perceptron! That's it, something used to solve binary variables questions. It has a variety of usages, from showing logic gates, to predict the breed of iris. [see_the_programming](codings/perception.py)
![result_pictures](pictures/Perceptron_illustration.png)

### Artificial Neural Network

![Artificial Neural Network analogy](pictures/neuron.png)

As we mention above, artificial neural network is actually a combination of mathematical models. Under supervised learning, the model can work similiar to human brain's neural system. During the initialization process, every node is connected to each other with a random weight and each node use a non-linear function such as Sigmoid or ReLU function. After the running the they system for the first time, the model will calculate the different between the actual results and the expected results, and then make modification to the weight that are pre-determined, which is called back propogation. 
![ANN Net](pictures/nueral_net.jpg)

```ruby
import numpy as np
import math
import random

from numpy.core._multiarray_umath import ndarray


class ANN:
    def __init__(self,weights_input_hidden,weights_hidden_output,result,input,time_of_iterate=0):
        self.weights_input_hidden = weights_input_hidden
        self.weights_hidden_output = weights_hidden_output
        self.result = result
        self.input = input
        self.time = time_of_iterate
        self.error = None
        self.o_delta = None
        self.sum = None
        self.calculated_value = np.zeros([3,1])
        self.hidden_error = None
        self.hidden_delta = None

    def sigmoid(self,x):
        return 1.0/ (1.0 + math.exp(-x))

    def sigmoid_derivative(self,x):
        return x*(1-x)

    def random_weight(self):
        return round(random.random(),2)

    def get_weight_input_hidden(self):
        return self.weights_input_hidden

    def get_weight_hidden_output(self):
        return self.weights_hidden_output

    def get_time_of_interate(self):
        return self.time

    def get_input(self):
        return self.input

    def get_result(self):
        return self.result

    def initialize(self):
        a = ANN
        for i in range(np.shape(self.weights_input_hidden)[0]):
            for j in range(np.shape(self.weights_input_hidden)[1]):
                self.weights_input_hidden[i][j] = round(random.random(),2)
        for k in range(np.shape(self.weights_hidden_output)[0]):
            for l in range(np.shape(self.weights_input_hidden)[1]):
                self.weights_hidden_output[k][l] = round(random.random(),2)

    def feedforward(self ,sum=0 ,node_num=0):
        a = ANN
        while node_num<3:
            hidden_neuron_input = np.sum(np.dot(self.input[self.time], self.weights_input_hidden[node_num]))
            #print("The " + str(node_num+1) + " sum of one node is " + str(hidden_neuron_input))
            result = 1.0 / (1.0 + math.exp(-hidden_neuron_input))* self.weights_hidden_output[0][node_num]
            #print(str(self.weights_hidden_output[0][self.time]))
            #print('The ' + str(node_num) + ' result is ' + str(result))
            self.calculated_value[node_num] = result
            self.sum = np.sum(self.calculated_value)
            node_num+=1
        self.time+=1
        self.sum = 1.0/ (1.0 + math.exp(-self.sum))
        return self.sum

    def back_propagation(self):
        a = ANN
        self.error = self.sum-self.result[self.time-1][0]
        self.delta = self.error*(1.0/(1.0 + math.exp(-self.result[self.time-1][0])))
        self.hidden_error = np.dot(self.delta,self.weights_hidden_output)
        adjustment = 1.0/(1.0+ math.exp(self.calculated_value[0]))
        self.hidden_delta = self.weights_input_hidden*adjustment
        #self.hidden_error = np.reshape(self.hidden_error,[3,1])
        self.weights_input_hidden += self.hidden_delta
        self.weights_hidden_output += self.hidden_error
        print("----------weights_input_hidden------------")
        print(self.hidden_delta)
        print(self.hidden_error)
        print("----------weights_hidden_output------------")

        return self.weights_input_hidden, self.weights_hidden_output

    def train(self):
        a = ANN(self.weights_input_hidden,self.weights_hidden_output,self.result,self.input)
        a.initialize()
        n = len(self.input)
        while n>0:
            print('This is the ' + str(self.time+1) + " iteration")
            print("The weights between the input layer and the hidden layers are")
            print(self.weights_input_hidden)
            print("The weights between the hidden layer and the output layers are")
            print(self.weights_hidden_output)
            a.feedforward()
            a.back_propagation()
            n-=1


input = [[99,1],[97,3],[43,57],[26,74],[90,10],[80,20],[50,50],[39,61],[70,30],[75,25],[99,1],[97,3],[43,57]]
result = [[0.98],[0.983],[0.3],[0.4],[0.91],[0.85],[0.2],[0.38],[0.6],[0.77],[0.98],[0.983],[0.3]]
learning_rate = 0.5
weights_a = np.array([[0.5,0.5],[0.5,0.5],[0.5,0.5]])
weights_b = np.array([[0.5,0.5,0.5]])

if __name__ == "__main__":
    a = ANN(weights_a,weights_b,result,input)
    a.train()


```
### How Artificial Neural Network works?
An ANN usually involves a large number of processors operating in parallel and arranged in tiers. The first tier receives the raw input information -- analogous to optic nerves in human visual processing. Each successive tier receives the output from the tier preceding it, rather than from the raw input -- in the same way neurons further from the optic nerve receive signals from those closer to it. The last tier produces the output of the system.

Each processing node has its own small sphere of knowledge, including what it has seen and any rules it was originally programmed with or developed for itself. The tiers are highly interconnected, which means each node in tier n will be connected to many nodes in tier n-1 -- its inputs -- and in tier n+1, which provides input data for those nodes. There may be one or multiple nodes in the output layer, from which the answer it produces can be read.

Artificial neural networks are notable for being adaptive, which means they modify themselves as they learn from initial training and subsequent runs provide more information about the world. The most basic learning model is centered on weighting the input streams, which is how each node weights the importance of input data from each of its predecessors. Inputs that contribute to getting right answers are weighted higher.
