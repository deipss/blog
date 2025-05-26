---
layout: default
title: gem
parent: Command
---

# ruby gem bundle 三者的关系

- ruby的安装和使用：brew install ruby

```log
(base) ➜  blog git:(main) brew list | grep ruby
chruby
ruby-install
```

- gem的安装和使用： brew install rubygems

gem 是包管理工具，ruby内置，有点类似 node和npm，python和pip。

- bundle的安装和使用
  bundle是一个具体的gem，用于依赖管理