# 微前端

  <img src="https://flyfedx.github.io/framework-docs/images/framework-base/microapp1.png"  width="520">

## 微前端架构

中后台应用由于其应用生命周期长(动辄 3+ 年)等特点，最后演变成一个巨石应用的概率往往高于其他类型的 web 应用。而从技术实现角度，微前端架构解决方案大概分为两类场景：

- 单实例：即同一时刻，只有一个子应用被展示，子应用具备一个完整的应用生命周期。通常基于 url 的变化来做子应用的切换。
- 多实例：同一时刻可展示多个子应用。通常使用 Web Components 方案来做子应用封装，子应用更像是一个业务组件而不是应用

MPA 方案的优点在于 部署简单、各应用之间硬隔离，天生具备技术栈无关、独立开发、独立部署的特性。缺点则也很明显，应用之间切换会造成浏览器重刷，由于产品域名之间相互跳转，流程体验上会存在断点。

SPA 则天生具备体验上的优势，应用直接无刷新切换，能极大的保证多产品之间流程操作串联时的流程性。缺点则在于各应用技术栈之间是强耦合的。

目标：将二者优势结合起来，构建出一个相对完善的微前端架构方案

微前端架构的优势，正是 MPA 与 SPA 架构优势的合集。即保证应用具备独立开发权的同时，又有将它们整合到一起保证产品完整的流程体验的能力。

  <img src="https://flyfedx.github.io/framework-docs/images/framework-base/microapp2.png"  width="520">

## 微前端的价值

- 微前端架构具备以下几个核心价值：
  - 技术栈无关 主框架不限制接入应用的技术栈，子应用具备完全自主权
  - 独立开发、独立部署 子应用仓库独立，前后端可独立开发，部署完成后主框架自动完成同步更新
  - 独立运行时 每个子应用之间状态隔离，运行时状态不共享

## 微应用开发

  1. 导出相应的生命周期钩子  
    - 微应用需要在自己的入口 js (通常就是你配置的 webpack 的 entry js) 导出 bootstrap、mount、unmount 三个生命周期钩子，以供主应用在适当的时机调用。  

        ```js
        /**
         * bootstrap 只会在微应用初始化的时候调用一次，下次微应用重新进入时会直接调用 mount 钩子，不会再重复触发 bootstrap。
        * 通常我们可以在这里做一些全局变量的初始化，比如不会在 unmount 阶段被销毁的应用级别的缓存等。
        */
        export async function bootstrap() {
          console.log('react app bootstraped')
        }
        /**
         * 应用每次进入都会调用 mount 方法，通常我们在这里触发应用的渲染方法
        */
        export async function mount(props) {
          console.log(props)
          ReactDOM.render(<App />, document.getElementById('react15Root'))
        }
        /**
         * 应用每次 切出/卸载 会调用的方法，通常在这里我们会卸载微应用的应用实例
        */
        export async function unmount() {
          ReactDOM.unmountComponentAtNode(document.getElementById('react15Root'))
        }
        /**
         * 可选生命周期钩子，仅使用 loadMicroApp 方式加载微应用时生效
        */
        export async function update(props) {
          console.log('update props', props)
        }
        ```
    - 无webpack项目嵌入主应用方式
      需要额外声明一个 script，用于 export 相对应的 lifecycles

      例如:
      - 声明 entry 入口
        ```html
        <!DOCTYPE html>
          <html lang="en">
          <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Purehtml Example</title>
          </head>
          <body>
              <div>
                  Purehtml Example
              </div>
          </body>
          
          <script src="//yourhost/entry.js" entry></script>
        </html>
        ```
      - 在 entry js 里声明 lifecycles
        ```js
          const render = ($) => {
          $('#purehtml-container').html("Hello, render with jQuery");
              return Promise.resolve();
          }
          
          (global => {
              global['purehtml'] = {
              bootstrap: () => {
                  console.log('purehtml bootstrap');
                  return Promise.resolve();
              },
              mount: () => {
                  console.log('purehtml mount');
                  return render($);
              },
              unmount: () => {
                  console.log('purehtml unmount');
                  return Promise.resolve();
              },
          };
          })(window);
        ```
  2. 配置微应用打包工具
    - 除了代码中暴露出相应的生命周期钩子之外，为了让主应用能正确识别微应用暴露出来的一些信息，微应用的打包工具需要增加如下配置：
      ```js
      const packageName = require('./package.json').name;
      module.exports = {
        output: {
          library: `${packageName}-[name]`,
          libraryTarget: 'umd',
          jsonpFunction: `webpackJsonp_${packageName}`,
        },
      };
      ```
  3. 检查入口  
    检查微应用的 entry html 中入口的 js 是不是最后一个加载的脚本。如果不是，需要移动顺序将其变成最后一个加载的 js，或者在 html 中将入口 js 手动标记为 entry。
  4. 微应用的静态资源支持跨域  
    主应用通过 fetch 去获取微应用的引入的静态资源的，所以必须要求这些静态资源支持跨域。  
    如果是自己的脚本，可以通过开发服务端跨域来支持。如果是三方脚本且无法为其添加跨域头，可以将脚本拖到本地，由自己的服务器 serve 来支持跨域。  
  5. 微应用同步主应用数据
    ```js
    // 从生命周期 mount 中获取通信方法，使用方式和 master 一致
    export function mount(props) {
      props.onGlobalStateChange((state, prev) => {
        // state: 变更后的状态; prev 变更前的状态
        console.log(state, prev);
      });
      //给主应用传递数据
      props.setGlobalState(state);
    }
    ```

## 为什么我们需要微前端？

1. 系统本身是需要集成和被集成的 一般有两种情况：
   - 旧的系统不能下，新的需求还在来。
     没有一家商业公司会同意工程师以单纯的技术升级的理由，直接下线一个有着一定用户的存量系统的。而你大概又不能简单通过 iframe 这种「靠谱的」手段完成新功能的接入，因为产品说需要「弹个框弹到中间」
   - 你的系统需要有一套支持动态插拔的机制。
     这个机制可以是一套精心设计的插件体系，但一旦出现接入应用或被接入应用年代够久远、改造成本过高的场景，可能后面还是会过渡到各种微前端的玩法。
2. 系统中的部件具备足够清晰的服务边界
   - 通过微前端手段划分服务边界，将复杂度隔离在不同的系统单元中，从而避免因熵增速度不一致带来的代码腐化的传染，以及研发节奏差异带来的工程协同上的问题。
3. 团队沟通协作成本太高
   - 如移动/联通功能类似但细节不一致
   - 如移动/联通版本版本发布时间不一致
4. 微前端是我们针对 R 版本业务应用接入的接口
