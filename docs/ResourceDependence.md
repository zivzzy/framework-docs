# 依赖

### 框架及功能

| 序号 | 依赖             |  说明                                                      |
| :--: | :---------------------- | :-------------------------------------------------------- |
|  1   | 应用系统监控层-应用埋点    | 可视化埋点/手动埋点/无埋点/埋点SDK/埋点管理                                  |
|  2   | 应用系统监控层-系统管家    | 应用服务器监控/监控指标可视化/性能指标分析/监控数据采集/预警管理                 |
|  3   | 应用接入层-应用接入 | 应用定制/登录页定制/主题定制/租户定制               |
|  4   | 应用接入层-低代码 | 报表平台/可视化平台/表单设计器/仪表盘设计器 |
|  5   | 应用接入层-容器化      | docker/Kubernetes/rancher/kubesphere                                 |
|  6   | 应用接入层-应用网关  | nginx/openresty/灰度发布                 |

## 低代码

| 序号 | 分类           | 依赖模块名              | 是否必要 | 说明                                                      |
| :--: | :------------- | :---------------------- | :------- | :-------------------------------------------------------- |
|  1   | fedx-framework | web-config(配置中心)    | 必要     | 用于处理客户端微服务配置                                  |
|  2   | fedx-framework | service-config          | 必要     | web-config node 服务                                      |
|  3   | fedx-framework | web-framework(基础应用) | 非必要   | 需要登录页及入口菜单时，需要部署,非必要依赖               |
|  4   | fedx-framework | oss-material (素材中心) | 必要     | 需要自行维护图片等素材时,必须部署,仅发布大屏时,不需要部署 |
|  5   | fedx-framework | web-theme(主题定制)     | 非必要   | 自定义平台主题,非必要依赖                                 |
|  6   | fedx-framework | web-security(权限管理)  | 非必要   | 需要登录及入口菜单时，需要部署,非必要依赖                 |
|  7   | fedx-framework | service-security        | 非必要   | web-security node 服务                                    |
|  8   | fedx-framework | service-framework       | 必要     | fedx-framework node 服务                                  |
|  9   | fedx-bff-web   | plugin-midwayjs         | 必要     | node 服务基础依赖                                         |
|  10  | fedx-bff-web   | monorepo-package        | 必要     | node 服务基础依赖                                         |
|  11  | fedx-bff-web   | core                    | 必要     | node 服务基础依赖                                         |
|  12  | fedx-bff-web   | plugin-midwayjs         | 必要     | node 服务基础依赖                                         |
|  13  | fedx-bff-web   | plugin-react            | 必要     | node 服务基础依赖                                         |
|  14  | fedx-bff-web   | utils                   | 必要     | node 服务基础依赖                                         |
|  15  | 数据服务       | data-center (数据中心)  | 必要     | 低代码平台数据源                                          |
|  16  | 数据服务       | data-center-services    | 必要     | data-center node 服务                                     |
