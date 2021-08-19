---
tags:
  - writingidea
  - code
---

## Issue

If you get this error

```
TypeError: Object.entries(…).flatMap is not a function at Array.forEach 
```

when running `npx webpack --mode=production` on an [[Ubuntu]] server. This is because your server using an old Node version. 

## Fix

If you installed [[Nodejs]] via `sudo apt install nodejs` , then this is how you update it.

```
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```

then

`sudo apt install nodejs`

finally

```
sudo apt install build-essential
```

This will update your [[Nodejs]] version and you should be able to run `npx webpack`

Tags: [[Webpack]], [[npm]], [[npx]]

> sidenote: this problem can be a good thing to write about and share on the [[Digital Ocean]] blog.