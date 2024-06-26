---
title: "VSCode 中最好用的 Git 可视化工具"
date: 2021-04-26T00:00:00.000Z
release: 9
---

前端爱好者周刊 (Github: shfshanyue/weekly)，每周记录关于前端的开源工具、优秀文章、重大库版本发布记录等等，周刊中优秀文章会在公众号**全栈成长之路**逐一推送。每周一发布，订阅平台如下，欢迎订阅。

- 订阅网站: <https://weekly.shanyue.tech>
- 订阅Github: [shfshanyue/weekly](https://github.com/shfshanyue/weekly)
- [点击在微信订阅](https://mp.weixin.qq.com/mp/appmsgalbum?action=getalbum&__biz=MjM5NjU5NjQ0NQ==&scene=1&album_id=1880625492081344514&count=3#wechat_redirect)

## 文章推荐

### 一、 [React Express](https://www.react.express/)

学习 React 的专业小书，重实践，对每一小节，都有在线实时代码可以调试并学习。

## 开源与库

### 一、 [react flow: 使用 React 来构建流程图](https://reactflow.dev/)

![](./assets/react-flow.png)

- [repo: wbkd/react-flow](https://github.com/wbkd/react-flow)
- [npm: react-flow-renderer](https://npm.devtool.tech/react-flow-renderer)

## 开发利器

### 一、 [Gitlen](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)

VSCode 中最好用的 Git 可视化工具

### 二、 [commonmark.js dingus](https://spec.commonmark.org/dingus/)

标准 markdown 语法 commonmark 如何正确的把 Markdown 转化为 HTML

## 代码片段

### 一、 当重复点击按钮时，以下三个 `<Heading />` 是如何渲染的

```js
import React, { memo, useMemo, useState } from "react";

const Heading = memo(({ style, title }) => {
  console.log("Rendered:", title);

  return <h1 style={style}>{title}</h1>;
});

export default function App() {
  const [count, setCount] = useState(0);

  const normalStyle = {
    backgroundColor: "teal",
    color: "white",
  };

  const memoizedStyle = useMemo(() => {
    return {
      backgroundColor: "red",
      color: "white",
    };
  }, []);

  return (
    <>
      <button
        onClick={() => {
          setCount(count + 1);
        }}
      >
        Increment {count}
      </button>
      <Heading style={memoizedStyle} title="Memoized" />
      <Heading style={normalStyle} title="Normal" />
      <Heading title="React.memo Normal" />
    </>
  );
}
```

## 版本发布

### 一、 [Node 16 发布](https://github.com/nodejs/node/releases/tag/v16.0.0)

1. Timers Promise API

`Timers Promise API` 其实在 Node15 就已存在，那时候是一个实验特性，目前已进入了稳定阶段，是一项令人兴奋的特性。

```js
import { setTimeout } from "timers/promises";

await setTimeout(100);
```

而当 `setInterval` 也变为 Promise 形式后，对于每间隔一分钟便执行操作的定时任务而言，具有更大的可读性

```js
import { setInterval } from "timers/promises";

for await (const startTime of setInterval(100, Date.now())) {
  const now = Date.now();
  if (now - startTime > 1000) break;
}
```

2. 底层依赖升级

我们知道，Node 基于 v8、libuv、llhttp 等诸多依赖，这次它对诸多依赖进行了升级。如同我们的业务项目依赖于诸多软件包，每一次依赖的升级也会对性能造成不少提升

```js
> process.versions
{
  node: '16.0.0',
  v8: '9.0.257.17-node.10',
  uv: '1.41.0',
  zlib: '1.2.11',
  brotli: '1.0.9',
  ares: '1.17.1',
  modules: '93',
  nghttp2: '1.42.0',
  napi: '8',
  llhttp: '6.0.0',
  openssl: '1.1.1k+quic',
  cldr: '39.0',
  icu: '69.1',
  tz: '2021a',
  unicode: '13.0',
  ngtcp2: '0.1.0-DEV',
  nghttp3: '0.1.0-DEV'
}
```

3. btoa 与 atob

关于 Base64 的转化，Node 在以前使用了 `Buffer.from`，而现在支持 btoa/atob 与浏览器环境保持了一致。
