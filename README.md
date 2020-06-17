# 《HTTP 权威指南》

> 这个笔记目的是精简整理书中知识，方便查询回顾 ——不忘初心，方得始终

《HTTP: The Definitive Guide》

> [dɪˈfɪnətɪv]

HTTP 是在万维网上进行通信时所使用的协议方案，它有很多应用，最著名的是用于 Web 浏览器和 Web 服务器之间的双工通信。

> **双工通信**：在同一时刻信息可以进行双向传输，例如打电话时既能说又能听

本书将 HTTP 中一些互相关联且常被误解的规则梳理清楚，并编写了一系列基于各种主题的章节介绍 HTTP 各方面的特性，对 HTTP “为什么”这样做进行了详细的解释，而不仅仅停留在它是“怎么做”的。

1. [HTTP：Web 的基础](./part1.md)
   1. [第 1 章 HTTP 概述](./chapter1.md)
   2. 第 2 章，URL
   3. 第 3 章，HTTP 报文
   4. 第 4 章，HTTP 链接管理
2. HTTP 结构
   1. 第 5 章，Web 服务器结构
   2. 第 6 章，HTTP 代理服务器
   3. 第 7 章，Web 缓存
   4. 第 8 章，网管与应用服务器
   5. 第 9 章，Web 上的客户端
   6. 第 10 章，HTTP-NG 协议
3. 识别、认证与安全
   1. 第 11 章，识别用户
   2. 第 12 章，验证用户
   3. 第 13 章，摘要认证
   4. 第 14 章，密码体系、数字证书、SSL
4. 实体、编码和国际化
   1. 第 15 章，HTTP 内容的结构
   2. 第 16 章，Web 标准
   3. 第 17 章，协商可接受内容的机制
5. 内容发布与分发
   1. 第 18 章，部署服务器及 HTTP 对虚拟网站托管的支持
   2. 第 19 章，创建 Web 内容并装载到 Web 服务器的技术
   3. 第 20 章，Web 流量分流
   4. 第 21 章，日志格式
6. [附录](./appendix.md)
   1. A，URI 方案支持的协议
   2. B，HTTP 响应代码
   3. C，HTTP 首部字段参考
   4. [D，MIME 类型](./appendix-d.md)
   5. E，Base-64 编码
   6. F，实现 HTTP 中的各种认证方案
   7. G，HTTP 首部的语言标签值
   8. H，支持国际化 HTTP 的字符编码

TODO

- [x] 添加 gitbook
- [x] 附录 D 链接
  - [x] part 1 1.3 MIME
- [ ] 附录 D 表格使用文字识别转换成文字，方便查询和查看