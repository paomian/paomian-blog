---
layout: post
title: "把html变为hiccup"
date: 2014-03-31 16:12
comments: true
categories: 
---
用clojure写web程序的时候，让我感觉不爽的是，html的编写，因为大部分都是用模板语言。

我个人认为用html写也是可以的，可是大家都推荐用模板语言，我也就跟着大神走吧，以前写的时候

还怨声载道，可是在啊后来慢慢的学习中慢慢发现了模板语言的强大之处

1. 首先，他是clojure代码，这样可以无缝与clojure代码结合，而且lisp的特性代码即数据。
    
    使得这些模板语言的控制与重复利用的非常有效率。

2. 再者就是好定制，嵌入，和拆分，这点用起来是非常爽的，一个小的html代码段，可以多次利用。

    虽然别的模板语言用了特殊的方式处理这些，但我认为clojure模板语言还是可以接受的。
---------

**但是一个很大的问题是，网上有很好的html模板代码，但是无法使用，这大段的html无法使用的确让人感觉很不爽**

我就从网上找了找转换的模板语言，就找到了这个[hickory][1]

[1]:https://github.com/davidsantiago/hickory

我只是用了这其中的一个功能，他本身也是一个模板语言，我只是用hiccup习惯了，索性就用他来转化html了

以下是粘贴自hickory的github主页 

```clojure
user=> (use 'hickory.zip)
nil
user=> (require '[clojure.zip :as zip])
nil
user=> (-> (hiccup-zip (as-hiccup (parse "<a href=foo>bar<br></a>"))) zip/node)
([:html {} [:head {}] [:body {} [:a {:href "foo"} "bar" [:br {}]]]])
user=> (-> (hiccup-zip (as-hiccup (parse "<a href=foo>bar<br></a>"))) zip/next zip/node)
[:html {} [:head {}] [:body {} [:a {:href "foo"} "bar" [:br {}]]]]
user=> (-> (hiccup-zip (as-hiccup (parse "<a href=foo>bar<br></a>"))) zip/next zip/next zip/node)
[:head {}]
user=> (-> (hiccup-zip (as-hiccup (parse "<a href=foo>bar<br></a>"))) 
           zip/next zip/next 
           (zip/replace [:head {:id "a"}]) 
           zip/node)
[:head {:id "a"}]
user=> (-> (hiccup-zip (as-hiccup (parse "<a href=foo>bar<br></a>"))) 
           zip/next zip/next 
           (zip/replace [:head {:id "a"}]) 
           zip/root)
([:html {} [:head {:id "a"}] [:body {} [:a {:href "foo"} "bar" [:br {}]]]])
user=> (-> (hickory-zip (as-hickory (parse "<a href=foo>bar<br></a>"))) 
           zip/next zip/next 
           (zip/replace {:type :element :tag :head :attrs {:id "a"} :content nil}) 
           zip/root)
{:type :document, :content [{:type :element, :attrs nil, :tag :html, :content [{:content nil, :type :element, :attrs {:id "a"}, :tag :head} {:type :element, :attrs nil, :tag :body, :content [{:type :element, :attrs {:href "foo"}, :tag :a, :content ["bar" {:type :element, :attrs nil, :tag :br, :content nil}]}]}]}]}
user=> (hickory-to-html *1)
"<html><head id=\"a\"></head><body><a href=\"foo\">bar<br></a></body></html>"
```
