---
title: Aggregated MapReduce
date: 2021-11-28 12:00:00 -0600
categories: [Research]
tags: []     # TAG names should always be lowercase
math: true
---
Relevant papers: [[J2]({{ site.baseurl }}{% link _tabs/research.md %})], [[C2]({{ site.baseurl }}{% link _tabs/research.md %})].

We have extended our coded [scheme]({% post_url 2021-11-28-coding-&-distributed-computing %}) for a general MapReduce framework to a class of distributed algorithms, broadly used in deep learning, where intermediate computations of the same task can be combined. In this case, our goal is to execute multiple MapReduce jobs. Prior techniques reduce the communication load significantly. However, they suffer from a requirement of a similar flavor to subpacketization, i.e., they require a number of jobs that grows exponentially in the system parameters. We propose a new scheme that achieves the same load as the state-of-the-art while ensuring that the number of jobs (and hence the number of subfiles) that the data set needs to be split into remain small.

Performing large matrix-vector multiplications is a key building block of several machine learning algorithms. For instance, during each step of the forward propagation in deep neural networks, the output of the layer is the result of multiplying the matrix of the input data set with the weight vector. We formulate the matrix-vector product as a MapReduce operation and test our algorithm by executing multiple massive such multiplications using the naive method and the proposed *CAMR (Coded Aggregated MapReduce)* scheme. We now give a different interpretation of the resolvable design in terms of jobs instead of subfiles. Table 1 demonstrates the gain obtained by multiplying 512 fat matrices on 20 **AWS EC2** servers. We compare against the baseline method, which does not involve any coded transmissions, and supersede it by a speedup factor of **4.31x**.

![Table 1](/kostas_files/camr_table.png){: width="750" }
*Table 1: Time for computing 512 products **Ab**, where **A**: 234000x100 and **b**: 100x1 on 20 servers.*