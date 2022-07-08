---
layout: post
category: 技术
title: Composer相关
---

# github token 错误
```zsh
 [UnexpectedValueException]
  Your github oauth token for github.com contains invalid characters: "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"
```
`解决方法`

访问[github new token](https://github.com/settings/tokens)
```zsh
php composer.phar config -g github-oauth.github.com 这里是github新生成的token
```
