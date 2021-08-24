---
layout:
title: React Library 網頁浮水印 （浮水印文字可換行）
date: 2021-04-14 21:32:43
categories: Library 分享
tags: 
- React
- Library
- 浮水印
- 工作
- 分享
photos:
- https://github.com/saucxs/watermark-dom/raw/master/examples/img/demo.png
---

> 最近工作上出現了一個需求：在整個網頁加上文字浮水印
沒錯，不是在圖片上加浮水印，是整個網頁⋯
<!-- more -->

![saucxs/watermark-dom](https://github.com/saucxs/watermark-dom/raw/master/examples/img/demo.png)
圖源：[saucxs/watermark-dom](https://github.com/saucxs/watermark-dom)

---

<br />

# 簡介
找了一堆浮水印的 Library，但大多都有個問題——__文字浮水印沒辦法換行__，
找半天終於找到可以換行的救星：__[@pansy/watermark](https://www.npmjs.com/package/@pansy/watermark)__
![@pansy/watermark](pansy_watermark.png "@pansy/watermark")

# API
API 只有兩個：
- `update(options);` 修改浮水印 options
- `render();` 渲染浮水印

所以只要兩行就解決煩惱：
{% codeblock lang:js %}
// options 值為版本 1.2.0 之預設值
update({
  mode: 'repeat',
  monitor: true,
  container: 'body',
  text: ['text1','text2','text3'],
  zIndex: 9999,
  width: 160,
  height: 80,
  opacity: 0.2,
  rotate: 20,
  fontSize: 14,
  fontWeight: 'normal',
  fontColor: '#727071',
  fontFamily: 'sans-serif',
  textAlign: 'center',
});
render();
{% endcodeblock %}

## 浮水印設定參數
|    參數    |                              說明                              |         類型         |   預設值   |  版本 |
|:----------:|:--------------------------------------------------------------:|:--------------------:|:----------:|:-----:|
| mode       | 浮水印是重複排列還是間隔排列                                   | repeat \| interval   | `repeat`     | 1.2.0 |
| monitor    | 監聽浮水印元素是否被篡改、被修改或者删除等操作，則重新渲染水印 | boolean              | `true`       | --    |
| container  | 浮水印掛載的容器                                               | HTMLElement \| sting | `body`       |       |
| text       | 浮水印文本                                                     | string \| string[]   | --         | --    |
| zIndex     | 浮水印層級                                                     | number               | `9999`       |       |
| width      | 單個浮水印區域寬度                                             | number               | `160`        | --    |
| height     | 單個浮水印區域高度                                             | number               | `80`         | --    |
| opacity    | 透明度                                                         | number               | `0.2`        | --    |
| rotate     | 旋轉的角度                                                     | number               | `20`         | --    |
| fontSize   | 字體大小                                                       | number               | `14`         | --    |
| fontWeight | 字體粗细                                                       | --                   | `normal`     | --    |
| fontColor  | 字體顏色                                                       | string               | `#727071`    | --    |
| fontFamily | 字體設定                                                   | string               | `sans-serif` | --    |
| textAlign  | 文本對齊設定                                                   | string               | `center`     | --    |

# Library 連結
package: [@pansy/watermark](https://www.npmjs.com/package/@pansy/watermark)
demo: [@pansy/watermark Demo](https://react-components-vert.vercel.app/components/basic/watermark)