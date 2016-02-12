#### the original http://wesbos.com/javascript-modules/
#An Intro To Using npm and ES6 Modules for Front End Development
#### http://haoduoshipin.com/v/179

    将npm 和ES6模块机制用在前端开发中的一些相关信息

A big thanks to bitHound for sponsoring my time to research and write this article. Ch  eck out their service, which provides continuous analysis and quality checks for both your front and back end JavaScript and its dependencies.

    很感谢bitHound赞助我研究和撰写这篇文章。研究他们的提供的服务，他们的服务提供了持续的分析和质量的
    检查，在前端和后端的js和其相应的依赖。

The JavaScript landscape is changing quickly and along with it the way that we work with dependencies in our websites and applications.

    伴随着JavaScript世界日新月异的变化，我和我们的网站以及应用中的各种依赖文件打交道的方式也在发生着变化

This post is for developers who are currently loading in their JavaScript via multiple script tags and finding that dependency management is becoming a little cumbersome as their webpages or applications start to grow.

    这篇博文，适合于那些仍然用多个script标签加载js，发现随着他们的网页数量和应用规模扩大，依赖管理将变得
    越来越麻烦

For a deep dive into everything the spec has to offer, as well as some great comparisons to CommonJS and AMD, check out Axel Rauschmayer’s Exploring ES6 book, particularly chapter 17.

    如果想要深入了解ES6模块规范内容，以及它和Commonjs和AMD的差别，请查看Axel Rauschmayer’s Exploring ES
    6 book，尤其适合第17章

  #What are JavaScript Modules?
  
  什么是JS模块
