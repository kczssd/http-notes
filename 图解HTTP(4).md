## 图解HTTP(4)

### HTTP报文首部

---

> 请求报文

```http
GET / HTTP/1.1
Host:hacker.jp
User-Agent:"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.150 Safari/537.36 Edg/88.0.705.63"
Accpet:text/heml,application/xhtml+xml,application/xml;q=0.9
Accpet-Language:ja,en-us
Accept-Encoding:gzip,deflate
...
```

1. 通用首部字段(请求和响应都会使用)

   ​	

   |     首部字段      |            说明            |
   | :---------------: | :------------------------: |
   |   Cache-Control   |       控制缓存的行为       |
   |    Connection     |    逐跳首部、连接的管理    |
   |       Date        |     创建报文的日期时间     |
   |      Pragma       |          报文指令          |
   |      Trailer      |     报文末端的首部一览     |
   | Transfer-Encoding | 指定报文主体的传输编码方式 |
   |      Upgrade      |       升级为其他协议       |
   |        Via        |       代理服务器相关       |
   |      Warning      |          错误通知          |

2. 请求首部字段

   |     首部字段名      |                   说明                    |
   | :-----------------: | :---------------------------------------: |
   |       Accept        |           用户可处理的媒体类型            |
   |   Accept-Charset    |               优先的字符集                |
   |   Accept-Encoding   |              优先的内容编码               |
   |   Accept-Language   |                优先的语言                 |
   |    Authorization    |                Web认证信息                |
   |       Expect        |           期待服务器的特定行为            |
   |        From         |               用户email地址               |
   |        Host         |            请求资源所在服务器             |
   |      If-Match       |               比较实体标记                |
   |  If-Modified-Since  |            比较资源的更新时间             |
   |      If-Range       |        比较实体标记与If-Match相反         |
   | If-Unmodified-Since | 比较资源的更新时间与If-Modified-Since相反 |
   |    Max-Forwards     |              最大传输逐跳数               |
   | Proxy-Authorization |      代理服务器要求客户端的认证信息       |
   |        Range        |            实体的字节范围请求             |
   |       Referer       |          对请求中URI的原始获取方          |
   |         TE          |             传输编码的优先级              |
   |     User-Agent      |              HTTP客户端程序               |

---

> 响应报文

```http
HTTP/1.1 304 Not Modified
Date:Thu, 07 Jun 2021 07:21:33 GMT
Server:Apache
Connection:close
...
```

3. 响应首部字段

   |     首部字段名     |             说明             |
   | :----------------: | :--------------------------: |
   |   Accept-Ranges    |     是否接收字节范围请求     |
   |        Age         |     推算资源创建经过时间     |
   |        ETag        |        资源的匹配信息        |
   |      Location      |  令客户端重定向至指定的URI   |
   | Proxy-Authenticate | 代理服务器对客户端的认证信息 |
   |    Retry-After     |   对再次发起请求的时机要求   |
   |       Server       |     HTTP服务器的安装信息     |
   |        Vary        |   代理服务器缓存的管理信息   |
   |  WWW-Authenticate  |   服务器对客户端的认证信息   |

4. 实体首部字段

   | 首部字段名       | 说明                   |
   | ---------------- | ---------------------- |
   | Allow            | 资源可支持的HTTP方法   |
   | Content-Encoding | 实体主体适用的编码方式 |
   | Content-Language | 实体主体的自然语言     |
   | Content-Length   | 实体主体的大小         |
   | Content-Location | 替代对应资源的URI      |
   | Content-MD5      | 实体主体的报文摘要     |
   | Content-Range    | 实体主体的位置范围     |
   | Content-Type     | 实体主体的媒体类型     |
   | Expires          | 实体主体过期的日期时间 |
   | Last-Modified    | 资源的最后修改日期时间 |

5. 其他

   Cookie、Set-Cookie、Content-Disposition

   * Cookie--服务器接受到的Cookie信息
   * Set-Cookie--开始状态管理所使用的Cookie信息
     * name姓名
     * exprires有效期(默认为浏览器关闭为止)
     * path将服务器上的文件目录作为Cookie的适用对象
     * domain作为Cookie适用对象的域名
     * Secure仅在HTTPS通信时才会发送Cookie
     * **HttpOnly使Cookie不能被JavaScript脚本访问**

> HTTP首部字段分为端到端首部、逐跳首部两种。前者会转发给请求/响应对应的最终接收目标，后者只对单次转发有效。

