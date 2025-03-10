# v-watermark-plugin

​	`v-watermark-plugin` 是一款实用的网页水印添加工具，配置选项丰富灵活，用户可按需自定义水印样式和布局。插件提供 `createWaterMark` 和 `removeWatermark` 两个核心函数，分别用于添加和移除水印。

​	它支持 UMD、ESM、IIFE、CJS 四种模块格式，能适配不同开发环境。同时，支持通过 CDN 链接直接引入，方便用户根据具体需求灵活使用。

## 安装插件

​	你可以通过以下常见的包管理工具来安装 `v-watermark-plugin`：

```bash
# npm
npm install v-watermark-plugin

# pnpm
pnpm install v-watermark-plugin

# yarn
yarn add v-watermark-plugin
```

## 使用示例

### 添加单行水印

```typescript
import { createWaterMark } from 'v-watermark-plugin';

const options = {
  text: ['Vivien 20250221'], // 注意！参数是一个数组
};

// 调用 createWaterMark 函数添加水印
createWaterMark(options);
```

效果：

<img src="./images/image-20250221101901444.png" alt="image-20250221101901444"/>

### 添加多行水印

```typescript
import { createWaterMark } from 'v-watermark-plugin';

const options = {
  text: ['good good study ', 'day day up'], // 注意！参数是一个数组
};

// 调用 createWaterMark 函数添加水印
createWaterMark(options);
```

效果：

<img src="./images/image-20250221102008589.png" alt="image-20250221102008589"/>

### 移除水印

```typescript
import { removeWatermark } from 'v-watermark-plugin';

// 调用 removeWatermark 函数移除水印
removeWatermark();
```

## 使用 CDN 链接

​	可以通过 CDN 链接直接将 `v-watermark-plugin` 引入到项目中。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>使用 CDN 链接添加水印</title>
  <!-- 引入 v-watermark-plugin 的 CDN 链接，这里@latest假设最新版本，实际按需调整
	特别注意：决定引入 UMD、ESM、IIFE、CJS 中的哪种格式文件，需要综合考量你项目环境。
	-->
  <script src="https://cdn.jsdelivr.net/npm/v-watermark-plugin@latest/dist/v-watermark-plugin.[umd/esm/iife/cjs].js"></script>
</head>

<body>
  <h1>这是一个测试页面</h1>
  <script>
    const options = {
      text: ['vivien'],
      fontSize: '16px',
      rotate: -25
    };
    // 调用 createWaterMark 函数添加水印
    window.vWatermarkPlugin.createWaterMark(options);
  </script>
</body>

</html>
```

## 直接引入文件

### 使用 IIFE 格式 [v-watermark-plugin.iife.js](./dist/v-watermark-plugin.iife.js)

​	在传统的 HTML 页面里，可通过 `<script>` 标签直接引入 JS 文件。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>使用 JS 文件添加水印</title>
</head>
<body>
    <h1>这是示例页面</h1>
    <script src="path/to/your/v-watermark-plugin.iife.js"></script>
    <script>
        const options = {
            text: ["vivien"],
        };
        createWaterMark(options); 
    </script>
</body>
</html>
```

### 使用 UMD 格式 [v-watermark-plugin.umd.js](./dist/v-watermark-plugin.umd.js)

​	UMD 格式具备广泛的兼容性，支持 AMD、CommonJS 以及作为全局变量使用。

- AMD 环境

```javascript
requirejs.config({
    paths: {
        watermark: 'path/to/your/v-watermark-plugin.umd.js'
    }
});

require(['watermark'], function (createWaterMark) {
    const options = {
        text: ["vivien"],
    };
    createWaterMark(options); 
});
```

- CommonJS 环境（例如 Node.js 或 Webpack 项目）

```javascript
const { createWaterMark } = require('path/to/your/v-watermark-plugin.umd.js');

const options = {
    text: ["vivien"],
};
createWaterMark(options);
```

### 使用 ESM 格式 [v-watermark-plugin.esm.js](./dist/v-watermark-plugin.esm.js)

​	若你使用的是现代的 ES 模块环境（例如支持 `type="module"` 的浏览器或者打包工具），可以使用 ESM 格式。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>使用 ESM 格式添加水印</title>
</head>
<body>
    <h1>这是示例页面</h1>
    <script type="module">
        import { createWaterMark } from 'path/to/your/v-watermark-plugin.esm.js';

        const options = {
            text: ["vivien"],
        };
        createWaterMark(options);
    </script>
</body>
</html>
```

## 配置参数

​	`createWaterMark` 函数接受一个配置对象作为参数，以下是该对象支持的所有配置项：

| 配置项       | 类型               | 默认值                     | 描述                                                         |
| ------------ | ------------------ | -------------------------- | ------------------------------------------------------------ |
| text         | string[]           | ['域账号 日期']            | **必填项**。水印文本内容，支持多行显示，日期默认取当前日期，可不传。 |
| fontSize     | string             | '14px'                     | 水印文本的字体大小，可使用常见的 CSS 字体大小单位，如 px、em 等。 |
| color        | string             | '#c9c9c9' | 水印文本的颜色，支持 CSS 颜色值，如十六进制、RGB、RGBA 等。  |
| rotate       | number             | -25                        | 水印的旋转角度，单位为度，正值表示顺时针旋转，负值表示逆时针旋转。 |
| zIndex       | number             | 9999                       | 水印元素的层级，数值越大，水印越显示在顶层。                 |
| intervalX    | number             | 285                        | 水印在水平方向上的间隔距离，单位为像素。                     |
| intervalY    | number             | 200                        | 水印在垂直方向上的间隔距离，单位为像素。                     |
| opacity      | number             | 0.4                        | 水印的透明度，取值范围为 0（完全透明）到 1（完全不透明）。   |
| fontFamily   | string             | '微软雅黑'               | 水印文本的字体系列，可使用常见的字体名称，如 Arial、Times New Roman 等。 |
| fontWeight   | string             | 'normal'                   | 水印文本的字体粗细，支持 normal、bold、bolder、lighter 以及具体的数值。 |
| fontStyle    | string             | 'normal'                   | 水印文本的字体样式，支持 normal、italic、oblique。           |
| textAlign    | CanvasTextAlign    | 'center'                   | 水印文本的水平对齐方式<br/>取值范围为 'start'、'end'、'left'、'right'、'center'。 |
| textBaseline | CanvasTextBaseline | 'middle'                   | 水印文本的垂直对齐方式<br/>取值范围为 'top'、'hanging'、'middle'、'alphabetic'、'ideographic'、'bottom'。 |

## 注意事项

- **`text` 参数**：该参数必须为数组类型，若需显示多行水印，可在数组中添加多个字符串元素。
- **字体与颜色兼容性**：`fontFamily` 和 `color` 参数需确保使用的字体和颜色在目标浏览器或设备上是兼容的，以避免显示异常。
- **路径问题**：当直接引入文件时，要确保文件路径 `path/to/your/` 正确指向 `v-watermark-plugin` 对应的文件，否则会导致引入失败。