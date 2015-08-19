title: database-note
date: 2015-08-20 05:55:47
tags:
---
# MySQL
## 查此session是用那個帳號登入

> Actually, you need to use two functions
>
> `SELECT USER(),CURRENT_USER();`
> USER() reports how you attempted to authenticate in MySQL
>
> CURRENT_USER() reports how you were allowed to authenticate in MySQL
>
> Sometimes, they are different
