
### 大前端学习线路图

#### 1. JS深度剖析
- **1.1 函数**
  * [ ] 函数式编程的本质以及应用场景
  * [ ] 如何以函数式编程风格创建应用程序
  * [ ] 用简单的代码构建复杂的应用程序
  * [ ] 纯函数的定义以及为什么使用纯函数
  * [ ] 为什么消除和控制副作用如此重要
  * [ ] 柯里化、compose、高阶函数的优点
  * [ ] 不可变的数据结构
  * [ ] 常见库（Lodash、Ramda.js）
- **1.2 异步**
  * [ ] JavaScript 的单线程设计
  * [ ] 同步模式和异步模式的调用差异
  * [ ] 回调函数的执行原理
  * [ ] Promise 异步方案的使用进阶与剖析
  * [ ] 处理异步任务的任务队列和事件循环
  * [ ] JavaScript 内部的宏任务与微任务
  * [ ] ES 6 Generator 迭代器的异步应用
  * [ ] 使用Async / Await 语法糖编写扁平的异步代码
  > 面试题：说下事件循环机制
- **1.3 性能优化**
  * [ ] JavaScript 中的垃圾收集
  * [ ] JavaScript 内存管理
  * [ ] V8 垃圾回收机制分类
  * [ ] 引用计数、标记清除、标记整理和增量标记
  * [ ] Performance 工具的使用及注意事项
  * [ ] 20个代码层面的优化细节
- **1.4 ES新特性**
  * [ ] JavaScript vs. ECMAScript
  * [ ] 块级作用域、模板字符串、对象与数组的解构、rest 操作符
  * [ ] 函数进阶（箭头函数、默认参数）
  * [ ] 对象和数组的扩展用法
  * [ ] Proxy、Reflect、Map、Set、Symbol、for...of、
  * [ ] 迭代器模式、生成器函数
  * [ ] ES Modules 模块系统
  * [ ] ES2016 - ES2020（ES7 - ES11）特性一览
  * [ ] 新特性编译工具（Babel）的使用
  * [ ] 新特性的Polyfill：CoreJS 标准库
- **1.5 TS高级编程**
  * [ ] 编程语言的几种不同类型系统
  * [ ] JavaScript 自有类型系统的问题
  * [ ] Flow 静态类型检查方案
  * [ ] Flow 工具的配置及相关插件的使用
  * [ ] TypeScript 基本语法
  * [ ] TypeScript 高级特性（泛型、接口）
  * [ ] TypeScript 内置对象标准库
  * [ ] TypeScript 的类型声明
#### 2. 前端工程化
- **2.1 脚手架工具**
  * [ ] 脚手架设计思想与目标
  * [ ] 脚手架工具的本质作用
  * [ ] 常用的脚手架工具一览
  * [ ] Yeoman 的基本使用以及自定义Generator
  * [ ] Yeoman Sub Generator 特性
  * [ ] 基于Yeoman 创建适合自己的脚手架工具
  * [ ] Plop 生成器的基本使用
  * [ ] 使用Plop提高项目创建同类文件的效率
  * [ ] 脚手架工作原理剖析
  * [ ] 手写一个自己的脚手架工具
- **2.2 自动化构建**
  * 如何使用自动化构建提高开发效率
  * 常用的自动化构建任务执行器
  * npmscripts&script hooks
  * Grunt 工具的使用及扩展开发
  * 相比于Grunt，Gulp 的优势体现
  * Gulp 的使用以及任务结构
  * 基于Gulp 创建自动化构建工作流
  * 封装独立的自动化构建工具
  * FIS3的使用以及常用的扩展插件
- **2.3 自动化部署（CI / CD）**
  * 持续集成与持续部署
  * 基于GitHub / GitLab 的自动化工作流搭建
  * 常见的CI实践：Jenkins、GitLab CI、Travis CI、Circle CI
  * 开源项目的新选择：GitHub Actions
  * 基于常用CI系统实现静态
  * Node 类型的项目自动部署
- **2.4 模块化开发与Webpack**
  * 模块化标准与规范、ES Modules 标准的支持情况
  * Webpack打包工具的基本使用
  * Webpack的配置详解
  * Webpack打包过程和打包结果分析
  * Webpack中资源模块的加载（Loader）
  * 如何开发一个Webpack的Loader
  * Webpack的插件机制、开发一个Webpack插件
  * Webpack周边生态（Dev Server、HMR、Proxy）
  * Webpack高级特性（Tree-shaking、sideEffects)
  * Webpack打包过程及打包结果的优化
  * 深度剖析Webpack实现原理（AST 语法树）
  * 其他常见的打包工具（Rollup、Parcel）
- **2.5 规范化标准**
  * 常见的代码Lint 工具（ESLint、Stylelint）
  * 创建项目或者团队专属的Lint规则/ 风格
  * 通用型代码格式化工具Prettier
  * 结合自动化工具或者Webpack的使用
  * 配合GitHook确保源代码仓库中代码的质量
  * 结合脚手架、自动化、模块化、规范化搭现代化前端工程
