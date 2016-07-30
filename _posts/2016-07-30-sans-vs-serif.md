---
layout: post
title:  "Serif VS Sans Serif"
date:   2016-07-29 09:40:56
author: Ranger, Hush Please
overview: font type
categories: font-type blog-build
---
首先是中英文对照

Serif -> 衬线体，以下是网页效果：
<div style="font-size: 96px;font-family: Georgia;overflow-x:hidden;">ABCDEFGHIGHLMN</div>
<div style="font-size: 96px;font-family: 宋体;overflow-x:hidden;">中文衬线体</div>
Sans Serif -> 无衬线体，以下是网页效果：
<div style="font-size: 96px;overflow-x:hidden;">ABCDEFGHIGHLMN</div>
<div style="font-size: 96px;overflow-x:hidden;">中文无衬线体</div>
从上面的示例当中可以看出，衬线体着重强调了字母或笔划的开始和结束，而无衬线体则整体较为醒目。下面就两种字体做简单的比较：

* Serif的字体容易辨认，因此易读性较高。反之Sans Serif则较醒目，但在行文阅读的情况下，Sans Serif容易造成字母辨认的困扰，常会有来回重读及上下行错乱的情形；
* Serif强调了字母笔划的开始与结束，因此较易前后连续性的辨识；
* Serif强调一个word，而非单一的字母，反之Sans Serif强调个别字母；
* 在小字体的场合，通常Sans Serif比Serif更清晰。

在传统印刷中，衬线字体用于正文印刷，因为它被认为比无衬线体更易于阅读，是比较正统的。相对的，无衬线体用于短篇和标题等，能够引起读者注意，或者提供一种轻松的气氛。像宣传类、海报类，为求醒目，它的短篇的段落也会采用Sans Serif字体。但在书籍、报刊杂志等正文有相当篇幅的情况下，则应采用Serif字体来减轻读者阅读上的负担。在Web设计及浏览器设置中也应遵循此原则。这里需要着重指出的是，这种结论的前提条件是在**传统印刷**中。

目前在计算机领域中倾向使用无衬线字体以方便在显示器上显示。因为，虽然衬线字体从审美角度较为正式优美，但是眼睛的感受并不及不采用衬线的黑体字，衬线体在笔划上有过多的点缀（笔划末端的小三角）很容易造成视觉疲劳（尤其是显示在目前常规的像素屏幕上时）。出于上述原因，大部分网页使用无衬线字体。另外，为了更好解决衬线字体的显示问题，新的反锯齿和次像素显示（如ClearType）等技术开始广泛运用。但是目前最一般的显示器分辨率也不过每英寸100像素，这是屏幕显示衬线体可读性的瓶颈所在。由此，也可以解释为什么衬线体在retina屏幕上的表现会更亮眼，其根本原因还是在笔画的开始和结尾的修饰上像素的还原程度较高。但由于目前retina屏幕的普及程度较低，所以还是无衬线体字体来作为web显示的基础字体。

由此，我们就不难得出最终的结论：**在web页面中，应该优先使用无衬线体。**

    