<h1 align="center">第 3 章 HTTP 报文</h1>

HTTP 报文就是 HTTP 用来传递信息的包裹

---

## 报文流

HTTP 报文是在 HTTP 应用程序之间发送的数据块，它以文本形式的描述报文内容及含义的元信息（meta-information）开头，后面跟着可选的数据。

报文在客户端、服务器、代理之间流动，“流入”、“流出”、“上游”、“下游”都是用来描述报文方向的

### 报文流入源端服务器

流入（inbound）和流出（outbound）是描述事务处理（transaction）方向的，报文流入源端服务器，从服务器流出向用户的 Agent 代理

![image](https://user-images.githubusercontent.com/37435717/85190454-37b6b180-b2eb-11ea-8762-b9243384b854.png)

### 所有报文都向下游流动

上游下游只是相对的，报文从发送者向接受者的流动叫向下游（downstream）流动，发送者在接受者的上游（upstream）

对请求报文来说，客户端在服务器的上游；对响应报文来说，客户端在服务器的下游

![image](https://user-images.githubusercontent.com/37435717/85190492-895f3c00-b2eb-11ea-98f7-7ea8d18c3853.png)

## 报文的组成部分

每条报文都包含一条来自客户端的请求，或者一条来自服务器的响应，由对报文进行描述的**起始行（start line）**、包含属性的**首部（header）**块、可选的包含数据的**主体（body）**组成

**起始行和首部**是一行一行的 ASCII 文本。每行都以**一个回车符（ASCII 13）和一个换行符（ASCII 10）结束，这两个字符组成的行终止序列可以写作 CRLF**。不过稳健的应用程序也应该接受以单个换行符作为行的终止的情况。

主体是可选的，可以是文本或二进制数据，或者是空

### 报文的语法

**两类报文**：请求报文（request message）、响应报文（response message）

**请求报文格式**

```
<method> <request-URL> <version>
<headers>

<entity-body>
```

**响应报文格式**

```
<version> <status> <reason-phrase>
<headers>

<entity-body>
```

- **method 方法**
  - 客户端希望服务器对资源执行的动作，一个单独的词，如 GET、HEAD
- **request-URL 请求 URL**
  - 命名了所请求的资源，或者 URL 路径组件的完整 URL。如果直接与服务器进行通信，那么只要是绝对路径就行了——服务器会假定自己是 URL 的主机/端口
- **version 版本**
  - 报文所使用的 HTTP 版本，样式：`HTTP/<major>.<minor>`
  - 主版本号（major）和次版本号（minor）都是整数
- **status-code 状态码**
  - 描述请求过程中发生情况的三位数字
  - 第一位数字用于描述状态的一般类别，如成功、出错等
- **reason-phrase 原因短语**
  - 数字状态码的可读版，包含**行终止学列之前的所有文本**，只对人类有意义，程序应该根据状态码去判断
- **header 首部**
  - 可以有**零或多个首部**，**每一行都是一个首部**
  - 首部结构：一个名字，一个 `:`，可选的空格，一个值，一个 CRLF
  - 整个首部区域是以一个 CRLF 结尾的，标志着首部的结束以及主体的开始
  - **某些 HTTP 版本（如 HTTP/1.1）要求有效的请求或响应报文中必须包含特定的首部**
  - 即使没有实体，首部也**应该**以一个空行（一个 CRLF）结束，但客户端和服务器都应该考虑那种最后没有 CRLF 的情况
- **entity-body 实体的主体部分**
  - 由任意数据组成的数据块
  - 不是所有报文都包含主体部分

### 起始行

请求的起始行说明要干什么，相应的起始行说明发生了什么

#### 请求行

请求报文的起始行，包含方法、请求 URL、HTTP 的版本，用于告知服务器对哪个资源执行哪种操作，以及客户端使用的 HTTP 版本。这些字段都用空格符分隔。

在 HTTP/1.0 之前，并不要求请求行中包含 HTTP 版本号

#### 响应行

响应报文的起始行，包含响应报文使用的 HTTP 版本、数字状态码、原因短语，都由空格符分隔，在 HTTP/1.0 之前，不要求响应中包含响应行

#### 方法

常用的 HTTP 方法

方 法   | 描 述                                              | 是否包含主体
:-------|:-------------------------------------------------|:-----:
GET     | 从服务器获取一份文档                               |      否
HEAD    | 只从服务器获取文档的首部                           |      否
POST    | 向服务器发送需要处理的数据                         |      是
PUT     | 将请求的主体数据存储在服务器上                     |      是
TRACE   | 对可能经过代理服务器传送到服务器上去的报文进行追踪 |      否
OPTIONS | 决定可以在服务器上执行哪些方法                     |      否
DELETE  | 从服务器上删除一份文档                             |      否

并不是所有服务器都实现了上述 7 种方法，而且某些服务器可能还会实现一些自己的请求方法，称之为**扩展方法**

#### 状态码

状态码位于响应的起始行中，用于告诉客户端发生了什么

状态码的分类

 整体范围 | 已定义范围 | 分 类
:--------:|:----------:|:-----
100 ～ 199 | 100 ～ 101  | 信息提示
200 ～ 299 | 200 ～ 206  | 成功
300 ～ 399 | 300 ～ 305  | 重定向
400 ～ 499 | 400 ～ 415  | 客户端错误
500 ～ 599 | 500 ～ 505  | 服务器错误

#### 原因短语

响应起始行的最后一个组件，对状态码进行文本形式的解释，与状态码成对出现，可以以任何形式出现

#### 版本号

HTTP/x.y，用于告知对方自己遵循的协议版本

### 首部

#### 首部分类

- 通用首部，请求、响应中都有
- 请求首部
- 响应首部
- 实体首部，描述主体的长度或内容或资源自身
- 扩展首部，规范中没有定义的

格式：`<name>:[空格]<value><CRLF>`

如 
```
Accept: image/gif, image/jpeg, text/html
```
说明了客户端可以接受 GIF、JPET 图片和 HTML

#### 首部延续行

将唱的首部分为多行可以提高可读性，多出来的每行前面至少要有一个空格或制表符（tab）

如下面例子，`Server` 首部的值被分成了多个延续行，这个首部的完整值是 `Test Server Version 1.0`

```
HTTP/1.0 200 OK
Content-Type: image/gif
Content-Length: 8588
Server: Test Server
    Version 1.0
```

[附录 C](./appendix-c.md) 提供了所有首部的详细资料