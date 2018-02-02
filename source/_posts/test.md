title: react
author: Xiaolan Wu
tags:
  - javascript
  - react
categories:
  - 前端
date: 2018-02-02 15:28:00
---
# 从来没有写过的人来写个 react 程序clear

## 一.为什么?
### 我为什么现在要学 react?
今天老陆跟我建议说,让我学学 react 和 react-native,这样以后能接到更多项目.  

我想想也是,既然我现在是一个**自由职业者**,现在主要就是靠接活而实现在家上班的理想,而在国内的 spa 界, react 和 vue 算是平分秋色,那我不会 react 不就丢掉半壁江山了么.  
### 为什么以前在 vue 和 react 之间我选择在团队里推 Vue
以前一直不学 react, 是因为

1. vue 更容易上手,也有更多中文文档,**对团队来说推广成本更低**
2. react 感觉是在 js 里写 html, 而 vue 是在 template 里写结构,我感觉后者我更喜欢点
3. 好几年前,估摸着三四年前了吧.我当时去一个技术大会,我听到一个人说

	> 未来的一个趋势,有可能就是不用写传统的 css, 而是css 对象化,每一个 css 属性都只是一个对象的属性,比如{backGround: xx}
	
 我觉得好好的 css 那么写不行么,这种是不是有点作?  
 
综合以上几点原因,我就在闪银 C端里推 Vue 了.
## 二.是什么
React 是一个 SPA 方案,主要是 vue 层.当然,你可以通过用它的一些支持的库来实现其它层
## 三.怎么用
1.就像 Vue 有 Vue-cli 这种脚手架工具, React 也有` create-react-app`, 简称 cra,
先把脚手架 down 下来
```
npx create-react-app projectName
cd project-name
yarn start
```
诶, npx, 没装过呀,哈哈,不用着急,从 npm5.x2开始,已经自动带了 npx这个辅助命令了.
所以只要你的 npm 是5.2,你执行 npx, 它不会报错的.
摘录一段某熊的全栈之路里对 npx 的解说
> npx, 允许我们仅仅执行一次脚本,而不需要把它实际安装到本地,同时, npx 还允许我们以不同的 node 版本来运行指定命令,允许我们交互式地开发 node 命令行工具以及便捷的安装来自于 gist 的脚本

然后呢,你会发现浏览器已经自动打开了 localhost:3000
我们看一下官方的 hello-world 是怎么写的

```javascript
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('root')
);
```