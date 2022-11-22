# 登录页定制

- 支持通过 json 配置属性以及配置 css 样式，非常灵活的配置登录页样式布局。
- 配置说明:

```json
{
  "apiBaseUrl": "http://10.10.2.8:7001", //鉴权服务地址+端口
  /* 样式配置 */
  "styleConfig": {
    /* 配置名称 */
    "default": {
      "loginPageContainerImg": "/login/default/background.png", //整体页面的背景图片
      "loginPageContainerLogo": "/login/default/container-logo.png", //页面LOGO
      "loginFormContainerLogo": "/login/default/logo.png", //表单上方LOGO
      /* 页面LOGO样式，行内样式为CSS属性 */
      "loginPageLogoStyle": {
        "width": "400px",
        "top": "14%",
        "left": "7%"
      },
      "loginPageDecorate": "/login/default/container-decorate.png", //整体页面装饰图，覆盖到背景图片上方
      /* 页面装饰图样式，行内样式为CSS属性 */
      "loginPageDecorateStyle": {
        "top": "50%",
        "transform": "translate(-50%, -50%)",
        "left": "38%"
      },
      "loginFormContainerColorTheme": "dark", //表单框内样式主题：（dark/light）控制字体颜色
      /* 表单框定位参数，可传入其他css样式 */
      "loginFormContainerPosition": {
        "right": "7%"
      },
      "pageContainerBackgroundColor": "rgb(36, 45, 103)", //整体页面背景颜色
      "loginFavicon": "/OSS.svg", //浏览器图标
      "formContainerBackgroundImage": null, //表单框内背景图片
      "formContainerBackgroundColor": "rgba(69,75,113,0.4)", //表单框内背景颜色
      "loginTitle": "鉴权登录", //页面标题
      "usernameLabel": "账号", //用户名栏内显示文字
      "usernamePlaceholder": "请输入用户名/邮箱", //用户名栏内提示文字
      "usernameDefaultIcon": "iconzhanghao-3-2", //用户名栏内默认显示图标
      "usernameFocusIcon": "iconzhanghao-3", //用户名栏内聚焦图标
      "showUsernamePlaceholder": false, //是否展示用户名栏内提示文字
      "passwordLabel": "密码", //密码栏（字段介绍如上所示）
      "passwordPlaceholder": "请输入密码",
      "passwordDefaultIcon": "iconmimabeifen-3",
      "passwordFocusIcon": "iconmimabeifen-3-2",
      "showPasswordPlaceholder": false,
      "verifyCodeLabel": "验证码", //验证码栏（字段介绍如上所示）
      "verifyCodePlaceholder": "请输入验证码",
      "showVerifyCodePlaceholder": false,
      "verifyCodeDefaultIcon": "iconyanzhengma-3",
      "verifyCodeFocusIcon": "iconyanzhengma-3-2",
      "focusInputHideInputPrefixLabel": true, //聚焦的时候是否显示前缀（默认为显示）
      "findPasswordByMobileButton": true //是否展示找回密码按钮
    }
  },
  "stylePackageName": "default", // 当前使用的样式配置名称(在styleConfig中配置)
  "captchaCountdown": 5, //nubmer类型 找回密码验证码倒计时
  /*  登录方式配置  只有两种 默认 / frame    如果是frame  需要配置src和id 。都需要配置标题   可以配置 内容的类型（contentType）  增加："verify-code" 验证码登录方式 */
  "loginPage": [
    {
      "tabTitle": "本地登录"
    },
    {
      "tabTitle": "SSO登录",
      "isFrame": true,
      "frameSrc": "http://sso.gmcc.net/?client_id=cnms_gmcc_net&amp;returnUrl=http://cnms.gmcc.net/SMonitor/ssoCheck.aspx",
      "frameId": "loginIframe"
    }
  ]
}
```

- 示例：  
  - 移动登录页  

    <img src="https://flyfedx.github.io/framework-docs/images/framework-base/login1.jpg"  width="1000">
  - 可视化平台登录页  

    <img src="https://flyfedx.github.io/framework-docs/images/framework-base/login2.jpg"  width="1000">
  - 联通登录页  

    <img src="https://flyfedx.github.io/framework-docs/images/framework-base/login3.jpg"  width="1000">
