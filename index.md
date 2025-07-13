---
title: Home
layout: home
nav_order: 1
---


¡Has venido!
{:.label.label-purple }

Ты пришел/пришла!
{: .label .label-black }

Tu es venu(e) !
{:.label.label-yellow }

Ελήθηκες!
{: .label .label-blue }

Du bist gekommen!
{:.label.label-red }

你来啦！
{: .label .label-black }

Here you are .
{: .label .label-green }

Ты здесь.
{: .label .label-purple }

Você chegou aqui!
{: .label .label-green }

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

لقد أتيت!
{: .label .label-orange }



---

# Welcome to my blog

recent posts:
<div class="home-posts two-column-wrapper" style="display:flex; gap:2em;">
  <ul>
    {% assign sorted_pages = site.pages | where_exp:"page", "page.dir contains '/docs/'" | sort: "last_modified_date" | reverse %}
    {% for page in sorted_pages limit:15 %}
      <li>{{ page.last_modified_date }} - <a href="/blog{{ page.url }}">{{ page.title }}</a></li>
    {% endfor %}
  </ul>
  <ul>
    {% for page in sorted_pages offset:15 limit:15 %}
      <li>{{ page.last_modified_date }} - <a href="/blog{{ page.url }}">{{ page.title }}</a></li>
    {% endfor %}
  </ul>
</div>

--- 

```text

    /-------------------------------------------------------------\
   /                                                               \
  /                                                                 \
 /                                                                   \
/                                                                     \
                        ☀️                                       🌙
+-----------------------------------------------------------------------+
|                                                                       |
|  _     _     _     _     _     _     _     _                          |
| | |   | |   |▀▀|   | |   | |   | |   | |   | |   | |                  |
| |_|   |_|   |▄▄|   |_|   |_|   |_|   |_|   |_|   |_|                  |
|                                                                       |
|  _     _     _     _     _     _     _     _                          |
| | |   | |   | |   | |   | |   | |   | |   | |   | |                   |
| |_|   |_|   |_|   |_|   |_|   |_|   |_|   |_|   |_|                   |
|                                                                       |
+-----------------------------------------------------------------------+
     |           |           |           |           |           |
     |   Python  |   Java    |   C++     |   JS      |   Ruby    |    O   O   O   O
     |           |           |           |           |           |   /|\ /|\ /|\ /|\
     |    ____   |   ____    |   ____    |   ____    |   ____    |   / \ / \ / \ / \
     |   |    |  |  |    |   |  |    |   |  |    |   |  |    |   |
     |   |  Py|  |  | Java|  |  | C++|   |  | JS |   |  |Ruby|   |
     |   |____|  |  |____|   |  |____|   |  |____|   |  |____|   |
     |           |           |           |           |           |
     |   ______  |  _______  |  ________ |  ________ |  ________ |
     |  |TensorFlow| |Spring | |Qt      | |React     | |Rails     |
     |  |________| |________| |________| |________|  |________|   |
     |                                                               |
     |_______________________________________________________________|                                                                        
```



