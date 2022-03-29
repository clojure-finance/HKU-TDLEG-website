{:title "Development of Heap Structure for Data Storage and Output in Clojure"
 :layout :page
 :page-index 4
 :navbar? true}

## Contributor
ZHU Jiarui

## Description
Heap is a kind of efficient data storage structure, especially in the representation of priority queues. So it is a good choice for data logging, sorting and output.

Existing implementations are mostly based on index operations in vectors, rather than the real tree structure. This kind of structure cannot meet the requirements for efficient computing. 

In this case, we need a maximum/minimum heap implementation scheme that is more in line with the characteristics of the heap.

## Blogs
- [Clojure Methods for OOP Development](/posts-output/2022-03-14-Blog-Post-ZHU-Jiarui/2022-03-14-Blog-Post-ZHU-Jiarui)

## Details
- [Proposal](/pdf/Proposal-ZHU-Jiarui.pdf)
- [Summary report](/pdf/Report-ZHU-Jiarui.pdf)
- [GitHub repository](https://github.com/clojure-finance/clojure-heap)