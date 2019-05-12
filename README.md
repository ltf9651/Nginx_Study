# Nginx_Study
Systematic learning about nginx

```sh
// 平滑重载
> nginx -s reload

// 热部署，新Master处理新进程
> kill -USR2 13164
// 优雅退出老进程
> kill -WINCH 13164


// 日志切割
> mv access.log access_bak.log
> nginx -s reopen access.log
```


GoAccess 日志分析工具


SSL/TLS 在表示层进行数据安全加密（密钥交换、身份验证、对称加密、签名hash）


- 对称加密
    - 同一把密钥进行加解密
    - 性能较高
- 非对称加密
    - 公钥加密，私钥解密

- TLS通信过程
  - 验证身份
  - 达成安全套件共识
  - 传递密钥
  - 加密通讯

### 架构基础
Nginx 请求处理流程
![](https://github.com/ltf9651/Nginx_Study/blob/master/image/1.png)


Nginx 多进程结构
![](https://github.com/ltf9651/Nginx_Study/blob/master/image/2.png)

- 不使用多线程：多线程共享同一地址空间，不能保证高可用
- Master 管理、监控 Worker进程和 Cache manager，
- Woker 进程处理真正请求
- 缓存被 Woker, Cache manager, Cache loader 使用
- 进程间使用共享内存进行通讯
- Woker 进程数与CPU数量一致，并将每一个Woker进程与某一个CPU核进行绑定，可以更好地使用CPU缓存