```js modules allow us to chunk our code into separate files inside our project or to use open source modules that we can install via npm. Writing your code in modules helps with organization, maintenance, testing, and most importantly, dependency management.

    js模块让我们可以把项目代码拆分成一个一个孤立的文件，或者通过Npm安装开源的模块来使用。将你的代码模块化组织
    可以利于组织，维护，测试，更重要的是依赖的管理。

When we write JavaScript, it’s ideal if we can make modules that do one thing and one thing well. This separation allows us to pull in various modules only when we need them. Modules represent the core principle behind npm — when we need specific functionality, we can install the modules we need and load them into our application.

    在我们使用js时，让模块做一件事，并且做好，这是不错的想法。仅当我们需要模块的时候，我们可
    以给独立的文件拉入模块。模块代表着Npm工具背后的核心理念。有时候我们需要一些很特别的功能，我
    们可以安装我们需要的模块，并将模块加载入我们的应用中

As time goes on, we’re seeing fewer large frameworks that do everything under the sun while seeing more small modules that do one thing and one thing well.

    随着时间推移，当我们了解更多的将一件事完成的很好的小模块时，我们就知道我们可以通过模块化机
    制，用很轻的而很完善的大型框架搭建应用

For example, many of us learned jQuery. It included methods for doing absolutely everything from CSS manipulation to ajax calls. Now, many of us are migrating to libraries like React where often we need to pull in additional packages to perform tasks like ajax or routing.

    例如，我们大多数人都学过jQuery。jQuery涵盖了几乎一切方法，可以操作css，可以回调ajax等等。而现在，
    我们很多人正将重心从jQuery迁移到React中去，React里面 我们需要做的仅仅是下载其他的安装包来执行任
    务，比如ajax或者routing.

This article will take a look at using npm and ES6 Modules. There are other registries (e.g. Bower) and other module loaders (e.g. CommonJS and AMD), but there are plenty of articles already on those topics.

    这篇文章将对npm和ES6模块的使用做一个简短的介绍。另外，还有其他的类似的产品(e.g. Bower) 和其他模
    块加载工具 (e.g. CommonJS and AMD),关于这些知识，网上有很多，就不一一赘述了。

Whether you are doing Node or frontend development, I believe that ES6 modules and npm are the way forward. If you look at any of the populr open source projectas today, such as React or lodash, you’ll see they have also adopted ES6 modules + npm.

    如果你正使用Node或者前端开发,我相信ES6模块是未来发展的方向。如果你关注任何的开源项目，比如React或者
    lodash，你就会知道他们也已经在采用ES6模块和npm

###Current workflow
当前工作流

Many workflows for JavaScript look like this:
    许多Js工作流看起来像这样
- Find a plugin or library that you want and download it from GitHub
    找到一个你想要的插件或者库，然后从github上下载即可
- Load it into your website via a script tag
    接着通过script标签加载到你的网站上
- Access it via a global variable or as a jQuery plugin
This type of workflow has worked fairly well for years, but not without its issues:

    借助一个全局变量或者作为一个插件访问它
    这些年来，工作流运作的挺棒的，然而并不是没有问题：


Updates to the plugins have to be done manually — it’s hard to know when there are critical bug fixes or new functionality available.
Messy source control history — all dependencies need to be checked into source control and unpleasantness can result when libraries are updated.
    插件需要手动升级——导致很难知道有严重的bug修复或者可用的新功能
混乱的版本控制历史——所有的依赖文件都需要加入源码控制中去，然而当库文件更新的时候，一切变得混乱不堪

***Little to no dependency management*** — many scripts duplicate functionality but could easily ***share that functionality*** via a small module.
Pollution and possible collisions within the global name space.

    几乎无以来管理——许多脚本功能重复，但是如果采用一个js模块，就很容易实现功能共享
    全局命名空间中的命名污染和冲突

The idea of writing JavaScript modules isn’t new, but with the arrival of ES6 and the industry settling on npm as the preferred package manager for JavaScript, we’re starting to see many devs migrate away from the above workflow and standardizing on using ES6 and npm.

    撰写js模块并非新想法了，但是随着es6的到来和作为js最受欢迎的包管理系统npm的成熟，我们开始
    看到许多开发者已经慢慢从上述的工作流迁移到了es6和Npm并将其标准化

Hold on. npm? Isn’t that for Node?
Many moons ago, npm began as the package manager for Node.js, but it has since evolved to become the package manager for JavaScript and front end dev in general. Nowadays, we can cut the whole song and dance for installing libraries down to 2 steps:

    等一下，Npm？那不是Node专用的吗?
    很久之前，Npm刚开始确实是作为node的包安装管理器，但是后来呢，它慢慢成为了js和前端开发
    者常用的包安装管理系统。时至今日，我们可以将安装软件包的过程缩减为两步

Install our dependency from npm, e.g.: npm install lodash --save
Import it into the file where we need that dependency, e.g.:
```js
import _ from 'lodash';
```
There’s a lot more that goes into setting this workflow up, as well as plenty to learn about importing and exporting from modules, so let’s dive into that.
我们利用npm安装依赖文件，例如：***npm install lodash --save***
    导入依赖到需要的文件中
```js
import _ from 'lodash';
```   

    关于工作流还有很多东西需要我们研究，并且有大量的关于导入和导出模块的知识需要学习，所以就
    让我们一起来探究一下吧。


The idea behind Modules
Instead of just loading everything into the global namespace, we use import and export statements to share things (variables, functions, data, anything…) between files. Each module will import the dependencies that it needs and export anything that should be made import-able by other files.
模块背后的理念   
代替加载所有文件到全局变量中，我们使用import和export语句来在文件之中共享资源（变量，函数，数据，任何事）。每个模块将导入自己需要的依赖并导出其他文件需要的资源
```
Getting everything working in current browsers requires a bundle step. We’ll talk about that later in this article, but for now let’s focus on the core ideas behind JavaScript Modules.
让所有代码能在当前浏览器中顺利运行需要一个大包步骤。我们将在篇章末尾谈论其相关的知识，现在让我们关注一下js模块背后的核心理念吧。



