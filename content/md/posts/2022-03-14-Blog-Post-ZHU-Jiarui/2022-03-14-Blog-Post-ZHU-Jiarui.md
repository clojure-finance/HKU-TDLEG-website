{:title  "clojure methods for OOP development"
 :layout :post
 :author "ZHU Jiarui"}

 ### 1. defrecord

 standard formula: **(defrecord name [& fields] & opts+specs)**
 
Record is a type in clojure. *defrecord* can be used to define Java class. Each spec consists of a protocol or interface name followed by zero
or more method bodies. 
The class features can be specified in [ ]. 

To initialize a record, one can use **(name. [features])**
e.g. for a record defined as ```(defrecord Heapnode [data lc rc])```, 
it can be initialized as ```(Heapnode. 0 nil nil)```

One thing that should be noticed is that when trying to use a record, it should be imported like Java objects, as it is complied like Java classes. 

### 2. defprotocol

standard formula: **(defprotocol name & opts+sigs)**

Protocol is an interface in clojure. 
A protocol is a named set of named methods and their signatures
It should be noted that the first parameter of all methods in the protocol is the self/this parameter (similar to python), and the second parameter is the parameter passed in when calling. 

e.g. a protocol can be defined as ```
(defprotocol HEAP (heap_pop [this]) (heap_push [this data]))```.
And then *heap_pop* and *heap_push* can be used as methods inside a clojure record.