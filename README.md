# network 学习笔记

## 1. 网站登录逻辑的进化 http=>cookie=>session=>JWT token

http是无状态服务，每次客户端向服务器都要重新发送用户名和密码。

cookie, 服务器校验过客户端第一次发过来的账号密码之后，把账号密码信息返还给浏览器，以key、value的形式存在浏览器的cookie里，下次用户不用再输入用户名和密码，浏览器会自动将cookie里的信息包含在请求头中发给服务器，用户名和密码明文存在cookie中不安全。

session，为了解决cookie的安全问题，会在服务器端为每个登录客户端创建一个session，把客户的账号信息存在服务器session端，把session id返回给浏览器客户端，浏览器下次访问服务器只需要利用存在cookie中的session id就可告知服务器登录用户是谁。海量用户时，session会给服务器造成负荷。

JWT token, JWT规定了数据传输的结构，一串完整的JWT由三段落组成，每个段落用英文句号连接（.）连接，他们分别是：Header、Payload、Signature，所以，常规的JWT内容格式是这样的：AAA.BBB.CCC
Header包含加密的方式、type, payload包含实际传递的参数内容,signature主要决定了Header、Payload有没有被人篡改

## 2. 数字证书
https://www.bilibili.com/video/BV1af4y1u76i/?vd_source=2384206e0cca974945c9ce5d1cb7fbd0

个人生成公钥私钥，文件用哈希算法得到哈希值。个人用私钥对哈希值加密。对方用公钥对哈希值解密，并比对与文件用哈希算法得到的哈希值是否一致。

CA机构会在电脑或手机中预装他们的根证书，根证书包含CA机构信息及其公钥，CA机构用CA的私钥将个人信息和个人公钥加密，对方用CA根证书可以将个人的数字证书解密为个人的身份信息和个人公钥。