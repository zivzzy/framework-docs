# 核心配置

### 框架配置说明  

```json
{
  "appId": 110002,
  "prefixCls": "oss-ui",
  "siderWidth": 250, // mix和side模式侧边菜单宽度
  "navTheme": "dark", // 菜单主题 可选dark和light
  /* 主题设置 */
  "themeConfig": {
    "theme": "light", // 默认主题色
    "showThemeSelector": true, // 是否展示主题切换器
    /* 主题切换列表 */
    "themeList": [
      { "key": "light", "name": "浅色主题" },
      { "key": "darkblue", "name": "深蓝主题" },
      { "key": "dark", "name": "暗黑主题" }
    ]
  },
  "layout": "top", // 布局模式 可选项为'top','side','mix','card','cardNav'
  "contentWidth": "Fluid",
  "fixedHeader": true,
  "fixSiderbar": true,
  "menu": { "locale": true, "defaultOpenAll": false },
  "headerHeight": 52, // 菜单栏高度
  "headerFontSize": 12, // 菜单栏文字尺寸
  "title": "故障管理中心", // 项目标题
  "description": "测试描述测试描述",
  "iconfontUrl": "", // iconfont路径
  "logo": "/images/default-logo.jpg", // logo路径
  "logoMin": "/images/default-logo-min.png", // 折叠后的小logo路径
  "logoStyle": {}, // logo的样式
  "logoTitleColor": "", // logo文字的颜色
  "defaultUrl": "/",
  "welcomeImageUrl": "/images/welcomeAndError/welcome.png", // 欢迎页图片路径
  /* 自定义欢迎页配置 */
  "welcomePageConfig": {
    "enable": false, // 是否启用
    "entry": "http://localhost:9005/security/power-admin-manage", // entry路径（不可以是主应用的路径）,需为完整路径，如果值存在则protocol、hostname、port、path均失效
    "module": "oss-security-manager", // module （必填）
    "curRoute": "/security/power-admin-manage", // 当前路由（和path二选一必填）
    "protocol": "http:", // 协议
    "hostname": "localhost", // 域名
    "port": 3000, // 端口
    "path": "/data-center/data-object-management" // 路径（和curRoute二选一必填）
  },
  /* 鉴权配置 */
  "authorizeConfig": {
    "authorize": true, // 是否启用鉴权
    "authorizeUrl": "http://10.12.2.187:7001", // 鉴权路径
    "ssoUrl": "http://10.12.2.187:9011/ssoUrl", // 登录地址
    "timeout": 20000, // 超时时间
    "anonymousUrls": [],
    "refreshTime": 600000, // 刷新token时间间隔
    "clientId": "oss-framework",
    "clientSecret": "boco",
    /* 第三方登出接口配置 */
    "externalLogout": {
      "externalLogoutUrl": "xxx/token/blacklist",
      "params": {
        "exp": "${timestamp}",
        "jti": "${thirdpart_access_token}"
      },
      "method": "post"
    },
    "confirmBeforeLogout": false // 退出登录确认提示
  },
  /* 日志设置 */
  "logConfig": {
    "logUrl": "http://10.12.2.187:7001",
    "level": "debug"
  },
  /* 菜单配置 */
  "contextmenuConfig": {
    "menuUrl": "contextmenu.json"
  },
  "maxTabsCount": 15, // 最大tab页数量
  /* 菜单栏按钮配置 */
  "actionConfig": {
    /* 工具栏配置 */
    "toolbarConfigs": [
      {
        "key": "help",
        "title": "使用文档",
        "actionMode": "blank",
        "entry": "https://www.baidu.com",
        "icon": "QuestionCircleOutlined",
        "isShow": false,
        "params": {}
      }
    ],
    /* 消息中心配置 */
    "noticeConfig": {
      "isShowNotice": true,
      "noticeWsUrl": "ws://10.10.2.8:7006",
      "noticeUrl": "http://10.10.2.8:7006",
      /* 消息类型配置 */
      "noticeList": [
        {
          "key": "notification",
          "title": "通知",
          "emptyText": "你已查看所有通知"
        },
        {
          "key": "message",
          "title": "消息",
          "emptyText": "你已读完所有消息"
        },
        {
          "key": "event",
          "title": "待办",
          "emptyText": "你已完成所有待办"
        }
      ]
    },
    /* 全屏配置 */
    "fullScreenConfig": {
      "isShowFullScreen": true // 是否展示全屏按钮
    },
    /* 头像下拉框按钮栏配置 */
    "menubarConfigs": [
      {
        "key": "ruleAdmin",
        "title": "关联规则管理后台",
        "actionMode": "self",
        "entry": "/?appId=12301",
        "icon": "HomeOutlined",
        "isShow": true,
        "params": {}
      }
    ]
  },
  "entryPagePath": "", // 登录默认打开路径（优先级高于欢迎页和自定义欢迎页）
  "useMenuManage": false, // 是否使用菜单管理
  "showVersion": true, // 是否开启版本更新提示
  /* 记录在线状态接口设置 */
  "recordOnlineTime": {
    "enable": false, // 启用
    "timeout": 10000, // 接口调用间隔
    "onlineUrl": "http://xxx.aaa/bbb", // 接口地址
    "method": "get" // 接口类型
  },
  "userSettingConfig": {
    "hideModifyPassword": false // 隐藏修改密码页面
  }
}
```

### 集中配置
- 可通过集中配置平台，快速配置、管理各应用的配置文件，实现统一配置、统一管理

<img src="https://flyfedx.github.io/framework-docs/images/framework-base/config-center.jpg"  width="1000">
