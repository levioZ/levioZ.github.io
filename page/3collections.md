---
layout: page
title: Collections
permalink: /collection/
icon: bookmark
---

* content
{:toc}

## 工具

* [markdown在线编辑](http://mahua.jser.me/)
* [Smart Address Validation](http://www.pcapredict.com/en-gb/address-capture-software/)    
* [Unicode编码 UTF-8编码 URL编码/解码 Unix时间戳 Ascii/Native编码互转](http://tool.chinaz.com/tools/urlencode.aspx)

## 学习网站

* [runoob.com](http://www.runoob.com/)
* [博客园](http://www.cnblogs.com/)
* [importnew](http://www.importnew.com/)
* [开源中国](http://www.oschina.net/)
* [IBM](http://www.ibm.com/developerworks/cn/java/)
* [iteye](http://www.iteye.com/)
* [可汗学院](https://www.khanacademy.org)
* [infoq](http://www.infoq.com/cn/)
* [csdn](http://blog.csdn.net/)
* [stackoverflow](http://stackoverflow.com/)
* [spring tutorials](https://spring.io/guides#tutorials)
* [spring doc](http://docs.spring.io/spring/docs/current/spring-framework-reference/html/)
* [spring Framework Reference Documentation cn](http://spring.cndocs.tk/)
* [Spring Security Reference Documentation](http://docs.spring.io/spring-security/site/docs/3.0.x/reference/springsecurity.html)
* [Spring Integration Reference Manual](http://docs.spring.io/spring-integration/reference/htmlsingle/)
* [thymeleaf](http://itutorial.thymeleaf.org/)
* [极客学院](http://wiki.jikexueyuan.com/list/java/)
* [csdn 知识库](http://lib.csdn.net/)
* [Python 中文官方文档](http://python.usyiyi.cn/)

## 框架

### React

* [深入理解 React -Thinking in React 中文版](http://reactjs.cn/react/docs/thinking-in-react.html)
* [Thinking in React](http://facebook.github.io/react/docs/thinking-in-react.html)

## 技术的博客

* [凳子_Joinery 邓智容  http://www.dengzhr.com/](http://www.dengzhr.com/)  
* [周XXXX](http://blog.csdn.net/z69183787/article/category/2175163)

## Comments

{% if site.duoshuo_shortname %}
<!-- 多说评论框 start -->
<div class="ds-thread" data-thread-key="{{ site.url }}{{ page.url }}" data-title="{{page.title}}" data-url="{{ site.url }}{{ page.url }}"></div>
<!-- 多说评论框 end -->
{% endif %}

{% if site.disqus_shortname %}
<div id="disqus_thread"></div>
<script>
/**
* RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
* LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables
*/

var disqus_config = function () {
this.page.url = '{{ site.url }}{{ page.url }}'; // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = '{{ site.url }}{{ page.url }}'; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};

(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');

s.src = '//{{site.disqus_shortname}}.disqus.com/embed.js';

s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript" rel="nofollow">comments powered by Disqus.</a></noscript>
{% endif %}


<script>
/**
 * target _blank
 */
(function() {
    var aTags = document.querySelectorAll('.left a')
    for (var i = 0; i < aTags.length; i++) {
        aTags[i].setAttribute('target', '_blank')
    }
}());
</script>
