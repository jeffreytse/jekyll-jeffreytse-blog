---
layout: post
title: Email Server Ports Table
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - email
  - misc
---

## Table

Here’s a table of the email server ports.

| Ports | Protocal | Security    | Authentication   | Description       |
| ----- | -------- | ----------- | ---------------- | ----------------- |
| 25    | SMTP     | None        | AUTH             | Outgoing Messages |
| 587   | SMTP     | None or TLS | STARTTLS         | Outgoing Messages |
| 465   | SMTP     | SSL         | SSL              | Outgoing Messages |
| 143   | IMAP     | None or TLS | AUTH or STARTTLS | Incoming Messages |
| 993   | IMAP     | SSL         | SSL              | Incoming Messages |
| 110   | POP3     | None        | AUTH             | Incoming Messages |
| 995   | POP3     | SSL         | SSL              | Incoming Messages |

- **SMTP** - The Simple Mail Transfer Protocol (SMTP) is for electronic
  mail transmission. User-level email clients typically use SMTP only
  for sending messages to a mail server for relaying.
- **IMAP** - The Internet Message Access Protocol (IMAP) is an Internet
  standard protocol used by email clients to retrieve email messages
  from a mail server over a TCP/IP connection.
- **POP3** - The Post Office Protocol (POP) is an application-layer
  Internet standard protocol used by e-mail clients to retrieve e-mail
  from a mail server.

## What is the difference between POP3 and IMAP?

There are two possibilities for retrieving emails:

**IMAP:** Emails are synchronized between your computer and the email
server. Furthermore, you can create your own folders on the server in
order to sort or move your messages. These will then be available to
you worldwide and on multiple devices.

**POP3:** Emails are "retrieved" from your computer and deleted by the
server in the default setting. Due to this, you no longer have access
to these messages. There is also no possibility to create folders on
the server and to use these synchronously with several devices.

**In summary:**

- If you use your email account **with several devices** and you would
  like to use your own folders, we recommend using IMAP.
- If you **only use one device** for email access, **access through
  POP3** is normally sufficient.

## References

- [A List of SMTP and POP3 Server](https://www.arclab.com/en/kb/email/list-of-smtp-and-pop3-servers-mailserver-list.html)
- [A List of SMTP and IMAP Server](https://www.arclab.com/en/kb/email/list-of-smtp-and-imap-servers-mailserver-list.html)
- [What is IMAP and how can I use it?](https://www.strato.com/faq/en_us/product/what-is-imap-and-how-can-i-use-it/)
