# Next.Js框架

## 🎯什么是Next.Js

这是一个用于 生产环境的 React 框架.

Next.Js为您提供生产环境所需的所有功能以及最佳的开发体验：包括静态及服务器端融合渲染、 支持 TypeScript、智能化打包、 路由预取等功能 无需任何配置. 

Next.Js主要用于React程序的**SSR**(服务端渲染) ,**SSR**简单理解是将组件或页面通过服务器生成html字符串.  再发送到浏览器.  最后将静态标记"混合"为客户端上完全交互的应用程序.

**CSR**(客户端渲染)首次加载的时候需要把所有相关的静态资源加载完毕.  然后核心JS才会开始执行.  这个过程会消耗一定的时间.  接着还会请求网络接口.  最终才能完全渲染完成.

**SSR**后端拦截到路由.  找到对应组件.  开始渲染组件.  所有的 JS 资源在服务器本地. 排除了JS资源的网络加载时间.  接着只需要对当前路由的组件进行渲染. 至于页面的服务请求.  如果在同一台服务器上.  速度也会快很多. 最后后端把渲染好的页面反回给前端.  前端构建DOM的效率大大提高. 

相比之下.  **SSR**能更快地展示出页面的内容.  降低客户端等待时间。**SEO**在爬取页面信息的时候.  会发送**HTTP请求**来获取网页内容.  而服务端渲染首次的数据是后端返回的.  返回的时候已经是渲染完成的 title、内容等信息.  便于爬虫抓取内容。但同时**SSR**也会对服务器的性能有较高的要求。

## 🎌Next.Js快速开始

### ⚙环境要求

- **Node.js 10.13**或更高版本
- MacOS、Windows (包括 WSL) 和 Linux 都被支持

### 🛠创建新的Next.Js应用程序

#### 🚩推荐: 使用`create-next-app`创建

1. 安装 `create-next-app`

    > 安装方法如下:
    >
    > ```shell
    > npm install -g create-next-app
    > ```

2. 使用`create-next-app`

    方法1: 直接使用
    
    
    ```shell
    create-next-app my-app
    ```
    > my-app 就是程序名称
    
    方法2: 使用npx创建
    
    ```shell
    npx create-next-app my-app
    ```
    方法3: 使用yarn创建
    
    ```shell
    yarn create-next-app my-app
    ```
    
    > 另外.  如果你希望使用 TypeScript 开发项目.  可以通过 `--typescript` 参数创建 TypeScript 项目
    > ```shell
    > create-next-app my-app --typescript
    > # or
    > npx create-next-app my-app --typescript
    > yarn create-next-app my-app --typescript
    > ```

#### 💡当然也可以自己创建
> 如果你很熟悉的话

### 🎈创建完成后

第一件事. 就是先运行项目[即.  以开发模式启动 Next.js]
```shell
npm run dev
```

> 如果运行没有任何问题.  则表明Next.Js应用程序搭建完成

## 👀Next.Js项目文件预览

```tree
├─node_modules
├─pages
│  ├─api
│  │  └─index.js
│  ├─_app.js
│  └─index.js
├─public
└─styles
   ├─Home.module.css
   └─globals.css
```

> Next.Js应用程序 和 React 应用程序大致相同.  都是把index.js作为入口函数
>
> 把pages(Next.Js)看作src(React).  就很好理解了吧

## 🤡Next.Js的特性

> 就是自我的总结.  比较片面

- Next.Js的**活**路由

    `pages` 目录的任何( `.js`、`jsx`、`.ts` 或 `.tsx` )文件.  都会被Next.Js使用其文件名作为路由

- Next.Js的动态路由

    例如: 创建文件`pages/post/[pid].js`

    ```javascript
    import { useRouter } from 'next/router'
    
    const Post = () => {
      const router = useRouter()
      const { pid } = router.query
    
      return <p>Post: {pid}</p>
    }
    
    export default Post
    ```
    > 不要被`Post`、`post`这些单词给迷惑了
    
    > 访问: http://localhost:3000/post/1
    > 就会跳转到显示`<p>Post: 1</p>`这样的网页
    
