<div align=center> <img src="https://s2.loli.net/2024/01/17/vGWJMQilRyt6ko1.png" width="100%"/> </div>

<p align="center">
  <span><b>VaultWarden Serverless Devs</b></span><br>
</p>

<p align="center" class="flex justify-center">
    <a href="https://www.serverless-devs.com" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=vaultwarden-aliyun&type=packageType">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=vaultwarden-aliyun" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=vaultwarden-aliyun&type=packageVersion">
  </a>
  <a href="http://www.devsapp.cn/details.html?name=vaultwarden-aliyun" class="ml-1">
    <img src="http://editor.devsapp.cn/icon?package=vaultwarden-aliyun&type=packageDownload">
  </a>
</p>

<description>

本项目是基于阿里云函数计算 FC 和 Serverless Devs 一键部署 VaultWarden ，Serverless Devs 是一个开源开放的 Serverless 开发者平台，致力于为开发者提供强大的工具链体系。通过该平台，开发者不仅可以一键体验多云 Serverless 产品，极速部署 Serverless 项目，还可以在 Serverless 应用全生命周期进行项目的管理，并且非常简单快速的将 Serverless Devs 与其他工具/平台进行结合，进一步提升研发、运维效能。

</description>

## 前提条件

在使用该项目之前，您需要确保已经开通以下服务：

- [函数计算服务](https://common-buy.aliyun.com/package?planCode=package_freetierfc_cn)
- [容器镜像服务](https://cr.console.aliyun.com/cn-hongkong/instances)
- [文件存储服务](https://nasnext.console.aliyun.com/)
- [专有网络服务](https://common-buy.aliyun.com/?commodityCode=vpc)

开通容器镜像服务具体步骤：

1. 登录[容器镜像服务控制台](https://cr.console.aliyun.com/?spm=a2c4g.11186623.0.0.53a47b17eCUOUy)。
2. 在顶部菜单栏，选择所需**地域**，在左侧导航栏，选择**实例列表**。
3. 在实例列表页面单击目标**个人版实例**，如有需要请选择创建**个人版实例**。
4. 在个人版实例管理页面选择**仓库管理** > **命名空间**。
5. 在命名空间页面单击**创建命名空间**。
6. 在创建命名空间对话框中设置命名空间名称单击确定。
7. 将新创建的命名空间的**默认仓库类型**设为**私有**并启用**自动创建仓库**选项。
  
部署时需要以下的产品权限 / 策略：

- 函数计算服务 / AliyunFCFullAccess
- 容器镜像服务 / AliyunContainerRegistryFullAccess
- 文件存储服务 / AliyunNASFullAccess
- 专有网络服务 / AliyunVPCFullAccess

除此之外，你还需要下面几样产品：

- 一个域名
- 域名对应的 SSL 证书

## 应用中心一键部署

1. 通过 [Serverless 应用中心](https://fcnext.console.aliyun.com/applications/create?template=vaultwarden-aliyun) ，点击下面按钮直接部署体验：

    [![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun.com/applications/create?template=vaultwarden-aliyun)

2. 进入到创建应用页面后，**部署类型**可以选择**直接部署**，这样可以省去创建代码仓库的步骤。

    ![direct-deployment.png](https://s2.loli.net/2024/01/17/5jhqH73lAIpYDkU.png)

3. 部署时**高级配置**需要提供如下参数：

    - 地域：选择服务所部署的区域，由于大陆部署的自定义域名需要备案，因此更推荐部署在国外区域，默认中国香港
    - 数据库地址：如果使用其他数据库实例请提供数据库连接 url，此参数支持 MySQL、PostgreSQL 和 SQLite，默认/mnt/auto/db.sqlite3
    - 镜像仓库命名空间：前提条件中所创建的容器镜像服务命名空间，用来存储 VaultWarden 的镜像。

    ![advanced-configuration.png](https://s2.loli.net/2024/01/17/mJdV6MEer3HNYxZ.png)

4. 单击**创建并部署默认环境**，并在温馨提示窗口选择**继续创建**，然后等待环境创建，部署时间可能会有点长，需要等待一段时间。
  
    ![wait-for-the-environment-to-be-created.png](https://s2.loli.net/2024/01/17/eZMfyiwoABdQOnj.png)

    > 💡部署完成后会提供 serverless-devs 的测试域名作为自定义域名，此域名不支持 HTTPS 且随时可能会被收回，推荐参考绑定个人域名章节重新设置自定义域名。

## 绑定个人域名

1. 登录[函数计算控制台](https://fcnext.console.aliyun.com/overview)。
2. 在左侧菜单栏选择**高级功能** > **域名管理**。
3. 在顶部菜单栏，选择所需**地域**，在**域名管理**页面选择**添加自定义域名**。
   ![custom-domain.png](https://s2.loli.net/2024/01/17/5Chw9H3L7KBaRWU.png)
4. 在**添加自定义域名**页面配置如下参数：
   - 域名：填写个人域名地址，如 `vaultwarden.mydomain.com`
   - 公网 CNAME：将上面填写的域名对应的 DNS 添加此处提供的 CNAME
   - HTTPS：选择**启用**，并勾选**强制 HTTPS**
   - 证书类型：如果是阿里云平台的域名可以去[SSL证书管理](https://yundun.console.aliyun.com/?p=cas#/certExtend/free/cn-hangzhou)申请免费证书，如果是其他平台则需要手动上传申请的证书文件
   - TLS 协议版本：选择**支持 TLS1.2 及以上版本，兼容性较好，安全性最高**
   - 加密套件：选择**全部加密套件，兼容性较高，安全性较低**
   - CDN 加速：选择**禁用**
   - 路由配置：路径保持默认，服务名称选择刚刚创建的服务，函数名称选择**vaultwarden-function**，版本或别名选择**LATEST**，重写策略**未配置**
  ![custom-domain-config.png](https://s2.loli.net/2024/01/17/Jh6wTlO3Nynbsiq.png)
5. 点击**创建**，然后就可以使用 `https://vaultwarden.mydomain.com` 访问服务了