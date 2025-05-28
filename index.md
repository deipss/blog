---
title: Home
layout: home
nav_order: 1
---

```text
             
              |                                                                    /\\    /\\  
              __ \   _ \  __| _ \  |   |  _ \  |   |  __|   _` |  __| _ \                      
              | | |  __/ |    __/  |   | (   | |   | |     (   | |    __/            _____    
             _| |_|\___|_|  \___| \__, |\___/ \__,_|_|    \__,_|_|  \___|                   
                                  ____/                                                   


```

---
` `
{: .label .label-white }

你来啦！
{: .label .label-black }

Here you are .
{: .label .label-green }

Ты здесь.
{: .label .label-purple }

Tu es là aussi.
{: .label .label-yellow }

いらっしゃい。
{: .label .label-red }

--- 
Ok,Let's Go……

![hello_world.gif](assets%2Fimages%2Fhello_world.gif)

# 欢迎来到我的博客

这里是最新的 20 篇文章：

<div class="home-posts">
  <!-- 在某个页面中显示 docs 目录的所有文件 -->
    <ul>
      {% assign sorted_pages = site.pages | where_exp:"page", "page.dir contains '/docs/'" | sort: "last_modified_date" | reverse %}
        {% for page in sorted_pages limit:20 %}
          <li>{{ page.last_modified_date }}</li><li><a href="{{ page.url }}">{{ page.title }}</a></li>
        {% endfor %}
    </ul>
</div>
--- 

[ my github ](https://github.com/deipss){: .btn .btn-blue .float-right}





