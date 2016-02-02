#### the original http://wesbos.com/javascript-modules/
#An Intro To Using npm and ES6 Modules for Front End Development

  将npm 和ES6模块机制用在前端开发中的一些相关信息

A big thanks to bitHound for sponsoring my time to research and write this article. Check out their service, which provides continuous analysis and quality checks for both your front and back end JavaScript and its dependencies.

  很感谢bitHound赞助我研究和撰写这篇文章。研究他们的提供的服务，他们的服务提供了持续的分析和质量的检查，在前端和后端的js和其相应的依赖。

The JavaScript landscape is changing quickly and along with it the way that we work with dependencies in our websites and applications.

    伴随着JavaScript世界日新月异的变化，我和我们的网站以及应用中的各种依赖文件打交道的方式也在发生着变化

This post is for developers who are currently loading in their JavaScript via multiple script tags and finding that dependency management is becoming a little cumbersome as their webpages or applications start to grow.

    这篇博文，适合于那些仍然用多个script标签加载js，发现随着他们的网页数量和应用规模扩大，依赖管理将变得越来越麻烦

For a deep dive into everything the spec has to offer, as well as some great comparisons to CommonJS and AMD, check out Axel Rauschmayer’s Exploring ES6 book, particularly chapter 17.

  如果想要深入了解ES6模块规范内容，以及它和Commonjs和AMD的差别，请查看Axel Rauschmayer’s Exploring ES6 book，尤其适合第17章

  #What are JavaScript Modules?
  
  什么事JS模块

JavaScript modules allow us to chunk our code into separate files inside our project or to use open source modules that we can install via npm. Writing your code in modules helps with organization, maintenance, testing, and most importantly, dependency management.

js模块机制让我们可以将模块化代码组织在分离的文件，或者通过Npm安装开源的模块来使用。将你的代码模块化组织可以利于组织，维护，测试，更重要的是以来管理。

When we write JavaScript, it’s ideal if we can make modules that do one thing and one thing well. This separation allows us to pull in various modules only when we need them. Modules represent the core principle behind npm — when we need specific functionality, we can install the modules we need and load them into our application.

在我们使用js时，让模块做一件事，并且做好，这是不错的想法。仅当我们需要模块的时候，我们可以给独立的文件拉入模块。其实在npm背后，模块才是核心。有时候我们需要一些很特别的功能，我们可以安装我们需要的模块，并将模块加载入我们的应用中

As time goes on, we’re seeing fewer large frameworks that do everything under the sun while seeing more small modules that do one thing and one thing well.

随着时间推移，当我们了解更多的将一件事完成的很好的小模块时，我们就知道我们可以通过模块化机制，用很轻的大型框架搭建应用

For example, many of us learned jQuery. It included methods for doing absolutely everything from CSS manipulation to ajax calls. Now, many of us are migrating to libraries like React where often we need to pull in additional packages to perform tasks like ajax or routing.

例如，我们大多数人都学过jQuery。jQuery涵盖了几乎一切方法，可以操作css，可以回调ajax等等。而现在，我们很多人正将重心从jQuery迁移到React中去，React里面 我们需要做的仅仅是拉入额外的包来执行任务，比如ajax或者routing.

This article will take a look at using npm and ES6 Modules. There are other registries (e.g. Bower) and other module loaders (e.g. CommonJS and AMD), but there are plenty of articles already on those topics.

这篇文章将对npm和ES6模块的使用做一个简短的介绍。另外，还有其他的类似的产品(e.g. Bower) 和其他模块加载工具 (e.g. CommonJS and AMD),关于这些知识，网上有很多，就不一一赘述了。

Whether you are doing Node or frontend development, I believe that ES6 modules and npm are the way forward. If you look at any of the popular open source projects today, such as React or lodash, you’ll see they have also adopted ES6 modules + npm.

如果你正使用Node或者前端开发,我相信ES6模块是未来发展的方向。如果你关注任何的开源项目，比如React或者lodash，你就会知道他们也已经在采用ES6模块和npm

