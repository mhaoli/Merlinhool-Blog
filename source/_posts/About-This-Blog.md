title: 建站大业
comment: true
date: 2014-12-26 09:19:50
updated: 2015-09-09 22:57:00
categories: 博客
tags: BsLight
---
记录自己对BsLight主题的部分更改与一些较复杂的添加功能。   
持续更新。   
<!--more-->
注意：以下目录为"theme/..."是指你所用的主题目录下。   

##Add MathJax
实现的方法很多，比如使用CatX插件，或者更改页面代码。我选择了后者。   
在theme/layout/_partial/下新建mathjax.ejs：
```
	<script type="text/x-mathjax-config">
  		MathJax.Hub.Config({
    		tex2jax: {
      			inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      			processEscapes: true
		    }
  		});
	</script>

	<script type="text/x-mathjax-config">
    	MathJax.Hub.Config({
     		tex2jax: {
        		skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
      		}
    	});
	</script>

	<script type="text/x-mathjax-config">
    	MathJax.Hub.Queue(function() {
        	var all = MathJax.Hub.getAllJax(), i;
        	for(i=0; i < all.length; i += 1) {
            	all[i].SourceElement().parentNode.className += ' has-jax';
        	}
    	});
	</script>

	<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
	</script>
```
然后在页面中调用就好了。在theme/layout/_partial/after_foot.ejs里添加： 
```
<%- partial('mathjax') %>
```
这样就好了。但是存在两个问题。     

####**the first one**
如[这篇博文](http://zhyin5.com/2014/04/11/%E5%85%B3%E4%BA%8Emarkdown%E8%AF%AD%E6%B3%95%E4%B8%8Elatex%E8%AF%AD%E6%B3%95%E7%9A%84%E5%86%B2%E7%AA%81/)所说的，MathJax与markdown解析器的冲突。~~但是我稍微测试了一下，发现目前还没有问题，出现了再解决吧。。~~   
更换了解析器，选择了语法更强的[pandoc-markdown](http://johnmacfarlane.net/pandoc/)，hexo下可使用插件[hexo-renderer-pandoc](https://github.com/wzpan/hexo-renderer-pandoc)。    
安装方法：     
首先点进上面的页面安装pandoc。    
然后有很重要一步，一定要将pandoc.exe所在目录设为环境变量，不然后面hexo g会失败。    
最后，在git bash下面执行命令：
```
npm install hexo-renderer-pandoc --save
```    
最后的最后....因为语法略有改变，去折腾之前的文章吧> <    

####**the second one**
MathJax加载慢，于是考虑只有在需要的时候才加载mathjax.ejs。所以在theme/layout/_partial/after_foot.ejs中插入的代码更改为：
```
<% if (page.mathjax){ %>
<%- partial('mathjax') %>
<% } %>
```
然后，文章需要使用mathjax的话就在md文件的front-matter部分加上mathjax: true。   
当然，这样又出现了一个问题，就是在home page上面不会运行mathjax.ejs。如果需要运行，只需要在theme/layout/index.ejs里添加：
```
<%- partial('mathjax') %>
```

##Add “next page” button      
在theme/layout/_partial/post/下面写一个prev_next.ejs：
```
<% if (page.prev || page.next){ %>
<div class="prev_next clearfix">
  <% if (page.prev){ %>
    <a href="<%- config.root %><%- page.prev.path %>" class="alignleft prev" title="<%= page.prev.title %>"><%= page.prev.title %></a>
  <% } %>
  <% if (page.next){ %>
    <a href="<%- config.root %><%- page.next.path %>" class="alignright next" title="<%= page.next.title %>"><%= page.next.title %></a>
  <% } %>
</div>
<% } %>
```
然后修改文章模板。打开themes/layout/_partial/article.ejs，大概是在下面的位置这样添加：    
**2015.1.1UPD：按照原来的添加方法，在home page的文章页数超过1页时会有问题。fixed。**
```
 <footer>
      <%- partial('post/category') %>
      <%- partial('post/tag') %>
      <% if(!index){ %>
        <%- partial('post/prev_next') %>
      <% } %>
```
最后，添加相应的css。在theme/source/css/_partial/article.styl末尾添加：
```
.prev_next
  margin 1em 0
  clear both
  overflow hidden
  a
    display block
    float left
    width 50%
    background #dbdbdb
    text-align center
    padding 0.4em 0
    color #1ba1e2
    transition background .45s color .45s
    &:hover
      color #fafafa
      background #717171
    &.prev::before
      content "Previous："
      padding-right 0.5em
    &.next::before
      content "Next："
      padding-right 0.5em
```

##Add drop-shadow   
这是我在乱逛的时候发现的前端效果，非常赞，推荐！      
[效果介绍](http://zipperary.com/2013/06/23/box-and-shadow-effect/)。下面是添加的方法。    
在theme/source/css/_partial/article.styl中找到.post-content，在他后面的平行层添加：
```
.post-content:before
    content: "";
    position: absolute;
    z-index: -1;
    bottom: 15px;
    left: 10px;
    width: 50%;
    height: 20%;
    -webkit-box-shadow: 0 15px 10px rgba(0, 0, 0, 0.7);
    -moz-box-shadow: 0 15px 10px rgba(0, 0, 0, 0.7);
    box-shadow: 0 15px 15px rgba(0, 0, 0, 0.7);
    -webkit-transform: rotate(-2deg);
    -moz-transform: rotate(-2deg);
    -o-transform: rotate(-2deg);
    transform: rotate(-2deg);
  
  .post-content:after
    content: "";
    position: absolute;
    z-index: -1;
    bottom: 15px;
    left: 10px;
    width: 50%;
    height: 20%;
    -webkit-box-shadow: 0 15px 10px rgba(0, 0, 0, 0.7);
    -moz-box-shadow: 0 15px 10px rgba(0, 0, 0, 0.7);
    box-shadow: 0 15px 15px rgba(0, 0, 0, 0.7);
    -webkit-transform: rotate(-2deg);
    -moz-transform: rotate(-2deg);
    -o-transform: rotate(-2deg);
    transform: rotate(-2deg);
    right: 10px;
    left: auto;
    -webkit-transform: rotate(2deg);
    -moz-transform: rotate(2deg);
    -o-transform: rotate(2deg);
    transform: rotate(2deg);
```
等什么时候有空再研究下怎么加到comment的框架上。             

##Add some drafts
找到了在静态blog里用来写私密文章的方法(握拳            

其实就是利用草稿功能。         
```
$ hexo new draft "new draft"
```
该命令会在source/_drafts目录下生成一个new-draft.md文件。           

这篇文章不显示在blog上，不能被访问，也不会上传到github上。          

如果你希望强行预览草稿，更改配置文件：
```
render_drafts: true
```
或者，如下方式启动server：
```
$ hexo server --drafts
```
下面这条命令可以把草稿变成文章，或者页面：
```
$ hexo publish [layout] <filename>
```
