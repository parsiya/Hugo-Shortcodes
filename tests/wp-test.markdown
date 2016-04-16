---
date: 2016-04-16T00:07:14-04:00
draft: false
title: WP tag test
---

### Named variable test

* {{< wp tag="VIC_cipher" >}}
* {{< wp tag="VIC_cipher" lang="fr" >}}
* {{< wp tag="VIC_cipher" lang="fr" title="" >}}
* {{< wp tag="VIC_cipher" title="VIC Cipher" >}}
* {{< wp tag="VIC_cipher" lang="en" title="VIC Cipher" >}}


### Positional variable test

* {{< wp VIC_cipher >}}
* {{< wp VIC_cipher fr >}}
* {{< wp VIC_cipher "" fr >}}
* {{< wp VIC_cipher "VIC Cipher" >}}
* {{< wp VIC_cipher "VIC Cipher" fr >}}
