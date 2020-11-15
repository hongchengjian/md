# HTTP

## HTTP 1.0

## HTTP 1.X

## HTTP 2.0 VS HTTP 1.X

```
HTTP1.X解析是Text，HTTP 2.0是只认Binary Format
Server Push
Header 压缩
多路复用
```



## HTTP VS HTTPS



 

## HTTP 状态码

```css
1 消息
▪ 100 Continue
▪ 101 Switching Protocols
▪ 102 Processing
2 成功
▪ 200 OK
▪ 201 Created
▪ 202 Accepted
▪ 203 Non-Authoritative Information
▪ 204 No Content
▪ 205 Reset Content
▪ 206 Partial Content
▪ 207 Multi-Status
3 重定向
▪ 300 Multiple Choices
▪ 301 Moved Permanently
▪ 302 Move Temporarily
▪ 303 See Other
▪ 304 Not Modified
▪ 305 Use Proxy
▪ 306 Switch Proxy
▪ 307 Temporary Redirect
4 请求错误 (前端发了，服务器未收到、服务器不接受、服务器不理解)
▪ 400 Bad Request
▪ 401 Unauthorized
▪ 402 Payment Required
▪ 403 Forbidden
▪ 404 Not Found
▪ 405 Method Not Allowed
▪ 406 Not Acceptable
▪ 407 Proxy Authentication Required
▪ 408 Request Timeout
▪ 409 Conflict
▪ 410 Gone
▪ 411 Length Required
▪ 412 Precondition Failed
▪ 413 Request Entity Too Large
▪ 414 Request-URI Too Long
▪ 415 Unsupported Media Type
▪ 416 Requested Range Not Satisfiable
▪ 417 Expectation Failed
▪ 418 I'm a teapot
▪ 421Misdirected Request
▪ 422 Unprocessable Entity
▪ 423 Locked
▪ 424 Failed Dependency
▪ 425 Too Early
▪ 426 Upgrade Required
▪ 449 Retry With
▪ 451 Unavailable For Legal Reasons
5 服务器错误 (服务器收到了前端的请求却处理不了)
▪ 500 Internal Server Error
▪ 501 Not Implemented
▪ 502 Bad Gateway
▪ 503 Service Unavailable
▪ 504 Gateway Timeout
▪ 505 HTTP Version Not Supported
▪ 506 Variant Also Negotiates
▪ 507 Insufficient Storage
▪ 509 Bandwidth Limit Exceeded
▪ 510 Not Extended
▪ 600 Unparseable Response Headers
```

## HTTP 扩展