- Next.Js的Api路由

    例如: 创建文件`pages/api/post/index.js`

      ```javascript
    export default (req.  res) => {
        res.statusCode = 200;
        res.setHeader("Content-Type".  "application/json");
        res.end(
            JSON.stringify({
                message: "这里是返回请求信息Api". 
                method: `当前为${req.method}`. 
                data: `请求信息如下: ${JSON.stringify(req.method == "GET"?req.query:req.body)}`. 
            })
        );
    };
      ```
    
    > 访问: http://localhost:3000/api/post?id=12345
    > 就会返回JSON信息
    >
    > ![image-20210721160432909](image-20210721160432909.png)
    
    > 当然.  普通路由有动态路由.  Api路由也同样拥有动态Api路由
    
- Next.Js的动态Api路由

    例如: 创建文件`pages/api/post/[id].js`

      ```javascript
    export default (req.  res) => {
        res.statusCode = 200;
        res.setHeader("Content-Type".  "application/json");
        res.end(
            JSON.stringify({
                message: "这里是返回请求信息Api". 
                method: `当前为${req.method}`. 
                data: `请求信息如下: ${JSON.stringify(req.method == "GET"?req.query:req.body)}`. 
            })
        );
    };
      ```
    
    > 访问: http://localhost:3000/api/post/123
    > 就会返回JSON信息
    >
    > ![image-20210721160809758](image-20210721160809758.png)
    

> 更多详细内容.  请自行观看官方文档

## 关于DEMO

### 描述

大致上的将Next.Js框架和Boostrap、Ant Design、Jquery、Axios进行结合.  没有做什么细节上的优化. 主要使用了Next.Js框架下的路由和Api. 

### 组成

分为5个部分.  介绍页面、Boostrap例子、Ant Design例子、Jquery例子、Axios例子

#### 介绍页面

![image-20210721161151249](image-20210721161151249.png)

> 介绍一些每个例子大大概内容

#### Boostrap例子

![image-20210721161210745](image-20210721161210745.png)

> 描述Api路由的信息

#### Ant Design例子

![image-20210721161227239](image-20210721161227239.png)

> 表单的搜索功能的实现

#### Jquery例子

![image-20210721161236614](image-20210721161236614.png)

> 字面意思

#### Axios例子

![image-20210721161312367](image-20210721161312367.png)

![image-20210721165139616](image-20210721165139616.png)

> 对Api路由的访问

### ❓是如何在Next.Js中使用

#### Bootstrap

> [react-bootstrap官网](https://react-bootstrap.github.io/)
>
> [bootstrap官网](https://v5.bootcss.com/docs/getting-started/introduction/)

| 使用方法                             | 优点                                                         | 缺点                                                         |
| ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 使用`react-bootstrap`                | 1. 简单.  一个`npm i`就下载完毕<br />2. 写起来简单.  就是用组件来写 | 1. 不够好看<br />2. 不自带Bootstrap的CSS样式<br />3. 提供组件不够多.  组件Api不行 |
| ✳直接通过`JavaScript`使用`bootstrap` | 1. 直接 `JavaScript`代码飞起.  会写就很方便.  不会写就不方便 | 1. 不够好看                                                  |

#### Ant Design

> [Ant Design官网](https://ant.design/docs/react/introduce-cn)

| 使用方法   | 优点                                                         | 缺点                              |
| ---------- | ------------------------------------------------------------ | --------------------------------- |
| 使用`antd` | 1. 简单.  一个`npm i`就下载完毕<br />2. 写起来简单.  就是用组件来写<br />3. 自带Ant Design的CSS样式 | 1. 组件Api足够多.  眼睛都要看花眼 |

#### Jquery例子

| 使用方法     | 优点                                                       | 缺点 |
| ------------ | ---------------------------------------------------------- | ---- |
| 使用`jquery` | 1. 简单.  一个`npm i`就下载完毕<br />2. 老牌`JavaScript`库 |      |

#### Axios例子

> [Axios官网](http://www.axios-js.com/zh-cn/docs/)

| 使用方法                         | 优点                                                         | 缺点                |
| -------------------------------- | ------------------------------------------------------------ | ------------------- |
| 使用`react-axios`                | 1. 简单.  一个`npm i`就下载完毕<br />2. 写起来简单.  就是用组件来写 | 1. 使用起来不够灵活 |
| ✳直接通过`JavaScript`使用`axios` | 1. 直接 `JavaScript`代码飞起.  会写就很方便.  不会写就不方便 |                     |

### DEMO的GIF示意图

![动画](动画1.gif)
