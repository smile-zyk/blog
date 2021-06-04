HTML常用标签整理
# 基础标签
## !DOCTYPE
定义文档类型。`<!DOCTYPE>`
## html
定义 HTML 文档。
## title
定义文档的标题。
## body
定义文档的主体。
## !--...--
定义注释。`<!--...-->`
# 文字类标签
## 文字容器标签
### h1~h6
标题标签，会加粗加大文字，分为六类。  
实例：
```html
<h1>一级标签</h1>
<h2>二级标签</h2>
<h3>三级标签</h3>
<h4>四级标签</h4>
<h5>五级标签</h5>
<h6>六级标签</h6>
```
实际效果为：
<pre><h1>一级标签</h1><h2>二级标签</h2><h3>三级标签</h3><h4>四级标签</h4><h5>五级标签</h5><h6>六级标签</h6></pre>
### p
段落标签，字体较小，不同的段落标签之间自动换行。  
实例：
```html
<p>我是一个段落</p>
<p>我在上面那个段落的下面，我们两个在不同的段落，所以我会自己换行。</p>
```
实际效果为：
<pre><p>我是一个段落</p><p>我在上面那个段落的下面，我们两个在不同的段落，所以我会自己换行。</p></pre>
## 文字修饰标签
### em,i
斜体标签，把字体变斜。 
实例： 
```html
<em>我是斜体标签</em><br />
<i>我也是斜体标签</i>
```
实际效果：
<pre><em>我是斜体标签</em></br><i>我也是斜体标签</i></pre>
### b,strong
黑体标签，把字体变粗。  
实例：
```html
<b>我是黑体标签</b></br>
<strong>我也是黑体标签</strong>
```
实际效果：
<pre><b>我是黑体标签</b></br><strong>我也是黑体标签</strong></pre>
### small
细体标签，字体更斜。  
实例：
```html
<small>我是细体标签</small>
```
实际效果：
<pre><small>我是细体标签</small></pre>
### br
换行标签。  
实例：
```html
我是一行文字<br />我是另一行文字
```
实际效果：
<pre>我是一行文字<br />我是另一行文字</pre>
### hr
定义水平线。  
实例：
```html
<p>我是一个段落<p><hr />
<p>我是一个段落<p>
```
实际效果：
<pre><p>我是一个段落<p><hr /><p>我是一个段落<p></pre>
### del
删除线标签，给文字添加删除线。  
实例：
```html
<del>我是加了删除线的文字</del>
```
实际效果：
<pre><del>我是加了删除线的文字</del></pre>
# 布局类标签
## div
块容器标签(block)：自己要占一行。
实例：
```html
<div>我是第一个块容器</div>
<div>我是第二个块容器</div>
```
实际效果：
<pre><div>我是第一个块容器</div><div>我是第二个块容器</div></pre>
## span
内联容器(inline)：可以一行直到超出父容器宽度。
实例：
```html
<span>我是第一个内联容器</span>
<span>我是第二个内联容器</span>
```
实际效果：
<pre><span>我是第一个块容器</span><span>我是第二个块容器</span></pre>
# 列表类标签
## ul-li
无序列表标签。
实例：
```html
<ul>
	科目
	<li>语文</li>
	<li>数学</li>
</ul>
```
实际效果：
<pre><ul>科目<li>语文</li><li>数学</li></ul></pre>
## ol-li
有序列表标签。
实例：
```html
<ol>
	科目
	<li>语文</li>
	<li>数学</li>
</ol>
```
实际效果：
<pre><ol>科目<li>语文</li><li>数学</li></ol></pre>
## dl-dt-dd
定义列表标签。
实例：
```html
<dl>
	<dt>HTML</dt>
	<dd>超文本标记语言</dd>
	<dt>CSS</dt>
	<dd>层叠样式表</dd>
</dl>
```
实际效果：
<pre><dl><dt>HTML</dt><dd>超文本标记语言</dd><dt>CSS</dt><dd>层叠样式表</dd></dl></pre>
# 表格类标签
## table
定义表格。
常用属性：  
1.border  
规定表格边框的宽度。  
2.cellpadding  
规定单元边沿与其内容之间的空白。  
3.cellspacing  
规定单元格之间的空白。  
如图：
<img src="https://i.loli.net/2019/10/05/wRD6FKngiQGxSL3.png" >
## caption
定义表格标题。
## th
定义表格中的表头单元格。  
相比td标签，th标签中的文字更加醒目。  
## tr
定义表格中的行。
## td
定义表格中的单元。
th和td标签都有两个很重要的标签，分别为行合并和列合并：rowspan，colspan。  
以该单元格为起点，向右向下合并其他单元格。
## thead
定义表格中的表头内容。
## tbody
定义表格中的主体内容。
## tfoot
定义表格中的表注内容。
</br>
实例：
```html
<table border="1">
  <caption>Example</caption>
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>

  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>

  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
</table>
```
实际效果：
<pre><table border="1"><caption>Example</caption><thead><tr><th>Month</th><th>Savings</th></tr></thead><tfoot><tr><td>Sum</td><td>$180</td></tr></tfoot><tbody><tr><td>January</td><td>$100</td></tr><tr><td>February</td><td>$80</td></tr></tbody></table></pre>
# 表单类标签
## form
定义供用户输入的 HTML 表单。
常用属性有：
1.action 规定当提交表单时向何处发送表单数据。
2.method 规定用于发送 form-data 的 HTTP 方法，具体为：get、post。
3.target 规定在何处打开 action URL，详见<a href="https://www.cnblogs.com/starof/p/4014691.html" target="_blank">超链接a的target属性</a>。
## input
定义输入控件。  
常用属性有：  
1.type 规定 input 元素的类型,主要有button、checkbox、password、radio、reset、submit、text等。  
2.name 定义 input 元素的名称。  
3.value 规定 input 元素的值。  
## button
定义按钮。
尽管已经有了input标签可以用作表示按钮，但是为了标签的语义化，我们引入了button标签也可以表示按钮。  
相比input提供的按钮，button标签有着更多的功能。
常用属性：type：input或者submit。  
## textarea
定义多行的文本输入控件。
常用属性：  
1.cols 规定文本区内的可见宽度。  
2.rows 规定文本区内的可见行数。
## select-option
定义选择列表（下拉列表）。
实例：
```html
<br />
<form action="">
	user:<input type="text" />
	<br />
	password:<input type="password" />
	<br />
	gender<input type="radio" checked="checked" name="gender"/>male
	<input type="radio" name="gender">female
	<br />
	hobby <input type="checkbox" checked="checked" />CSGO
	<input type="checkbox" />LOL
	<input type="checkbox" />OW
	<br /> address
	<select name="address" id="0">
	<option value="ch">china</option>
	<option value="am">americal</option>
	<option value="jp" selected="selected">japan</option>
	<option value="en">english</option>
	</select>
	<br />
	<textarea name="text" id="1" cols="30" rows="10"></textarea>
	<br />
	<button type="submit">提交</button>
	<input type="reset" value="重置" />
</form>
```
实际效果：
<pre><form action="">user:<input type="text" /><br />password:<input type="password" /><br />gender<input type="radio" checked="checked" name="gender"/>male<input type="radio" name="gender">female<br />hobby <input type="checkbox" checked="checked" />CSGO<input type="checkbox" />LOL<input type="checkbox" />OW<br /> address<select name="address" id="0"><option value="ch">china</option><option value="am">americal</option><option value="jp" selected="selected">japan</option><option value="en">english</option></select><br /><textarea name="text" id="1" cols="30" rows="10"></textarea><br /><button type="submit">提交</button> <input type="reset" value="重置" /></form></pre>
# 图像标签
图像标签为img，它有几个重要的属性：  
src：图片来源，可以是本地图片（绝对地址和相对地址），可以是图片的链接。  
alt：用来代替图片的文本，它有两个作用，一个是在图片加载失败时显示，一个是有利于搜索引擎的收录。  
实例：
```html
<img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570872627&di=450f95a557f17d1badcdcfc4ace2ea92&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.cwq.com%2F201712%2F1513127498165415.jpeg" alt="hello-world">
```
实际效果：
<pre><img src="https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570872627&di=450f95a557f17d1badcdcfc4ace2ea92&imgtype=jpg&er=1&src=http%3A%2F%2Fimg.cwq.com%2F201712%2F1513127498165415.jpeg" alt="hello-world"></pre>
# 超链接标签
超链接标签为a，它有两个重要属性：
href：超链接指向，它可以指向三种不同的内容：
1.URL：同一资源定位符 如：http://www.baidu.com  
2.URI：同一资源标志符 如：tel:10086/mail:****@163.com...
3.文件路径 如../1.html
target：详见<a href="https://www.cnblogs.com/starof/p/4014691.html" target="_blank">超链接a的target属性</a>
实例：
```html
<a href="http://www.baidu.com" target="_blank">baidu</a>
```
实际效果：
<pre><a href="http://www.baidu.com" target="_blank">baidu</a></pre>