---
title: Home
layout: home
nav_order: 1
---

```text
 _    _                                                    
| |  | |                                                   
| |__| | ___ _ __ ___   _   _  ___  _   _    __ _ _ __ ___ 
|  __  |/ _ \ '__/ _ \ | | | |/ _ \| | | |  / _` | '__/ _ \
| |  | |  __/ | |  __/ | |_| | (_) | |_| | | (_| | | |  __/
|_|  |_|\___|_|  \___|  \__, |\___/ \__,_|  \__,_|_|  \___|
                         __/ |                             
                        |___/                              
                                              
```

---

¡Has venido!
{:.label.label-blue }

Tu es venu(e) !
{:.label.label-pink }

Du bist gekommen!
{:.label.label-orange }

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

# Welcome to my blog

recent posts:

<div class="home-posts">
  <!-- 在某个页面中显示 docs 目录的所有文件 -->
    <ul>
      {% assign sorted_pages = site.pages | where_exp:"page", "page.dir contains '/docs/'" | sort: "last_modified_date" | reverse %}
        {% for page in sorted_pages limit:20 %}
          <li>{{ page.last_modified_date }} - <a href="{{ page.url }}">{{ page.title }}</a></li>
        {% endfor %}
    </ul>
</div>
--- 

[ my github ](https://github.com/deipss){: .btn .btn-blue .float-right}





