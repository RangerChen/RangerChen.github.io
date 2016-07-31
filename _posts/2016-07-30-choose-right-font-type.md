---
layout: post
title: "为博客挑选合适的字体"
---
关于博客标题，最初是“为WEB应用挑选合适的字体”，但是经过再三的斟酌，还是更改成了现在的标题。为什么呢？其实我自己也不能给出明确的答案，可能是害怕使用"WEB应用"这样的大范围的词之后，无法驾驭文章的实用性，也可能是我只是想为自己的博客挑选一个适合阅读的字体罢了，并不想深究。

进入正题：什么样的字体适合阅读呢？这里就不得不提到web字体中的两大字体族，他们分别是**Serif**和**Sans Serif**，对应翻译为中文就是**衬线体**和**无衬线体**，关于衬线体和无衬线体的讨论，我在[Serif VS Sans Serif](/font-type/blog-build/2016/07/29/sans-vs-serif.html)文章当中做了初步的描述和讲解，这里可以直接引用文章最后的结论，就是**在web页面中，应该优先使用无衬线体。**

除了适合阅读，我们更希望的是，我们的博客看起来更美观一点（难道不是么？）。在这里，需要思考的问题是各个浏览器当中所包含的字体是不尽相同的，这样会造成设置了单一的字体之后，当一些浏览器当中没有默认包含该字体时，就会使用浏览器默认的字体进行覆盖，其作用原理和文章[统一浏览器的显示效果](/font-type/blog-build/2016/07/29/font-type.html)是一样的。那么，如何才能让浏览器'服从命令,如臂指挥'呢？这里，我使用的是撒网战术：按照优先级，设置诸多字体，不管浏览器的默认字体库如何简略，总有命中的。下面让我们来看看各大网站都是如何处理这个问题的：

* [Github](https://github.com/)

```
	font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
```

* [stackoverflow](http://stackoverflow.com/)

```
	font-family: Arial,"Helvetica Neue",Helvetica,sans-serif;
```

* [知乎](http://www.zhihu.com/)

```
	font-family: 'Helvetica Neue',Helvetica,Arial,sans-serif;
```

* [网易新闻](http://news.163.com/)

```
	font-family: "Microsoft YaHei","\5fae\8f6f\96c5\9ed1","\5b8b\4f53",sans-serif;
```

* [博客园](http://www.cnblogs.com/)

```
	font-family: Helvetica,Verdana,Arial,sans-serif;
```

通过对各大网站的字体使用情况进行统计，可以得出如下的结论：    

* 都统一使用了无衬线体(Sans serif);
* 都在fon-family中设置了至少4种字体；
* 英文内容为主的站点，字体可选空间远超过中文内容为主的站点。

最后，参考各大网站的字体设置，我的博客字体设置代码如下：

```
	font-family: "Microsoft YaHei",Arial,Helvetica,sans-serif,"\5b8b\4f53";
```

**注**："\5fae\8f6f\96c5\9ed1"的中文转码为"微软雅黑","\5b8b\4f53"的中文转码为"宋体"。
