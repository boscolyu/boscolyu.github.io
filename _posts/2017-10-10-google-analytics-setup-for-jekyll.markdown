---
layout: post
Title: "Google Analytics setup for jekyll"
Author: bosco lyu
Date: October 10, 2017
Meta: "Blog"
---
<img src="/images/fulls/05.jpg" class="fit image">

below document is very good to setup the google anaytics
If you already use the Jekyll theme, Please check the theme setting.
because jekyll theme also contain the google analytics setting property.


* good document : 
    * https://michaelsoolee.com/google-analytics-jekyll/

## Strata Jekyll theme setting for google analytics 

*  _config.yml file
```
google_analytics_key: ""
```

* default.html
    * please erase below \ in code block 

```
{\% if jekyll.environment == 'production' and site.google_analytics_key != '' %}
	<script>
		(function(i,s,o,g,r,a,m){i["GoogleAnalyticsObject"]=r;i[r]=i[r]||function(){
		(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
		m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
	})(window,document,"script","//www.google-analytics.com/analytics.js","ga");

		ga("create", "{{ site.google_analytics_key }}", "auto");
		ga("send", "pageview");
	</script>

{\% endif %}
```