```css
Accept 设置接受的内容类型 Ex. Accept: text/plain

Accept-Charset 设置接受的字符编码 Ex. Accept-Charset: utf-8

Accept-Encoding 设置接受的编码格式 Ex. Accept-Encoding: gzip, deflate  gzip压缩减少网络传输，纯文本大概可压缩至40%

Accept-Datetime 设置接受的版本时间 Ex. Accept-Datetime: Thu, 31 May 2007 20:35:00 GMT

Accept-Language 设置接受的语言 Ex. Accept-Language: en-US

Authorization 设置HTTP身份验证的凭证 Ex. Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ== 若没有使用SSL/TLS传输层安全协议，以明文传输的密钥和口令很容易被拦截。若需使用Basic Authorization，在服务器Response Headers添加access-control-allow-headers:Authorization

Cache-Control 设置请求响应链上所有的缓存机制必须遵守的指令 Ex. Cache-Control: no-cache

Connection 设置当前连接和hop-by-hop协议请求字段列表的控制选项 Ex. Connection: keep-alive、Connection: Upgrade、Connection: closed
HTTP早期，每个HTTP请求都要求打开一个TCP Socket连接，并且使用一次之后就断开这个TCP连接。可以tcpdump -n host <u>www.baidu.com</u> 抓包分析。@See https://www.cnblogs.com/freefish12/p/5394876.html。但从HTTP/1.1起，浏览器都开启了keep-alive，Keep-Alive不会永久保持连接，它有一个被设定的保持时间(Apache可设定)。当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的TCP连接。长连接、长轮询long-polling基于HTTP的长连接，是一种通过长轮询long-polling实现服务器推技术。
    
Upgrade 请求服务端升级协议 Ex. Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket
Connection: Upgrade 表示Upgrade是一个hop-by-hop的字段，是给proxy看的(proxy一般是Nginx)。Upgrade: websocket 表示浏览器想要升级到WebSocket协议，是给最终处理请求程序看的。如果只有Upgrade: websocket，说明proxy不支持websocket升级，按照标准应该视为普通HTTP请求。使用首部字段 Upgrade 时，还需要额外指定 Connection: Upgrade。
hop-by-hop header(逐跳头部)用来描述当前浏览器与直连服务器(Nginx反向代理)的连接信息，默认的hop-by-hop header 有Connection, Keep-Alive, Proxy-Authenticate, Proxy-Authorization, TE, Trailers, Transfer-Encoding, Upgrade @See https://www.yuque.com/devweb/front/ztg8ur

Content-Length 设置请求体的字节长度  Ex. Content-Length: 348

Content-MD5 设置基于MD5算法对请求体内容进行Base64二进制编码 Ex. Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

Content-Type 设置请求体的MIME类型(适用POST和PUT请求) Ex. Content-Type: application/x-www-form-urlencoded、Content-Type: multipart/form-data
Content-Type: multipart/form-data 可同时字段表单提交和Multipart文件上传，不直接先上传图片返回前端url再将url放@RequestBody请求服务端为了防刷上传

Cookie 设置服务器使用Set-Cookie发送的http cookie Ex. Cookie: $Version=1; Skin=new;

Date 设置消息发送的日期和时间 Ex. Date: Tue, 15 Nov 1994 08:12:31 GMT

Expect 标识客户端需要的特殊浏览器行为 Ex. Expect: 100-continue

Forwarded 披露客户端通过http代理连接web服务的源信息

Forwarded: for=192.0.2.60;proto=http;by=203.0.113.43
Forwarded: for=192.0.2.43, for=198.51.100.17

From 设置发送请求的用户的email地址

From: user@example.com

Host 设置服务器域名和TCP端口号，如果使用的是服务请求标准端口号，端口号可以省略

Host: en.wikipedia.org:8080
Host: en.wikipedia.org

If-Match 设置客户端的ETag，当时客户端ETag和服务器生成的ETag一致才执行，适用于更新自从上次更新之后没有改变的资源 Ex. If-Match: "737060cd8c284d8af7ad3082f209582d

If-Modified-Since 设置更新时间，从更新时间到服务端接受请求这段时间内如果资源没有改变，允许服务端返回304 Not Modified Ex. If-Modified-Since: Sat, 29 Oct 1994 19:43:31 GMT

If-None-Match 设置客户端ETag，如果和服务端接受请求生成的ETage相同，允许服务端返回304 Not Modified

If-None-Match: "737060cd8c284d8af7ad3082f209582d"

If-Range 设置客户端ETag，如果和服务端接受请求生成的ETage相同，返回缺失的实体部分；否则返回整个新的实体

If-Range: "737060cd8c284d8af7ad3082f209582d"

If-Unmodified-Since 设置更新时间，只有从更新时间到服务端接受请求这段时间内实体没有改变，服务端才会发送响应

If-Unmodified-Since: Sat, 29 Oct 1994 19:43:31 GMT

Max-Forwards 限制代理或网关转发消息的次数

Max-Forwards: 10

Origin 标识跨域资源请求（请求服务端设置Access-Control-Allow-Origin响应字段）

Origin: http://www.example-social-network.com

Pragma 设置特殊实现字段，可能会对请求响应链有多种影响

Pragma: no-cache

Proxy-Authorization 为连接代理授权认证信息

Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==

Range 请求部分实体，设置请求实体的字节数范围，具体可以参见HTTP/1.1中的Byte serving

Range: bytes=500-999

Referer 设置前一个页面的地址，并且前一个页面中的连接指向当前请求，意思就是如果当前请求是在A页面中发送的，那么referer就是A页面的url地址（轶事：这个单词正确的拼法应该是"referrer",但是在很多规范中都拼成了"referer"，所以这个单词也就成为标准用法）

Referer: http://en.wikipedia.org/wiki/Main_Page

TE 设置用户代理期望接受的传输编码格式，和响应头中的Transfer-Encoding字段一样

TE: trailers, deflate

User-Agent 用户代理的字符串值

User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/21.0

Via 通知服务器代理请求

Via: 1.0 fred, 1.1 example.com (Apache/1.1)

Warning 实体可能会发生的问题的通用警告

Warning: 199 Miscellaneous warning

常用非标准请求头字段
X-Requested-With 标识Ajax请求，大部分js框架发送请求时都会设置它为XMLHttpRequest

X-Requested-With: XMLHttpRequest

DNT 请求web应用禁用用户追踪

DNT: 1 (Do Not Track Enabled)
DNT: 0 (Do Not Track Disabled)

X-Forwarded-For 一个事实标准，用来标识客户端通过HTTP代理或者负载均衡器连接的web服务器的原始IP地址

X-Forwarded-For: client1, proxy1, proxy2
X-Forwarded-For: 129.78.138.66, 129.78.64.103

X-Forwarded-Host 一个事实标准，用来标识客户端在HTTP请求头中请求的原始host,因为主机名或者反向代理的端口可能与处理请求的原始服务器不同

X-Forwarded-Host: en.wikipedia.org:8080
X-Forwarded-Host: en.wikipedia.org

X-Forwarded-Proto 一个事实标准，用来标识HTTP原始协议，因为反向代理或者负载均衡器和web服务器可能使用http,但是请求到反向代理使用的是https

X-Forwarded-Proto: https

Front-End-Https 微软应用程序和负载均衡器使用的非标准header字段 Front-End-Https: on
X-Http-Method-Override 请求web应用时，使用header字段中给定的方法（通常是put或者delete）覆盖请求中指定的方法（通常是post）,如果用户代理或者防火墙不支持直接使用put或者delete方法发送请求时，可以使用这个字段

X-HTTP-Method-Override: DELETE

X-ATT-DeviceId 允许更简单的解析用户代理在AT&T设备上的MakeModel/Firmware

X-Att-Deviceid: GT-P7320/P7320XXLPG

X-Wap-Profile 设置描述当前连接设备的详细信息的xml文件在网络中的位置

x-wap-profile: http://wap.samsungmobile.com/uaprof/SGH-I777.xml

Proxy-Connection 早起HTTP版本中的一个误称，现在使用标准的connection字段

Proxy-Connection: keep-alive

X-UIDH 服务端深度包检测插入的一个唯一ID标识Verizon Wireless的客户

X-UIDH: ...

X-Csrf-Token,X-CSRFToken,X-XSRF-TOKEN 防止跨站请求伪造

X-Csrf-Token: i8XNjC4b8KVok4uw5RftR38Wgp2BFwql

X-Request-ID,X-Correlation-ID 标识客户端和服务端的HTTP请求

X-Request-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5

常用标准响应头字段
Access-Control-Allow-Origin 指定哪些站点可以参与跨站资源共享

Access-Control-Allow-Origin: *

Accept-Patch 指定服务器支持的补丁文档格式，适用于http的patch方法

Accept-Patch: text/example;charset=utf-8

Accept-Ranges 服务器通过byte serving支持的部分内容范围类型

Accept-Ranges: bytes

Age 对象在代理缓存中暂存的秒数

Age: 12

Allow 设置特定资源的有效行为，适用方法不被允许的http 405错误

Allow: GET, HEAD

Alt-Svc 服务器使用"Alt-Svc"（Alternative Servicesde的缩写）头标识资源可以通过不同的网络位置或者不同的网络协议获取

Alt-Svc: h2="http2.example.com:443"; ma=7200

Cache-Control 告诉服务端到客户端所有的缓存机制是否可以缓存这个对象，单位是秒

Cache-Control: max-age=3600

Connection 设置当前连接和hop-by-hop协议请求字段列表的控制选项

Connection: close

Content-Disposition 告诉客户端弹出一个文件下载框，并且可以指定下载文件名

Content-Disposition: attachment; filename="fname.ext"

Content-Encoding 设置数据使用的编码类型

Content-Encoding: gzip

Content-Language 为封闭内容设置自然语言或者目标用户语言

Content-Language: en

Content-Length 响应体的字节长度

Content-Length: 348

Content-Location 设置返回数据的另一个位置

Content-Location: /index.htm

Content-MD5 设置基于MD5算法对响应体内容进行Base64二进制编码

Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==

Content-Range 标识响应体内容属于完整消息体中的那一部分

Content-Range: bytes 21010-47021/47022

Content-Type 设置响应体的MIME类型

Content-Type: text/html; charset=utf-8

Date 设置消息发送的日期和时间

Date: Tue, 15 Nov 1994 08:12:31 GMT

ETag 特定版本资源的标识符，通常是消息摘要

ETag: "737060cd8c284d8af7ad3082f209582d"

Expires 设置响应体的过期时间

Expires: Thu, 01 Dec 1994 16:00:00 GMT

Last-Modified 设置请求对象最后一次的修改日期

Last-Modified: Tue, 15 Nov 1994 12:45:26 GMT

Link 设置与其他资源的类型关系

Link: </feed>; rel="alternate"

Location 在重定向中或者创建新资源时使用

Location: http://www.w3.org/pub/WWW/People.html

P3P 以P3P:CP="your_compact_policy"的格式设置支持P3P(Platform for Privacy Preferences Project)策略，大部分浏览器没有完全支持P3P策略，许多站点设置假的策略内容欺骗支持P3P策略的浏览器以获取第三方cookie的授权

P3P: CP="This is not a P3P policy! See http://www.google.com/support/accounts/bin/answer.py?hl=en&answer=151657 for more info."

Pragma 设置特殊实现字段，可能会对请求响应链有多种影响

Pragma: no-cache

Proxy-Authenticate 设置访问代理的请求权限

Proxy-Authenticate: Basic

Public-Key-Pins 设置站点的授权TLS证书

Public-Key-Pins: max-age=2592000; pin-sha256="E9CZ9INDbd+2eRQozYqqbQ2yXLVKB9+xcprMF+44U1g=";

Refresh "重定向或者新资源创建时使用，在页面的头部有个扩展可以实现相似的功能，并且大部分浏览器都支持
<meta http-equiv="refresh" content="5; url=http://example.com/">

Refresh: 5; url=http://www.w3.org/pub/WWW/People.html

Retry-After 如果实体暂时不可用，可以设置这个值让客户端重试，可以使用时间段（单位是秒）或者HTTP时间

Example 1: Retry-After: 120
Example 2: Retry-After: Fri, 07 Nov 2014 23:59:59 GMT

Server 服务器名称

Server: Apache/2.4.1 (Unix)

Set-Cookie 设置HTTP Cookie

Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1

Status 设置HTTP响应状态

Status: 200 OK

Strict-Transport-Security 一种HSTS策略通知HTTP客户端缓存HTTPS策略多长时间以及是否应用到子域

Strict-Transport-Security: max-age=16070400; includeSubDomains

Trailer 标识给定的header字段将展示在后续的chunked编码的消息中

Trailer: Max-Forwards

Transfer-Encoding 设置传输实体的编码格式，目前支持的格式：chunked, compress, deflate, gzip, identity

Transfer-Encoding: chunked

TSV Tracking Status Value，在响应中设置给DNT(do-not-track),可能的取值
　　　"!" — under construction
　　　"?" — dynamic
　　　"G" — gateway to multiple parties
　　　"N" — not tracking
　　　"T" — tracking
　　　"C" — tracking with consent
　　　"P" — tracking only if consented
　　　"D" — disregarding DNT
　　　"U" — updated

TSV: ?

Upgrade 请求客户端升级协议

Upgrade: HTTP/2.0, HTTPS/1.3, IRC/6.9, RTA/x11, websocket

Vary 通知下级代理如何匹配未来的请求头已让其决定缓存的响应是否可用而不是重新从源主机请求新的

Example 1: Vary: *
Example 2: Vary: Accept-Language

Via 通知客户端代理，通过其要发送什么响应

Via: 1.0 fred, 1.1 example.com (Apache/1.1)

Warning 实体可能会发生的问题的通用警告

Warning: 199 Miscellaneous warning

WWW-Authenticate 标识访问请求实体的身份验证方案

WWW-Authenticate: Basic

X-Frame-Options 点击劫持保护：
　　　deny frame中不渲染
　　　sameorigin 如果源不匹配不渲染
　　　allow-from 允许指定位置访问
　　　allowall 不标准，允许任意位置访问

X-Frame-Options: deny

常用非标准响应头字段
X-XSS-Protection 过滤跨站脚本

X-XSS-Protection: 1; mode=block

Content-Security-Policy, X-Content-Security-Policy,X-WebKit-CSP 定义内容安全策略

X-WebKit-CSP: default-src 'self'

X-Content-Type-Options 唯一的取值是"",阻止IE在响应中嗅探定义的内容格式以外的其他MIME格式

X-Content-Type-Options: nosniff

X-Powered-By 指定支持web应用的技术

X-Powered-By: PHP/5.4.0

X-UA-Compatible 推荐首选的渲染引擎来展示内容，通常向后兼容，也用于激活IE中内嵌chrome框架插件
<meta http-equiv="X-UA-Compatible" content="chrome=1" />

X-UA-Compatible: IE=EmulateIE7
X-UA-Compatible: IE=edge
X-UA-Compatible: Chrome=1

X-Content-Duration 提供音视频的持续时间，单位是秒，只有Gecko内核浏览器支持

X-Content-Duration: 42.666

Upgrade-Insecure-Requests 标识服务器是否可以处理HTTPS协议

Upgrade-Insecure-Requests: 1

X-Request-ID,X-Correlation-ID 标识一个客户端和服务端的请求 Ex. X-Request-ID: f058ebd6-02f7-4d3f-942e-904344e8cde5
```

## TCP 重传、滑动窗口、流量控制、拥塞控制 