Creating your own Modules
Let’s say we are building an online store app and we need a file to hold all of our helper functions. We can create a module called helpers.js that contains a number of handy helper functions — formatPrice(price), addTax(price) and discountPrice(price, percentage), as well as some variables about the online store itself.
创建你自己的模块
比方说，我们将建立一个线上商店应用，我们需要一个文件保存所有的helper函数。我们可以创建一个叫做helpers.js的包，其中包含了若干个helper函数formatPrice(price), addTax(price) and discountPrice(price, percentage)，以及一些跟应用本身的变量
Our helpers.js file would look like this:
```js
const taxRate = 0.13;

const couponCodes = ['BLACKFRIDAY', 'FREESHIP', 'HOHOHO'];

function formatPrice(price) {
    // .. do some formatting
    return formattedPrice;
}

function addTax(price) {
    return price * (1 + taxRate);
}

function discountPrice(price, percentage) {
    return price * (1 - percentage);
}
Now, each file can have its own local functions and variables, and unless they are explicitly exported, they won’t ever bleed into the scope of any other files. In the above example, we might not need taxRate to be available to other modules, but it’s a variable we need internally within this module.

现在，每个文件都有他自己的本地变量和函数，并且除非你明确地导出，不然他们将不会渗入其他文件的作用域中。在上面的例子中，我们可能不需要对其他模块可用的taxRate函数,但是我们需要在这个模块内部使用的一个变量。

How do we make the functions and variables above available to other modules? We need to export them. There are two kinds of exports in ES6 – named exports and a single default export. Since we need to make multiple functions and the couponCodes variable available, we will used named exports. More on this in a second.

我们怎么样创建一些让其他模块可用的函数和变量呢？我们需要导出这些函数和变量。在ES6有两种办法导出他们，命名导出和单一默认 导出。因为我们需要创建不同的函数和couponCodes变量，我们将使用被命名的exports.更多信息马上取来


The simplest and most straightforward way to export something from a module is to simply stick the export keyword in front, like so:
从模块中导出数据，最简单有直接的方法是将export关键词添加到前面，比如这样：
```js
const taxRate = 0.13;

export const couponCodes = ['BLACKFRIDAY', 'FREESHIP', 'HOHOHO'];
export function formatPrice(price) {
    // .. do some formatting
    return formattedPrice;
}
```
//  ... 
We can also export them after the fact:
```js
export couponCodes;
export formatPrice;
export addTax;
export discountPrice;
Or all at once:
```js
export { couponCodes, formatPrice, addTax, discountPrice };
There are a handful of other ways use export, make sure to check the MDN Docs if you run into a situation where these aren’t working for you.
   还有其他几个导出方法，当你使用导出方式出现问题的时候，请查看mdn文档     
Default export
As mentioned before, there are two ways that you can export from a module — named or default. Above were examples of named exports. In order to import these exports into another module, we must know the names of the variables/functions we wish to import — examples of this coming in a second. The benefit of using named exports is that you can export multiple items from a single module.
默认导出
正如前面所提到，这里有两个你可以从一个被命名的或者默认的模块导出的方法。上面提到的都是命名的导出。为了导入另一个模块的导出，我们必须知道我们要导出的变量或者函数的名字 - 接下来我们讨论相关问题。使用命名导出的好处是，你可以从一个单一的模块导出不同的项目。

The other type of export is the default export. Use named exports when your module needs to export multiple variables/functions, and use a default export when your module only needs to export one variable/function. While you can use both default exports and named exports within a single module, I’d advise you to pick only one style per module.

另一个导出方法是默认导出。如果你需要导出多重变量/
函数，可以使用命名导出，如果你的模块仅仅需要导出一个变量/函数，可以使用默认导出。
虽然你可以在一个单一模块使用两种导出方法，我还是建议你遵循单一原则。
Examples of default exports may be a single StorePicker React Component or an array of data. For example, if we have the following array of data that we need to make available to other components, we can use export default to export it.
 默认导出的例子可能是一个名为StorePicker的React组件或者一个数组。例如，如果我们需要把下面的一个数组导出给其他组件，我们采用默认导出方式。

```js
// people.js
const fullNames = ['Drew Minns', 'Heather Payne', 'Kristen Spencer', 'Wes Bos', 'Ryan Christiani'];

