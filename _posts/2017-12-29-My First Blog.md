---
layout: post
title: Spring Boot & React
comment: true
tags: [Srping boot, react, webpack]
---

***Many people*** who are programer have been using Java. Particularly, Spring Framework is so popular in the world. With Spring Framework, Javascript has been improved rapidly since NodeJS revealed. Because I have only been used Spring before, I have been through many errors when I learned React. So, from now on, I am going to share my experiences about the ways to interwork both Spring boot and React. I am going to continue this post as I aussume that you already have some background knowledges about [Spring Boot](https://projects.spring.io/spring-boot/#quick-start).

## 1. Spring Boot
There are a lot of ways to set the project of Spring Boot in Intellij on other websites.(you also need to know the ways about configurating the Thymeleaf) 
* Settings of Intellij 
  * JDK: 1.8
  * Gradle Project
  * SpringBoot Version: 1.5.9
  * Core: lombok
  * Web: web, devtool(for livereload)
  * Templete Engine: Thymeleaf

You can add more to the settings. After setting, then you're going to be able to see the project of Intellij like picture below. 

![this project](/assets/img/post/2017-12-29-My_First_Blog/p1.png)

And you should make a file which is html file in order to load the first web page and configure URL controller in Spring boot. (I will talk about diffirences between Async and Sync Spring Server). 
> ***path: src/main/resources/templates/{your html file}***.  
> ***controller(SpringBoot): GetMapping("/") -> return "{your html file name(no extension)}"***.  

### Contents of Html
<script src="https://gist.github.com/ijunc2/0e8f30e3c72905292887fabb42af95a7.js"></script>

After settings, please make sure that your site is operated correctly.

## 2. React
For configurating the project of React, usually, [create-react-app](https://github.com/facebookincubator/create-react-app) is used to set the project. Even though I had tried to use [create-react-app](https://github.com/facebookincubator/create-react-app), I recogized that it was difficult for me to set the project for interworking SpringBoot & React, So I decided to use [npm](https://www.npmjs.com/) directly. We need to focus on how to operate SpringBoot. When we configure the web site using SpringBoot, Html Files are placed in 'src/main/resources/templates' generally. And static files such as 'image, script, css etc...' are located in 'src/main/resources/static' So, if you build the files of react using webpack, you shoud place the build files in static folder, and html files should refer the build files which are built by webpack. You can refer to the source code above that is index.html(line:9)

Now, let's set the project for React.
There are many ways to make a structure for React, I'm going to include or bind the project of react in Spring Boot. Project Structure is below.

- src
  - main (for java)
  - **client (from here, these are what we'll make the project for react.)**
    - **containers (folder for react file)**
    - **index.js (Main file for operating React)**. 
...  

- **package.json (if you initiallize the npm($ npm init), this file appear.)**
- **webpack.config.js (this is the setting file for building using webpack)**

After making these folders and files, Follow below steps.

> $ npm init 

> $ npm install react react-dom

> $ npm install babel webpack webpack-merge 

> $ npm install babel-core babel-loader babel-preset-react babel-preset-es2015 

> $ npm install babel-polyfill babel-plugin-transform-object-rest-spread

It helps you to create the project of React and the enviroment for building React. I'll talk about npm packages we installed later, but as soon as possible. I must concentrate on how to make the project of SpringBoot and React today. Once you finished this stuff, You should add codes in 'packages.js', 'webpack.config.js', '/src/client/index.js'

### package.js
```js
{
  ...
  "scripts": {
    ...
    "build": "webpack -d", // (for build!!)
    ...
  },
  ...
}
```

### webpack.config.js
<script src="https://gist.github.com/ijunc2/06a0dfccc3be2beacd792757a3d1f877.js"></script>

### /src/client/index.js
<script src="https://gist.github.com/ijunc2/ea25428576b55584272b8ef2160aa796.js"></script>

Finally, we have done everything to run a server. we should build the file which is refered in main html before running a server. 

> $ npm run build

Run a server of Spring Boot. 
What do you see? Do you see what you expected?

The key to interwork SpringBoot and React is to build the react files using webpack where html file in SpringBoot refer.

I'm supposed to share my opionions which are classified into three categories in the future.

#### 1. My experiences and specific skill about SpringBoot
#### 2. React
#### 3. My opinion about Back-end

ps. I am still learning computer science and programing, so I should study a lot of things. I want to learn a lot with you guys. If there is anything wrong, please share and discuss with me in manners. 








