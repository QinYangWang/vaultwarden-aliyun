> 注：当前项目为 Serverless Devs 应用，由于应用中会存在需要初始化才可运行的变量（例如应用部署地区、服务名、函数名等等），所以**不推荐**直接 Clone 本仓库到本地进行部署或直接复制 s.yaml 使用，**强烈推荐**通过 `s init ` 的方法或应用中心进行初始化，详情可参考[部署 & 体验](#部署--体验) 。
# vaultwarden-aliyun 帮助文档

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

基于阿里云函数计算FC一键部署部署Vaultwarden

</description>

## 前期准备

使用该项目，您需要有开通以下服务：

- 函数计算 FC
- 镜像服务
- NAS服务
- VPC服务

推荐您拥有以下的产品权限 / 策略：

- 函数计算 / AliyunFCFullAccess
- 镜像服务 / AliyunContainerRegistryFullAccess
- NAS服务 / AliyunNASFullAccess
- VPC服务 / AliyunVPCFullAccess


## 应用中心一键部署

通过 [Serverless 应用中心](https://fcnext.console.aliyun.com/applications/create?template=vaultwarden-aliyun) ，点击下面按钮直接部署体验：

[![Deploy with Severless Devs](https://img.alicdn.com/imgextra/i1/O1CN01w5RFbX1v45s8TIXPz_!!6000000006118-55-tps-95-28.svg)](https://fcnext.console.aliyun.com/applications/create?template=vaultwarden-aliyun)

## Serverless Devs Cli 部署

1. [安装 Serverless Devs Cli 开发者工具](https://www.serverless-devs.com/serverless-devs/install) ，并进行[授权信息配置](https://docs.serverless-devs.com/fc/config) ； 
2. 初始化项目：`s init vaultwarden-aliyun -d vaultwarden-aliyun `
3. 修改 `s.yaml` 中 `environmentVariables`，部分可选的环境变量：

    ```
    SIGNUPS_ALLOWED=true # 是否允许账户注册
    ADMIN_TOKEN=therandomstring # 管理员访问API的token
    SMTP_HOST=email-smtp.us-west-2.amazonaws.com # SMTP服务器主机地址
    SMTP_FROM=no-reply@example.com # 管理员姓名 
    SMTP_FROM_EMAIL=example@example.com # 管理员邮箱
    SMTP_USERNAME=your-smtp-username # SMTP服务器用户名
    SMTP_PASSWORD=your-smtp-password # SMTP服务器密码
    ```

4. 进入项目，并进行项目部署：`cd vaultwarden-aliyun && s deploy - y`

## 使用文档

<usedetail id="flushContent">

部署完成之后，获得一个域名，可以通过此域名访问vaultwarden服务。

</usedetail>


