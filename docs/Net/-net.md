---
layout: default
title: Net 
has_children: true
permalink: docs/net
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

                   <---> TCP/IP Stack
                   <---> HTTP / HTTPS
                   <---> WebSocket / MQTT
                   <---> gRPC / RPC

         "Connecting the world, one packet at a time."

```