const firstNames = fullNames.map(name => name.split(' ').shift());
```
export default firstNames; // ["Drew", "Heather", "Kristen", "Wes", "Ryan"]
Just like above, you can append the export default in front of a function you wish to export as well:
```js
export default function yell(name) { return `HEY ${name.toUpperCase()}!!` }
```
Importing your own modules
Now that we have separated our code into little modules and exported pieces that we need, we can go ahead an import parts or all of those modules into other parts of our application.

To import modules that are part of our codebase, we use an import statement and then point to a file’s location relative to the current module — just like you are used to in any HTML src path or CSS background image. You’ll notice that we leave off the .js extension as it’s not required.

It’s important to note that we don’t import modules once and have them available to the entire application as globals. Whenever one of your modules has a dependency on another module — say our above code needed a lodash method — we must import it into that module. If we require the same lodash function in 5 of our modules, then we import it 5 times. This helps keep a sane scope as well as makes our modules very portable and reusable.

Importing named exports
The first thing we exported was our helpers module. Remember we used named exports here, so we can import them in a number of ways:
```js
// import everything as methods or properties of an object
import * as h from './helpers';
// and then use them
const displayTotal = h.formatPrice(5000);
```
```
// Or import everything into the module scope:
import * from './helpers';
const displayTotal = addTax(1000);
// I'd recommend against this style because it's less explicit
// and could lead to code that's harder to maintain
```

// or cherry pick only the things you need:
import { couponCodes, discountPrice } from './helpers';
const discount = discountPrice(500, 0.33);
Importing default exports
If you recall, we also exported an array of first names from people.js, since this was the only thing that needed to be exported from that module.

Default exports can be imported as any name — it’s not necessary to know the name of the variable, function, or class that was exported.
```js
import firstNames from './people';
// or
import names from './people';
// or
import elephants from './people';
// these will all import the array of first names
```
// you can also get the default export like so:
import * as stuff from './people'
const theNames = stuff.default
Importing modules from npm
Many of the modules we will use come from npm. Whether we need a full library like jQuery, a few utility functions from lodash, or something to perform Ajax requests like the superagent library, we can use npm to install them.

npm install jquery --save
npm install lodash --save
npm install superagent --save
// or all in one go:
npm i jquery lodash superagent -S
Once these packages are in our node_modules/ directory, we can import them into our code. By default, Babel transpiles ES6 import statements to CommonJS. Therefore, by using a bundler that understands this module syntax (like webpack or browserify) you can leverage the node_modules/ directory. So our import statements only need to include the name of the Node module. Other bundlers may require a plugin or configuration to pull from your node_modules/ folder.
```js
// import entire library or plugin
import $ from 'jquery'; 
// and then go ahead and use them as we wish:
$('.cta').on('click',function() {
    alert('Ya clicked it!');
});
```
The above code works because jQuery is exported as a CommonJS module, and Babel transpiles our ES6 import statement to work with jQuery’s CommonJS export.

Let’s try it again with superagent. As jQuery, superagent exports the entire library as a default export using CommonJS, so we can import it with whatever variable name we like — it’s common to call it request.
```js
// import the module into ours
import request from 'superagent';
// then use it!
request
    .get('https://api.github.com/users/wesbos')
    .end(function(err, res){
        console.log(res.body);
    });
