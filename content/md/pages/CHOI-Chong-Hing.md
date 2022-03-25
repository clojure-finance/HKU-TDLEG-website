{:title "Data Processing Domain-Specific Language in Clojure"
 :layout :page
 :page-index 3
 :navbar? true}

Contributor: CHOI Chong Hing

Domain Specific Language (DSL) is a computer language, declared syntax or grammar that is specialised to a specific application. In contrast to General-Purpose Language, implemenation of DSL is designed with specific goals in that application domain. The use of macros in Lisp dialects enables developers to rewrite source code at compile time, making implementation of DSL more convenient. As one of the Lisp dialects, Clojure also inheriates such advantage. In addition to macros, the heavy use of core data literals in Clojure also gives an extensive developing opportunity in implementing DSLs.

In this project, a DSL extension to the existing data processing library, ```tech.ml.dataset```, will be developed. A generic query using core data literal serves as the foundation of the DSL. This enables huge flexibility in defining the syntax, subject to Clojure’s limitation.

### [Proposal](/pdf/Proposal-CHOI-Chong-Hing.pdf)

### Blogs
[Implementation of Query Foundation](/posts-output/2022-01-29-Blog-Post-CHOI-Chong-Hing/2022-01-29-Blog-Post-CHOI-Chong-Hing)<br/>
[Syntax Design](/posts-output/2022-02-26-Blog-Post-CHOI-Chong-Hing/2022-02-26-Blog-Post-CHOI-Chong-Hing)<br/>
[Sort-by Function Implementation](/posts-output/2022-03-12-Blog-Post-CHOI-Chong-Hing/2022-03-12-Blog-Post-CHOI-Chong-Hing)<br/>

### [Report](/pdf/Report-CHOI-Chong-Hing.pdf)

### [Poster](/pdf/Poster-CHOI-Chong-Hing.pdf)