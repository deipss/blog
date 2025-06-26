---
title: Home
layout: home
nav_order: 1
---


¡Has venido!
{:.label.label-purple }

Tu es venu(e) !
{:.label.label-yellow }

Du bist gekommen!
{:.label.label-red }

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

Ben arrivato!
{: .label .label-blue }

Você chegou!
{: .label .label-black }

당신이 왔어요!
{: .label .label-purple }

आप आ गए!
{: .label .label-yellow }

Siz geldiniz!
{: .label .label-black }

Sen burada!
{: .label .label-red }

Anda di sini!
{: .label .label-purple }

---

# Welcome to my blog

recent posts:

<div class="home-posts">
    <ul>
      {% assign sorted_pages = site.pages | where_exp:"page", "page.dir contains '/docs/'" | sort: "last_modified_date" | reverse %}
        {% for page in sorted_pages limit:20 %}
          <li>{{ page.last_modified_date }} - <a href="/blog{{ page.url }}">{{ page.title }}</a></li>
        {% endfor %}
    </ul>
</div>
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



