# HTML5幻灯片库reveal.js使用

官方demo:      [demo](http://lab.hakim.se/reveal-js/#/)

## 特点

​    `reveal.js`有一下几个特点：  

- 支持标签来区分每一页幻灯片
- 可以使用markdown来写内容
- 支持pdf的导出
- 支持演说注释
- 提供JavaScript API来控制页面
- 提供了多个默认主题和切换方式

## 幻灯片实现步骤

1. 从[reveal.js](https://github.com/hakimel/reveal.js)上下载压缩包，并解压      
2. 进入`reveal.js`文件夹，直接修改`index.html`文件就可以      

## 幻灯片内容实现方法

幻灯片的内容需要包含在`<div class="reveal"><div class="slides">`的标签中。    一个 `section`是一页幻灯片。当`section`包含在`section`中时，是一个纵向的幻灯片。    

```html
<div class="reveal">
	<div class="slides">
		<section>Single Horizontal Slide</section>
		<section>
			<section>Vertical Slide 1</section>
			<section>Vertical Slide 2</section>
		</section>
	</div>
</div>
```

## html实现内容

### 标题和正文

`section`中的内容就是幻灯片的内容，你可以使用`h2`标签标示`title`, `p`表示内容。需要红色的字体可以直接设置`style`的`color`为`red`。    

当某一页需要特殊背景色，可以使用`data-background`在`section`上设置,`data-background-transition`表示背景的过渡效果。

```html
<section data-background-transition="zoom" data-background="#dddddd">
```

正文一段一段出现，可以使用`fragment`

```html
<p class="fragment"></p>
```

### 代码

`reveal.js`使用`highlight.js`来支持代码高亮。可以直接写code标签来实现,    `data-trim`表示去除多余的空格

```html
<pre><code data-trim>
  console.log('hello reveal.js!');
</code></pre>
```

### 注释

在演说时，会用到注释，对于注释，可以通过<aside class="notes">来实现。For Example:

```html
<aside class="notes">
  这里是注释。
</aside>
```

在幻灯片页面，按下`s`键，就可以调出注释页面，注释页面包含了当前幻灯片，下一章幻灯片，注释，以及幻灯片播放时间。  

## markdown实现

​    `reveal.js`不仅支持html表示来实现内容， 还可以通过`markdown`来实现内容。使用`markdown`实现内容时，需要对`section`标示添加`data-markdown`属性，然后将`markdown`内容写到一个`text/template`脚本中。

```html
<section data-markdown>
    <script type="text/template">
        ## Page title

        A paragraph with some text and a [link](http://hakim.se).
    </script>
</section>
```

背景色，`fragment`功能的实现，可以通过注释来实现。

```html
<section data-markdown>
    <script type="text/template">
    <!-- .slide: data-background="#ff0000" -->
        - Item 1 <!-- .element: class="fragment" data-fragment-index="2" -->
        - Item 2 <!-- .element: class="fragment" data-fragment-index="1" -->
    </script>
</section>
```

### 外置md文件

​    `reveal.js`可以引用一个外置的`markdown`文件来解析。

```html
<section data-markdown="example.md"  
         data-separator="^\n\n\n"  
         data-separator-vertical="^\n\n"  
         data-separator-notes="^Note:"  
         data-charset="iso-8859-15">
</section>
```

### 分页实现

一个`markdown`文件中可以连续包含多个章内容。可以在`section`中通过属性`data-separator`,`data-separator-vertical`来划分章节。

```html
<section data-separator="---" data-separator-vertical="--"  >
  <script type="text/template">
    # 主题1
    - 主题1-内容1
    - 主题1-内容2
    --
    ## 主题1-内容1
    内容1-细节1
    --
    ## 主题1-内容2
    内容1-细节2
    ---
    # 主题2
  </script>
</section>
```

### 注释

对    `section`添加    `data-separator-notes="^Note:"`属性，就可以指定    `Note:`后面的内容为当前幻灯片的注释。For Example:  

```html
# Title
## Sub-title

Here is some content...

Note:
This will only display in the notes window.
```

## PDF导出

可以利用浏览器保存为pdf的功能来实现pdf的转化。步骤是

1. 再url后面添加`print-pdf`参数，访问后，页面会去加载打印用的css文件，页面效果就是pdf的样式。      
2. 右键选择打印。设置为保存pdf。

我试过保存pdf的功能，有内容会重叠，怀疑是样式没有处理好。

## 多主题

​    `reveal.js`提供了多种样式。可以通过引用不同的主题来实现。具体主题查看`reveal.js/css/theme`下的css文件。  







