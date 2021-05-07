---
layout: post
title: Fix error RC2104 undefined keyword or keyname
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - programming
  - windows
  - misc
---

## Introduction

When you use the **Microsoft Visual Studio** to compile a cpp
project, and encounter this problem about `error RC2104: undefined keyword: Key`, here is an article on how to fix this problem.

## Review

The picture best illustrates the problem, the error message and
related code is shown as below image:

![image](https://user-images.githubusercontent.com/9413601/98320058-0a11a100-201d-11eb-98bd-1423fbc9cf6d.png)

Therefore, let's find more about the `error RC2104`. And the error
definition can be found in [Resource Compiler Error RC2104](https://docs.microsoft.com/en-us/cpp/error-messages/tool-errors/resource-compiler-error-rc2104).

> This error is often caused by a typo in the resource definition,
> or in the included header file. It can also be caused by a missing
> header file.

![image](https://user-images.githubusercontent.com/9413601/98322246-f583d780-2021-11eb-97b6-cb9385e5beb1.png)

But here the problem is quite strange, when you locate to the error
code, you will find that there is no syntax error at all. **But why it
always shows us the error on this string?**

![image](https://user-images.githubusercontent.com/9413601/98322286-0c2a2e80-2022-11eb-8333-362c51bbf1bb.png)

Therefore, let us continue to look for possible errors in the resource
file. A place that is most likely to cause this problem comes into
view.

![image](https://user-images.githubusercontent.com/9413601/98322461-6b883e80-2022-11eb-9c7a-732bc48206da.png)

We see here that the code page of the resource will be set to
[936](https://www.wikiwand.com/en/Code_page_936), but our current resource file
is UTF-8 encoded, here is very likely to cause the resource compiler to
use the wrong code page to read the content, and eventually cause this
error.

So let us comment this line of code page setting:

![image](https://user-images.githubusercontent.com/9413601/98323261-5f04e580-2024-11eb-83ec-00a396a38cd5.png)

and recompile the project again:

![image](https://user-images.githubusercontent.com/9413601/98323441-b99e4180-2024-11eb-8500-7ae677d92f18.png)

Wow! What an exciting moment, isn't it?

## Conclusion

Now we know that this error is caused by the code page setting does not
match the actual file character encoding, **so we need to pay special
attention to this problem, especially when you are compiling a project
written on different language of operating system**.
