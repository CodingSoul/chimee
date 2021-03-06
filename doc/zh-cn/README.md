# chimee

[![Build Status](https://img.shields.io/travis/Chimeejs/chimee/master.svg?style=flat-square)](https://travis-ci.org/Chimeejs/chimee.svg?branch=master)
[![Coverage Status](https://img.shields.io/coveralls/Chimeejs/chimee/master.svg?style=flat-square)](https://coveralls.io/github/Chimeejs/chimee?branch=master)
[![npm](https://img.shields.io/npm/v/chimee.svg?colorB=brightgreen&style=flat-square)](https://www.npmjs.com/package/chimee)
[![dependency Status](https://david-dm.org/Chimeejs/chimee.svg)](https://david-dm.org/Chimeejs/chimee)
[![devDependency Status](https://david-dm.org/Chimeejs/chimee/dev-status.svg)](https://david-dm.org/Chimeejs/chimee?type=dev)

[English](https://github.com/Chimeejs/chimee) | 中文

## 简介

Chimee 由奇舞团研制的 h5 播放器，它支持 mp4、m3u8、flv 等多种格式。通过插件式开发，能满足业务方快速迭代、灰度发布等要求。让开发者能够轻松快捷地完成视频场景的开发。

## 特点

Chimee 首先是一个[视频播放器](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/chimee-api.md)。

1. 它让我们可以播放 mp4、m3u8、flv 等多种格式的视频流。
2. 它帮我们解决大部分的兼容性问题，能够解决包括全屏、自动播放、内联播放等常见视频需求。

其次，Chimee 是一个基于 video 设计的[组件化框架](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/why-chimee-is-a-frame.md)。

1. 它容许我们使用插件分割业务上与视频相关的功能。
2. 对于每个组件来说，它们的编写都相当于直接操作 video 元素，简便快捷。
3. 它会梳理好插件间的层级关系，让我们免于被 `z-index` 困扰。
4. 它提供了如透明插件、穿透插件、内外层插件等多种模式，能够覆盖多种交互情景。
5. 它提供了多种便利的方式让我们进行组件间的沟通。
6. 它允许我们定义高优先级插件，从而让我们轻松完成业务上的广告需求。
7. 它支持异步组件。

## 安装

### npm

```
npm install --save chimee
```

### cdn

> 敬请期待

## 用法

你可以直接使用 chimee。

假设你的页面中有一 `id`  为 `wrapper` 的 `div`。

```html
<body>
  <div id="wrapper">
  </div>
</body>
```

那么你可以直接在其上建立 chimee 实例。

```javascript
import Chimee from 'chimee';
const chimee = new Chimee('#wrapper');
chimee.on('play', () => console.log('play!!'));
chimee.load('http://cdn.toxicjohann.com/lostStar.mp4');
chimee.play(); // play!!
```

有的时候我们可能需要进行一些定制，你可以传入相应参数。

```javascript
import Chimee from 'chimee';
const chimee = new Chimee({
  wrapper: '#wrapper',
  src: 'http://cdn.toxicjohann.com/lostStar.mp4',
  controls: true,
  autoplay: true,
  events: {
    play () {
      console.log('play!!');
    }
  }
});
```

如果需要播放 `flv` 或者 `hls` 格式，请传入解码器，具体参数请查阅[此处](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/chimee-api.md#-preset)。

```javascript
import Chimee from 'chimee';
import flv from 'chimee-kernel-flv';
import hls from 'chimee-kernel-hls';
const chimee = new Chimee({
  wrapper: '#wrapper',
  src: 'http://cdn.toxicjohann.com/lostStar.mp4',
  controls: true,
  autoplay: true,
  preset: {
    flv,
    hls
  }
});
chimee.play();
```

如果你想了解更多，请点击[此处](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/chimee-api.md)。

如果你直接使用 chimee 的话，最好提那家以下样式。

```css
container {
  position: relative;
  display: block;
  width: 100%;
  height: 100%;
}
video {
  width: 100%;
  height: 100%;
  display: block;
  background-color: #000;
}
video:focus,
video:active {
  outline: none;
}
```

在没有配置任何皮肤插件的时候，chimee 会使用浏览器原生的皮肤。你可以尝试使用我们的皮肤插件。

```javascript
import ui from 'chimee-plugin-ui';
import Chimee from 'chimee';
Chimee.install(ui);
const chimee = new Chimee({
  wrapper: '#wrapper',
  src: 'http://cdn.toxicjohann.com/lostStar.mp4',
  plugin: [ui.name],
  controls: false,
  autoplay: true
});
```

如果你想了解更多关于 chimee 插件的知识，请点击[此处](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/plugin-api.md)。

可能你并不是太关心 chimee 是怎么运行的，你只是需要一个封装好的播放器。那么你可以直接下载 chimee-player。里面已经有基础 ui 和需要用的插件。

```javascript
import ChimeePlayer from 'chimee-player';

const chimee = new ChimeePlayer({
  wrapper: '#wrapper',
  src: 'http://cdn.toxicjohann.com/lostStar.mp4',
  controls: false,
  autoplay: true
});
```

## 文档

1. [Chimee API 介绍](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/chimee-api.md)
2. [为什么要将 Chimee 设计成一个组件化框架？](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/why-chimee-is-a-frame.md)
3. [Chimee 插件 API 介绍](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/plugin-api.md)
4. [如何编写一个插件?](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/how-to-write-a-plugin.md)
5. [如何编写一个广告插件](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/how-to-write-an-ad-plugin.md)
6. [如何编写一个UI插件](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/how-to-write-a-ui-plugin.md)
7. [如何编写一个弹窗插件](https://github.com/Chimeejs/chimee/blob/master/doc/zh-cn/how-to-write-a-popup-plugin.md)

## 不同的构建版本

你会发现我们有四种构建的版本。

| 名称               | 种类       | 用处                                   | 是否需要定义环境             |
| ---------------- | -------- | ------------------------------------ | -------------------- |
| index.js         | commonjs | Common js, 常用于 Webpack 1.            | 是                    |
| index.mjs        | esmodule | in es module, 常用于 webpack 2 和 rollup | 是                    |
| index.browser.js | umd      | 常直接用于浏览器                             | 否，构建为 development 环境 |
| index.min.js     | umd      | 常直接用于浏览器                             | 否，构建为 production 环境  |

## Development vs. Production

开发环境/生产环境模式是硬编码的 UMD 构建：开发环境下不压缩代码，生产环境下压缩代码。

CommonJS 和 ES Module 构建是用于打包工具的，因此我们不提供压缩后的版本。你有必要在打最终包的时候压缩它们。

CommonJS 和 ES Module 构建同时保留里原始的 `process.env.NODE_ENV` 检测，以决定它们应该运行在什么模式下。你应该使用适当的打包工具配置来替换它们的环境变量以便控制 Vue 所运行的模式。把 `process.env.NODE_ENV` 替换为字符串字面量同样可以让 UglifyJS 之类的压缩工具完全丢掉仅供开发环境的代码段，减少最终的文件尺寸。

#### Webpack

使用 Webpack 的 [DefinePlugin](https://webpack.js.org/plugins/define-plugin/):

```
var webpack = require('webpack')

module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      'process.env': {
        NODE_ENV: JSON.stringify('production')
      }
    })
  ]
}
```

#### Rollup

使用 [rollup-plugin-replace](https://github.com/rollup/rollup-plugin-replace):

```
const replace = require('rollup-plugin-replace')

rollup({
  // ...
  plugins: [
    replace({
      'process.env.NODE_ENV': JSON.stringify('production')
    })
  ]
}).then(...)
```

#### Browserify

## 贡献

克隆本项目

```
npm install
npm start
```

然后打开如下网页 [http://127.0.0.1:10001/demo/base/index.html](http://127.0.0.1:10001/demo/base/index.html)

你可以选择其他你想要的 demo

## 更新日志

请点击[更新日志](https://github.com/Chimeejs/chimee/releases)。

## 证书

[MIT](https://opensource.org/licenses/MIT)