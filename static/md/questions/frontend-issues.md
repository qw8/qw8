---
title: 前端问题
date: 2022-05-19 23:40:25
categories: 
- 前端问题
tags:
- 前端
---

### 本地pnpm版本与packageManager中pnpm版本不一致

问题：ERR_PNPM_BAD_PM_VERSION  This project is configured to use v8.6.10 of pnpm. Your current pnpm is v9.1.0

解决：If you want to bypass this version check, you can set the “package-manager-strict” configuration to “false” or set the “COREPACK_ENABLE_STRICT” environment variable to “0”
在.npmrc中添加

```
package-manager-strict=false
```



### Node16版本 对应node-sass和sass-loader的版本号

```
"node-sass": "6.0.1"
"sass-loader": "10.2.0"
```

改完记得要打开终端重新**npm install**下







# 其他

### 公司vpn才可以访问代码库、流水线，是什么原理

公司内部使用的VPN（虚拟私人网络）是一种安全的技术，它允许员工通过公共网络（如互联网）安全地连接到公司的内部网络。当员工在外部网络环境中工作时，比如在家办公或者出差在外，他们可以通过公司提供的VPN连接回到公司的内网，从而访问内部资源，如代码库、持续集成/持续部署（CI/CD）流水线等敏感信息和系统。

这种做法的主要原理包括：

1. **加密通信**：所有通过VPN传输的数据都会被加密，这确保了数据在传输过程中的安全，防止第三方窃听或篡改数据。

2. **身份验证**：在建立VPN连接前，用户需要通过身份验证机制来证明自己的身份，这通常包括用户名和密码，有时还会结合双因素认证（2FA）等更为严格的身份验证方式。

3. **访问控制**：一旦连接建立，公司可以根据不同的用户或用户组设置不同的访问权限，确保只有授权人员才能访问特定的资源。

4. **私有网络隔离**：即使是在公共网络上，通过VPN创建的连接也像是一个独立的私有网络，可以有效地将公司内部网络与外界隔离开来，保护内部网络不受外部威胁的影响。

通过这些措施，公司能够保证其内部资源的安全性，同时为远程工作的员工提供必要的访问权限。需要注意的是，使用公司提供的合法、合规的VPN服务是保障网络安全和个人信息安全的重要手段。在中国，使用未经批准的VPN服务或翻墙技术可能违反相关法律法规，因此，我们鼓励所有用户遵守国家的相关法律要求，选择合法的服务，保护个人信息安全，共同维护良好的网络环境。