```
Importing Pieces or Cherry Picking
One of my favorite things about ES6 modules is that many libraries allow you to cherry-pick just the pieces you want. lodash is a fantastic utility library filled with dozens of helpful JavaScript methods.

We can load the entire library into the _ variable since lodash exports the entire library as a the main module export (again, Babel transpiles our import to treat it as if lodash is using export default):
```js
// import the entire library in the _ variable
import _ from 'lodash';
const dogs = [
  { 'name': 'snickers', 'age': 2, breed : 'King Charles'},
  { 'name': 'prudence', 'age': 5, breed : 'Poodle'}
];
```
_.findWhere(dogs, { 'breed': 'King Charles' }); // snickers object
However, often you will want just one or two lodash methods instead of the entire library. Since lodash has exported every single one of its methods as a module itself, we can cherry-pick just the parts we want! This is made possible again because of how Babel transpiles your import statement.
```js
import { throttle } from 'lodash';
$('.click-me').on('click', throttle(function() {
  console.count('ouch!');
}, 1000));
```
Making sure modules are up-to-date
Some resistance to the whole “small modules” way of coding is that it’s easy to end up with a dozen or more dependencies from npm that all interact with each other.

The JavaScript ecosystem is moving very quickly right now, and keeping your dependencies up to date can be a headache. Knowing when both your own code and your dependencies have bugs, security flaws, or just general code smells isn’t as easy as it used to be. We need to know if anything in our project is insecure, deprecated, outdated, or unused.

To solve this, bitHound offers a fantastic service that will constantly monitor your code and let you know when there is anything wrong with your dependencies, as well as provide an overall score of how well your repo is doing. Find out how yours stacks up, it’s free for all your open source projects.

bitHound integrates with GitHub and BitBucket and has also rolled out automatic commit analysis which will notify bitHound of changes to your repository’s branches. When your dependencies are out of date, you’ll be pinged in Slack or HipChat or get an email detailing everything.



bitHound also has branch status on Pull Requests – set up pass/fail criteria and bitHound will post the status right to GitHub or Bitbucket.

Another tool that works well with bitHound is called npm-check-updates. Install globally on your development machine with npm install npm-check-updates -g and then run ncu. To quickly check if your packages have any available updates. If they do, you can run ncu --upgradeAll to automatically update all packages in your package.json. Make sure to run a npm install after doing this to fetch the latest code from NPM.

The Bundle Process
Because the browser doesn’t understand ES6 modules just yet, we need tools to make them work today. A JavaScript bundler takes in our Modules and compiles them into a single JavaScript file or multiple bundles for different parts of your application.

Eventually we won’t need to run a bundler on our code and HTTP/2 will request all import statements in one payload.

There are a few popular bundlers, most of which use Babel as a dependency to transpile your ES6 modules to CommmonJS.

Browserify was initially created to allow node-style commmonjs requires in the browser. It also allows for ES6 modules.
webpack is popular in the React community. It also handles many module formats, not just ES6.
Rollup is built for ES6, but seems to have trouble with sourcemaps — I’d check on this one in a few months.
JSPM sits on top of npm and SystemJS.
Ember CLI is an easy-breezy command line tool similar to webpack for users of Ember. It uses Broccoli under the hood.
Which one should you use? Whichever works best for you. I’m a big fan of Browserify for the ease of getting started and webpack for many of its React integrations. The beauty of writing ES6 modules is that you aren’t writing Browserify or webpack modules — you can switch your bundler at any time. There are a lot of opinions out there on what to use, so do a quick search and you’ll find plenty of arguments for each tool.

If you are already running tasks via gulp, Grunt, or npm tasks for your existing JavaScript and CSS, integrating Modules into your workflow is fairly simple.

There are many different ways to implement a bundler — you can run it as part of your gulp task, via your webpack config, as an npm script, or straight from the command line.

I’ve created a repo detailing how to use webpack and Browserify along with some sample modules for you to play with.

Importing code that isn’t a module
If you are working on moving your codebase over to modules but aren’t able to do it all in one shot, you can simply just import "filename" and it will load and run the code from that file. This isn’t exactly ES6, but it’s a feature of your bundler.

This concept is no different than running concatenation on multiple .js files except that the code you import will be scoped to the importing module.

Code that requires a global variable
Some libraries, such as jQuery plugins, don’t fit well into the JavaScript Modules system. The entire jQuery plugin ecosystem assumes that there is a global variable called window.jQuery that each plugin can tack itself onto. However, we just learned that there are no globals with ES6 modules. Everything is scoped to the module itself unless you explicitly set something on the window.

To solve this, first ask yourself if you really need that plugin or if it’s something you could code on your own. Much of the JavaScript plugin ecosystem is being rewritten to exclude the jQuery dependency and to be made available as standalone JavaScript Modules.

If not, you will need to look to your build process to help solve this problem. Browserify has Browserify Shim and webpack has some documentation on it.

Gotchas
When exporting a function, do not include a semicolon at the end of the function. Most bundlers will still allow the extra semicolon, but it’s a good practice to keep it off your function declarations so you don’t have an unexpected behavior when switching bundlers.
```js
// Wrong:
export function yell(name) { return `HEY ${name}`; };
// Right:
export function yell(name) { return `HEY ${name}`; }
Further Reading
Hopefully this was a nice introduction to using npm and ES6 Modules. There is a lot more to learn and in my opinion the best way to learn is to start using them in your next project. Here are some fantastic resources to help you along the way:

Exploring ES6 book
Brief Overview of ES6 Module syntax
ES6 Features
ES6 Modules on Rollup’s Wiki
Browserify vs webpack hot drama
webpack & ES6
ES6 features & webpack workshop (complete with repo and video recordings: ES6 features Migrating with Webpack)
Thanks + Updates
A huge thanks to Stephen Margheim, Kent C. Dodds, Mike Chen, Ben Berman, and Juan Pablo Osorio Ospina for reviewing and providing excellent feedback on this article.

If you have any suggestions, code samples, technical updates or clarifications you would like to add to this, please send on over a pull request.