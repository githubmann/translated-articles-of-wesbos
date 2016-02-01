#### the original http://wesbos.com/javascript-modules/
#An Intro To Using npm and ES6 Modules for Front End Development
#### 将npm 和ES6模块机制用在前端开发中的一些相关信息

####A big thanks to bitHound for sponsoring my time to research and write this article. Check out their service, which provides continuous analysis and quality checks for both your front and back end JavaScript and its dependencies.
####很感谢bitHound赞助我研究和撰写这篇文章。研究他们的提供的服务，他们的服务提供了持续的分析和质量的检查，在前端和后端的js和其相应的依赖。

####The JavaScript landscape is changing quickly and along with it the way that we work with dependencies in our websites and applications.
#### js变化得非常快并且充满着依赖的特性

#### This post is for developers who are currently loading in their JavaScript via multiple script tags and finding that dependency management is becoming a little cumbersome as their webpages or applications start to grow.
#### 这篇博文，建议那些正加载他们的JS,通过多种js变迁和寻找依赖解决方案将变得重要因为他们的网页和应用的访问量开始增长了

#### For a deep dive into everything the spec has to offer, as well as some great comparisons to CommonJS and AMD, check out Axel Rauschmayer’s Exploring ES6 book, particularly chapter 17.
#### 因为一个深潜到任何事，必须提供，还需些好的来比较CommonJS和AMD ，可以浏览Axel Rauschmayer的探讨ES6，特别是第17章