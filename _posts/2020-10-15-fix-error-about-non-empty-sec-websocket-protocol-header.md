---
layout: post
title: Fix error about non-empty Sec-WebSocket-Protocol header
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - fullstack
  - misc
---

## 1. Introduction

When you encounter this problem about `WebSocket connection to
'wss://<address>/live' failed: Error during WebSocket
handshake: Sent non-empty 'Sec-WebSocket-Protocol' header but
no response was received`, here is an article on how to fix this
problem.

## 2. Review

According to the error message, we know that the WebSocket client
sent a request with non-empty __'Sec-WebSocket-Protocol'__ header as
shown below:

![image](https://user-images.githubusercontent.com/9413601/96110449-77e11600-0f12-11eb-91c2-d75903ded4a8.png)

Therefore, let's find more about the `Sec-WebSocket-Protocol` header
field. And the header field definition can be found in [RFC 6455](https://tools.ietf.org/html/rfc6455#page-59).

> It is used in the WebSocket opening handshake. It is sent from the
client to the server and back from the server to the client to
confirm the subprotocol of the connection.  This enables scripts to
both select a subprotocol and be sure that the server agreed to
serve that subprotocol.

## 3. Conclusion

Now we know that this problem is caused by the backend server not
agreeing to serve the subprotocol (Known by above picture it is
`x-wss`). Therefore, we should add the `Sec-WebSocket-Protocol`
header field to the response in our server side, and the value
should be the same with the client. Otherwise, the connection will
be closed.
