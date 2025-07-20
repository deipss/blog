---
layout: default
title: Front-end
has_children: true
permalink: docs/Front-end
---

```text
   [Client]                             [Server]
   ________                            ___________
  |        |                          |           |
  |  User  |--.     INTERNET       .--|   Backend |
  |  App   |  '--.              .--'  |  Service  |
  |________|     '--.        .--'     |___________|
                   _|      |_             
                 .'            '.
                (     Router     )         [Database]
                 '.          .'           ____________
                   '--.__.--'            |            |
                      ||                 |   MySQL /  |
                .=====++====.            |   Redis    |
               ||   Firewall ||          |____________|
                '============'

```