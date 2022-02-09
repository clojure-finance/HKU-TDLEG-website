{:title  "Blog Post (Twitter)-LIN Maoran_20220102"
 :layout :post
 :author "LIN Maoran"}

This is the starting point for me to code an economic model using Clojure.

It is my first time to use a Java dialect. Therefore, multiple problems happened when I tried to depict some math calculation in the program.

1. The first issue is to have natural exponential functions and natural logarithm functions. For Clojure, it does not have a built-in exponential function. So, we could do it ourselves using the “repeat”, which could be found in this [tutorial](http://kimh.github.io/clojure-by-example/#about).

    For natural exp and natural log, we could directly use the Java language “Math/log” and “Math/exp”, which is one of the merits in Clojure!

2. Second, when running the program, the Clojure reported this issue to me multiple times: class java.lang.String cannot be cast to class java.lang.Number.

    It seems that the Clojure have misinterpreted the data type I would like to input. Therefore, I need to directly define the types of my inputs, which was found in a [community Clojure Docs](https://clojuredocs.org/clojure.core/double).
    
    We could use the function (double x) or (int x) to coerce the data into numbers we want. If it does not work, we could even use the Java languages (Double/parseDouble x) or (Integer/parseInt x)!

After resolving these issues, I could continue with my depiction. Definitely, the upcoming problems will be much more difficult than the aforementioned issues. Hence, I will try my best to enrich my knowledge to smooth my workflow.