---
layout: post
title: "在Octopress中使用Latex公式"
date: 2012-11-06 18:17
comments: true
categories: Octopress
---

对于我等diaosi，偶尔还是会需要在blog中输入一些符号、公式之类

But How？

* In the first, Use kramdown instead of rdiscount

``` bash
    gem install kramdown
```

然后在配置文件_config.yml中替换设置


``` bash
markdown: kramdown
```

* 设置样式  
Modify source/_layouts/defaults.html  

``` html
<!-- mathjax config similar to math.stackexchange -->
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
  jax: ["input/TeX", "output/HTML-CSS"],
  tex2jax: {
    inlineMath: [ ['$', '$'] ],
    displayMath: [ ['$$', '$$']],
    processEscapes: true,
    skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']
  },
  messageStyle: "none",
  "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
});
</script>
<script src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML" type="text/javascript"></script>

```


* 解决右击公式全屏空白问题

Modify sass/base_theme.scss

``` html
body {
  > div#main {
    background: $sidebar-bg $noise-bg;
```