#### 3. 核心框架原理与应用
- **3.1 Vue.js 原理深度剖析**
  * [ ] Vue.js框架基础回顾
  * [ ] Vue CLI基础设施深度解剖
  * [ ] 数据响应式实现原理分析Snabbdom库以及Snabbdom源码解读
  * [ ] 虚拟DOM 和Diff算法的实现
  * [ ] 模板编译模块的实现原理
  * [ ] Vue Router源码剖析
  * [ ] 手写Vue Router实现
- **3.2 Vue.js 高级与进阶**
  * [ ] 封装自己的Vue 组件库
  * [ ] Vue项目性能优化
  * [ ] Vuex 数据流管理方案
  * [ ] 使用TypeScript开发Vue.js 应用
  * [ ] 原生服务端渲染（SSR）的实现、同构开发
  * [ ] Nuxt.js 集成式SSR框架
  * [ ] 静态站点生成（SSG）方案及Gridsome
  * [ ] Vue.js3.0 设计和用法的变化以及优势
  * [ ] Vue.js3.0 Composition APIs
  * [ ] Vue.js+Vue Router+Vuex+TypeScript实战项目开发
- **3.3 React 设计原理解密**
  * React框架基础回顾、JSX语法
  * 分析Virtual-DOM目的及实现原理
  * React核心算法：Fiber
  * React框架的设计哲学
  * React框架核心源码解读
- **3.4 React 进阶与实战**
  * 封装React 自定义组件库
  * React 组件的性能优化
  * 受控和非受控组件的选用标准
  * React 组件的自动化测试
  * React 16.8Hooks 特性的使用以及实现原理分析
  * CSS-in-JS 方案以及emotion 库
  * 现代化React 应用UI框架Chakra-UI
  * 使用TypeScript开发React 应用
  * React 数据流方案：Redux、Mobx
  * Redux 常用中间件以及中间件的开发
  * 原生服务端渲染（SSR）的实现、同构开发
  * Next.js 集成式SSR框架
  * 静态站点生成（SSG）方案及Gatsby框架
  * React+React Router+Redux+AntDesign+TypeScript实战
#### 4. nodejs全栈开发
- **4.1 Node.js 高级编程**
  * 非堵塞IO、EventLoop、事件队列
  * CommonJS 原理解析
  * 核心模块、自定义模块、第三方模块
  * 文件系统、Buffer 对象、字符编码
  * 压缩和解压缩、加密和签名算法
  * 网络编程、TCP/IP、HTTP服务
  * cookie 和session 原理
  * 多进程和集群搭建搭建
  * 反向代理服务器
- **4.2 NoSQL 数据库**
  * NoSQL 数据库特性及优势介绍
  * MongoDB 的安装、连接、操作
  * mongoose 模块以及常用的操作API
  * Redis快速上手以及它所适合的场景
  * 使用Node.js 操作Redis
- **4.3 Web 开发框架**
  * Express完成基本的服务端应用开发
  * Express路由、模板引擎、错误处理
  * Express 中间件机制的设计思想
  * Express 中间件使用以及自定义中间件
  * Express 应用程序的进程管理器
  * Express安全与性能的最佳实践
  * Express+Handlebars+Mongoose实战
  * Koa 应用与实践、AOP面向切面编程
  * Koa 中间件实现、源码深度剖析
  * Koa 的中间件模型与Express 的差异
  * PM2宿主部署Node.js 应用
- **4.4 GraphQL API 开发**
  * 基于Koa开发RESTful API
  * 应用层最佳接口实践：GraphQL
  * GraphQL规格标准与设计优势
  * GraphQL快速开发库：Apollo
  * API鉴权标准、jsonwebtoken 模块及其相关API
  * Docker Compose+GitLab CI自动化部署Node.js 应用
- **4.5 企业级框架**
  * Egg.js项目架构与脚手架工具
  * Egg.js 中间件机制、洋葱圈模型
  * Egg.js路由、控制器、服务
  * Egg.js 插件机制以及插件开发
  * Egg.js 定时任务调度
  * Egg.js+Mongoose+Nunjucks+TypeScript项目实战
  * Nest.js框架的基本概念和内部组成
  * 使用Nest.js框架构建高效且可伸缩的服务端应用
  * Nest.js面向切面编程、依赖注入的实践
  * Adonis.js框架介绍

#### 5. 泛客户端开发
- **5.1 小程序与快应用**
  * 微信小程序MINA框架原生开发回顾
  * 其他小程序平台及其相关介绍
  * 京东Taro多端统一开发方案
  * uni-app多端统一开发方案
  * 基于uni-app 的多端电商小程序项目开发
  * 小程序打包快应用和H5
- **5.2 Hybrid App 开发**
  * 基于WebViewUI的基础方案
  * Cordova /Ionic通用型混合App开发框架
  * Cordova 的实现原理分析以及它的常用插件
  * H5配合原生WebView开发混合式App
  * 通过JSBridge完成H5与Native 的双向通讯
  * 原生App开发相关知识
