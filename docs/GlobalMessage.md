# 主微应用数据共享

主应用会共享`postMessage`、`addGlobalMessageListener`、`offGlobalMessageListener`、`onGlobalStateChange`方法，供微应用去传递/监听消息给主应用或其他微应用。

当需要在微应用间通信时，使用`postMessage`方法。

<b>方法说明: </b>

- `postMessage`

```
/**
* 发送消息方法
* @param messageType 消息类型 用来唯一标识消息
* @param params 消息传递参数 内容自定义
* @param target 消息传递目标 'framework'|'microApp'  默认传递'framework'：标识发送给框架，'microApp'：标识传递给微应用
*/
postMessage: (messageType, params, target = 'framework')
```

- `addGlobalMessageListener`-监听消息通知

```
/**
* 订阅消息通知
* @param messageType 消息类型 用来唯一标识消息
* @param handler 消息处理函数
*/
addGlobalMessageListener: (messageType, handler)
```

- `offGlobalMessageListener`-移除监听消息通知

```
/**
* 取消订阅消息通知
* @param messageType 消息类型 用来唯一标识消息
* @param handler 消息处理函数
*/
offGlobalMessageListener: (messageType, handler)
```

-  `onGlobalStateChange`-全局状态改变

```
/**
* 全局状态改变时触发
* @param callback 回调函数
*/
onGlobalStateChange: (callback)
```

<b>数据共享：</b>

- 主应用在登录成功获取到用户信息之后，会通过 `setGlobalState` 方法来存储用户信息及其他需要共享的数据。

```js
globalAction.setGlobalState({ userInfo: currentUserInfo })
```

- 当globalState发生变化时，会触发微应用传递给`onGlobalStateChange`的回调函数并将共享值当做参数传递，微应用可在该回调函数中存储获取的共享数据。

```js
props.onGlobalStateChange((value) => {
    setUserInfo(value.userInfo);
    setSystemInfo(value.systemInfo);
}, true);
```
