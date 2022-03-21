{:title  "Blog one - Getting to know Cryogen"
 :layout :post
 :author "ZHANG Wenkai"}

This is the first time I learned about Cryogen, a Clojure-based static website development tool. As introduced on its [official website](http://cryogenweb.org/), it is pretty simple and easy to get started:
1.	The tool offers several well-designed themes that developers can directly use.
2.	Developers can just use markdown files to upload pages and posts (html coding is not needed).
3.	All key configurations are stored in config.edn and can be changed easily.
4.	After installing Leiningen or Clojure CLI, the developer can generate the website locally at localhost: 3000 using the command “lein serve” (in Leiningen) or “clojure -X: serve” (in Clojure CLI).
5.	Appearance settings are centralized in the themes folder and can be modified easily.

I tried to build a website template in the past two weeks. I customized the website color (reduced red area and made the color contrast more balanced), font-size (decreased the font-size), icon (added unique icon, and GitHub icon linked to the repositories), navbar (changed the order of navbar and deleted a few useless options), etc. I also tried some key markdown features and added a few contents (copyright information, a brief introduction of the website, an example post).

However, I met some problems, too. There were few tutorials about Cryogen on the internet, so all I had was the official docs of Cryogen. I was unable to deploy the website to the internet because I didn’t have enough permission to modify the github.io setting in the repository. I also had difficulty figuring out the corresponding part each HTML/CSS/JavaScript file is responsible for on the website at the very beginning but started to have some ideas after a few tests.