- **5.3 React Native**
  * ReactNative开发环境搭建
  * 初始环节搭建以及相关基础配置
  * 热更新的开发体验
  * 使用Flexbox实现界面布局
  * 常见界面布局和长列表呈现
  * 接入第三方Native 组件（Objective-C / Swift / Java）
  * ReactNative架构的实现原理
- **5.4 Flutter 原生App 开发**
  * Flutter概述以及Windows / macOS 环境搭建
  * Dart 语言快速上手、包管理工具
  * Flutter快速上手、开发体验、路由和导航
  * UI开发：内置MaterialDesign 和Cupertino（iOS风格）Widget
  * 常用Widget、表单组件、布局方式
  * 数据响应：界面状态管理
  * 网络编程以及相关第三方包
  * Native功能和SDK的调用
  * Flutter在线课堂项目实战案例
- **5.5 Electron 桌面应用开发**
  * Electron运行时的基本结构分析
  * 快速上手、常用API、基础案例
  * 主进程与渲染进程之间的差异以及相互通信
  * 常见桌面应用程序功能的实现
  * Electron 结合React / Vue.js之类的前端框架
  * Electron 应用的调试（主进程与渲染进程）以及相关工具（Spectron /Devtron）
  * 集成式打包工具（electron-builder / electron-packager / electron-forge）
  * 实战案例：模仿Microsoft ToDoPart

#### 6. 商业级技术解决方案
- **6.1 Serverless 无服务端方案**
  * BaaS / FaaS / PaaS服务
  * Serverless架构与实现原理
  * Serverless 应用场景与局限性
  * 国外常见的Serverless服务（ZEITNow、Netlify）
  * 国内常见的Serverless服务（阿里云、腾讯云）
- **6.2 中途岛/ 中间层方案**
  * BFF架构的优势及常见方式
  * 基于Node.js 的中间层架构
  * 实现更合理的前后端分离架构
  * 中间层的目标与职责
  * 后端细粒度接口聚合
  * 服务端模板渲染
  * 前端路由设计
- **6.3 首屏性能提升方案**
  * 白屏加载和首屏加载时间的区别
  * 骨架屏：渲染一些简单元素进行占位
  * 使用PWA开发可离线化应用
  * 客户端缓存策略
  * 利用script 的async 和defer 异步加载
  * 前端资源的分块/按需加载
- **6.4 数据埋点方案**
  * 数据埋点的原理分析
  * 页面访问量统计
  * 功能点击量统计
  * 埋点系统的实现
- **6.5 长列表无限滚动方案**
  * 触底加载更多功能的实现
  * 长列表渲染卡顿问题的原因
  * 高性能长列表渲染的思路：虚拟列表
  * 不同框架下长列表无限滚动的实现方法
  * 高性能滚动及页面渲染优化
- **6.6 API 接口鉴权方案**
  * JSONWeb Token 方案介绍
  * jsonwebtoken 模块及其相关API
  * JWT 创建与签发、解码与验证
  * Node.js鉴权中间件的实现
  * Axios 统一鉴权模块
  * React / Vue.js框架下客户端路由鉴权
- **6.7 更多常见方案**
  * 渐进式加载方案
  * RBAC权限管理解决方案
  * 接口Mock方案
  * OSS云存储方案
  * H5直播方案
  * 多语言化方案
  * 防盗链方案
  * CDN加速方案
#### 7. 高阶技术专题
- **7.1 微前端架构与实践**
  * 微前端诞生的背景和解决的问题
  * 微前端下的工程化实践
  * 如何同时支持React / Vue.js / Angular等不同的框架
  * 开发一个简单的微前端框架
- **7.2 PWA 渐进式Web 应用**
  * PWA 使用场景分析
  * 服务端/客户端离线缓存技术
  * 浏览器多线程环境
  * 通过Service workers让PWA离线工作
  * ServiceWorkers 的生命周期
  * 基于PWA 的消息推送、应用更新
  * 渐进式加载
- **7.3 数据可视化**
  * 相关知识储备：Canvas、SVG
  * 数据可视化的目标
  * 实现数据可视化的常用方式
  * 相关库：D3.js、AntV、ECharts.js
- **7.4 现代化Web 101 架构剖析**
  * Web 应用主流架构概览
  * 域名、DNS、负载均衡等相关概念的普及
  * Web 应用服务端、数据库服务器
  * 缓存服务、任务队列服务
  * 云存储、CDN
- **7.5 Web Components**
  * Custom Elements
  * ShadowDOM
  * HTML Templates
  * Web Components 案例
  * Vue 组件转换成原生组件
- **7.6 更多技术专题**
  * CSS预/后处理器（Sass、PostCSS）
  * CSS架构（BEM、CSS-in-JS、emotion、styled-components）
  * 移动端真机调试
  * Web安全专题（HTTPS、XSS / CSRF、CSP）
  * 前端应用性能专题
  * Web Assembly
  