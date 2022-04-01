{:title  "Blog Two - Being Part of the INTERNET"
 :layout :post
 :author "Kevin ZHANG Wenkai"}

The website has been successfully deployed on the internet in the last two weeks. Its link is https://clojure-finance.github.io/HKU-TDLEG-website/ . I have uploaded six posts onto the website and updated the ```home```, ```about```, and ```content``` pages to make the website look more professional. I have developed a well-organized way to manage all the posts and pages: I now keep each markdown file and its images in one single folder under ```content/md``` instead of all images under ```content/img```. In this way, images in different posts can have the same name, and posts can be moved easily without worrying about losing their images. I also tried to do a version control: I keep a copy of the former version of the website locally in case the newer version messes up.

I also met some problems. Although math formulas can be shown correctly in the preview of the website, Cryogen cannot recognize them. In the end, I managed to solve it by adding a few lines of JavaScript codes, which converted plain MathJax lines to corresponding formulas. But some complex formulas still cannot be rendered. Another problem is that the website showed dates in Chinese. It seemed that the dates were automatically generated, and their language was based on the developer’s system language, which in my case is Chinese.

I think I will figure out how to change the language of the dates in the next few weeks. If it cannot be solved by coding, I will try to change my system language into English.