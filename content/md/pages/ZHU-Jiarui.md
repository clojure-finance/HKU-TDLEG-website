{:title "Development of heap structure for data storage and output in Clojure"
 :layout :page
 :page-index 5
 :navbar? true}

Contributor: ZHU Jiarui

Heap is a kind of efficient data storage structure, especially in the representation of priority queues. So it is a good choice for data logging, sorting and output.

Existing implementations are mostly based on index operations in vectors, rather than the real tree structure. This kind of structure cannot meet the requirements for efficient computing. 

In this case, we need a maximum/minimum heap implementation scheme that is more in line with the characteristics of the heap.

### [Proposal](/pdf/Proposal-ZHU-Jiarui.pdf)

### Blogs
[clojure methods for OOP development](/posts-output/2022-03-14-Blog-Post-ZHU-Jiarui/2022-03-14-Blog-Post-ZHU-Jiarui)<br/>

### [Report](/pdf/Report-ZHU-Jiarui.pdf)