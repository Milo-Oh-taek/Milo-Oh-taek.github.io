---
title: 쿠키가 동작 안할때 확인해야 할 것들 when cookie doesn't work
date: 2022-02-16 22:20:00 +09:00
categories: [WEB]
tags: [web, cookie]
---

#####쿠키가 제대로 작동하지 않을때 체크해야 할 리스트를 정리해 보았다.
##1. withCredentials
>XMLHttpRequest.withCredentials property is a boolean value that indicates     >whether or not cross-site Access-Control requests should be made using      >credentials such as cookies, authorization headers or TLS client            >certificates.

Credendial. 말그대로 자격을 뜻하며 
다른 origin 간에 자격증명(cookie 등을) 전송 할 것인지를 boolean 설정. 
**Client, Server의 withCredentials를 true로 설정하면 쿠키 전송 가능.**

다만, 
>Credential is not supported if the CORS header 'Access-Control-Allow-Origin' is '*'.

**'Access-Control-Allow-Origin' 을 *가 아닌 특정 도메인을 넣어줘야 한다.**

##2. Domain option
>The Domain attribute specifies which hosts can receive a cookie. If unspecified, the attribute defaults to the same host that set the cookie, excluding subdomains. If Domain is specified, then subdomains are always included. Therefore, specifying Domain is less restrictive than omitting it. However, it can be helpful when subdomains need to share information about a user.

**Domain attribute를 설정해야 sub domain에서 쿠키 사용이 가능하다.**
ex) <mark>Domain = myportfolio.com</mark> -> <mark>api.myportfolio.com</mark>에서 access ㅇ

##3. Path option
>The Path attribute indicates a URL path that must exist in the requested URL in order to send the Cookie header. The %x2F ("/") character is considered a directory separator, and subdirectories match as well.

**설정된 경로 및 하위 경로에 있는 페이지에서 접근 가능.**
ex) <mark>Path=/user</mark> -> <mark>/user/login</mark>, <mark>/user/logout</mark>, ...
Path=/ 로 설정할 시 제한 x

##4. SameSite
>The SameSite attribute of the Set-Cookie HTTP response header allows you to declare if your cookie should be restricted to a first-party or same-site context.

쿠키의 공유를 same site로 제한 할 지 설정.
- Lax(Chrome Default)
>Cookies are not sent on normal cross-site subrequests (for example to load images or frames into a third party site), but are sent when a user is navigating to the origin site (i.e., when following a link).
링크를 따라 들어 오는 등의 경로를 제외하고는 다른 도메인 쿠키 접근 불가.

same site의 기준은?
**도메인 접미사와 바로 앞의 도메인 부분이 결합된 것**

<mark>www.web.dev</mark>와  <mark>static.web.dev</mark>은 same site.
<mark>galaxy.github.io</mark>와  <mark>apple.github.io</mark>은 same site X.
>github.io 가 접미사이기 때문이다.
>public suffix list는 따로 문서화 되어있다. (https://publicsuffix.org/list/)


##Reference
- https://web.dev/samesite-cookies-explained/#explicitly-state-cookie-usage-with-the-samesite-attribute
- https://ko.javascript.info/cookie
- https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies






