# YAPI

## 简介

YApi 是**高效**、**易用**、**功能强大**的 api 管理平台，旨在为开发、产品、测试人员提供更优雅的接口管理服务。可以帮助开发者轻松创建、发布、维护 API。给用户提供了优秀的交互体验，开发人员只需利用平台提供的接口数据写入工具以及简单的点击操作就可以实现接口的管理。

**流程图**

![yapi-base-flow](.\YAPI\yapi-base-flow.jpg)

## 环境要求

- nodejs（7.6+)
- mongodb（2.6+）
- git

## 部署

1. 全局安装yapi的基础环境

```bash
# YAPI 核心服务
npm i yapi-cli -g --registry https://registry.npm.taobao.org
# YAPI 打包服务（可选）
npm i ykit -g --registry https://registry.npm.taobao.org
```

2. 切换到想要安装的目录，使用cmd打开，安装yapi服务

```bash
yapi server
```

3. 根据安装指示会引到安装页面，在网页进行安装。
   - 记得修改版本号。原装版本大概率报错
   - 注意 nodejs 版本，版本太高会部署失败
   - 安装太慢，记得右键一下cmd

4. 部署成功后，可以关掉之前的所有终端，在安装yapi的目录新开cmd并运行

```bash
# 方法一：简单使用，在此即可运行使用了。
node vendors/server/app.js


# 方法二：（使用版本控制启动）(强烈推荐，可以后台运行)
npm install pm2 -g --registry https://registry.npm.taobao.org # 安装pm2
pm2 start "vendors/server/app.js" --name yapi # pm2管理yapi服务
pm2 info yapi # 查看服务信息
pm2 stop yapi # 停止服务
pm2 restart yapi # 重启服务
```

（后续）升级

```bash
cd  {项目目录}
yapi ls //查看版本号列表
yapi update //更新到最新版本
yapi update -v {Version} //更新到指定版本
```



## 基本操作

### mock操作

## 插件

### [自动获取鉴权token](https://github.com/shouldnotappearcalm/yapi-plugin-interface-oauth2-token)

1. 在项目界面进行安装

```bash
yapi plugin --name yapi-plugin-interface-oauth2-token
```

2. 进入YAPI设置页面进行配置

- 环境名称： 对应环境配置的列表
- 获取 `token` 的地址： 获取 token 的地址，可以是 `GET` 请求或者是 `POST` 请求
- `token` 有效小时： 我会以定时任务的方式重新获取 `token`
- 请求头字段： 将获取到的结果放入这个环境的哪个 `Header` 字段，比如我这里选择了 `Authorization`，将会把获取到的 `token` 保存到这个属性里
- 获取路径
  - 比如你要获取请求体里面的内容，就是 `data.xxx`，记得以 `data` 开头获取请求体内容
  - 如果是获取 `header` 的内容请使用 `header.yyy`，可以使用 `+` 作为连接符
  - 获取返回结果中的内容请使用 `body.xxx`

3. **重启YAPI项目**
