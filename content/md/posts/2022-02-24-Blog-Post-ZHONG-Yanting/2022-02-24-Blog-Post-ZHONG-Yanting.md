{:title  "First Blog - Grace Zhong"
 :layout :post
 :author "ZHONG Yanting"}

After some back and forth, I decided on the pure computer science project – heap in Clojure, as an exploration in data structure while catering for a small technical need in Clojask.

After some research and discussion, I found that there are two main methods to approach this problem:

1. Start the construction of this data structure in Clojure from zero by defining a new type. The basic idea of a (binary) heap goes as follows:

    - For a max heap, for example, the value of the parent node must be greater than or equal to its child nodes, i.e., ```heap[k] >= heap[2*k+1]``` and ```heap[k] >= heap[2*k+2]``` for all ```k```, counting elements from zero.

    By this logic, the sorting should be starting from the last element collection and comparing ```heap[k]``` and ```heap[(k-1)/2]``` if k is odd, ```heap[(k-2)/2]``` when k is even, starting from zero.

2. Wrapping the priority queue in Java and use in Clojure. This should be a quicker method and would be the one I focus on for now. Three main aspects to work on:
    - How to define a class in Java
    - Clojure datatypes
    - How to use Java classes in Clojure

    Since I’m also new to Java, it still takes me sometime in the learning process before starting working.

I went through some materials to consolidate my foundational background.

1. Basics in data structures and algorithms, including concepts like ADT, stack, queue, priority queue and heap.
2. Clojure-by-examples.
3. Java tutorials.

I encountered some challenges with regard to the project - mainly the study of these languages since I’m new to both Java and Clojure. While having used heap in Python as a starting point to understand this data structure, the remaining problem would be how to move this idea to new languages.

Based on the plan above, I will continue to be studying Java and Clojure and working on wrapping the priority queue in Java.