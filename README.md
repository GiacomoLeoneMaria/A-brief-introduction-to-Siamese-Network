# **Siamese Network SNN**

Siamese Network is a type of network architecture that contains two or more identical subnetwork used for generate feature vectors for each input and compare them. 

A Siamese Neural Network is a class of neural network architectures that contain two or more ***identical subnetworks***. Identical, here means, they have the same configuration with the same parameters and weights. Parameter updating is mirrored across both sub-networks. It is used to find the similarity of the inputs by comparing its feature vectors, so these networks are used in many applications

![siameseNN](https://user-images.githubusercontent.com/72698188/167248712-5c399204-5517-4c90-95c1-3b6ce1024522.png)

We will deal the case in whitch the SNN is to train using the Triplet Loss function.
It is based on the distance on three inputs:

- ***Anchor*** (arbitrary class of points)
- ***Positive*** (same class of the Anchor)
- ***Negative*** (different class from the Anchor)

![apn](https://user-images.githubusercontent.com/72698188/167248840-c7cdd647-6887-444e-9856-194c97ee14ea.png)

## ***Pros and Cons of Siamese Networks***

The main advantages of Siamese Networks are:
- ***More Robust to class Imbalance:*** With the aid of One-shot learning, given a few images per class is sufficient for Siamese Networks to recognize those images in the future.
- ***Nice to an ensemble with the best classifier:*** Given that its learning mechanism is somewhat different from Classification, simple averaging of it with a Classifier can do much better than average 2 correlated Supervised models (e.g. RF classifier)
- ***Learning from Semantic Similarity:*** Siamese focuses on learning embeddings (in the deeper layer) that place the same classes/concepts close together. Hence, can learn *semantic similarity*.

The downsides of the Siamese Networks can be:
- ***Needs more training time than normal networks:*** Since Siamese Networks involves quadratic pairs to learn from (to see all information available) it is slower than normal classification type of learning(pointwise learning).
- ***Doesn’t output probabilities:*** Since training involves pairwise learning, it won’t output the probabilities of the prediction, but the distance from each class

## ***Triplet loss*** 

![Immagine 2022-05-07 121626](https://user-images.githubusercontent.com/72698188/167250083-bb131d68-dd61-469c-8559-1b5035dda402.png)

When the input are the same, and so d(A,P) = d(A,N)= 0, the loss i equal to zero. This is call *trivial solution*.

To prevent trivial output, we introduce a new term call *margin*, that pushes the anchor-positive pair and the anchor-negative pair further away from each other.

![Immagine 2022-05-07 121650](https://user-images.githubusercontent.com/72698188/167250101-ba042527-a25f-4103-81cc-9b68370d1e93.png)


## ***Choosing the triplets A, P, N***

During training, if A,P and N are choose randomly, d(A,P) + margin <= d(A,N) is easily satisfied.

So we are interesting to choose triplets that are "hard" to train on.
![Immagine 2022-05-07 121723](https://user-images.githubusercontent.com/72698188/167250113-bf303705-4579-4aba-b828-bca1ca89a703.png)


In that case the learning algorithm has to try hard to keep these on the right order, so that there is at least a margin between the left and the right side. This increasing the efficiency of the learning algorithm.

Than we can apply the *Gradient Descent* to try to minimize the Cost function J.

# ***References***
[`Learning Deep Structured Semantic Models for Web Search using Clickthrough Data, Po-Sen Huang, Xiaodong He, Jianfeng Gao, Li Deng, Alex Acero, Larry Heck`](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/cikm2013_DSSM_fullversion.pdf)

[`Image similarity estimation using a Siamese Network with a triplet loss`](https://keras.io/examples/vision/siamese_network/)

[`Deep learning Specialization, Andrew Ng`](https://www.coursera.org/specializations/deep-learning?utm_source=deeplearningai&utm_medium=institutions&utm_campaign=SocialYoutubeDLSC4W4L04)

