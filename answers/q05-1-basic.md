# 第 5 题 1. 基础入门

参考资料：《构建第一个 HarmonyOS 应用（ArkTS）·快速入门·基础入门》
（华为 HarmonyOS 开发者官网，文档更新时间 2026-08-29）

## 1. 程序入口的执行点

完整路径：

```text
entry/src/main/ets/entryability
```

入口文件是 `entry/src/main/ets/entryability/EntryAbility.ets`。
其中 `onWindowStageCreate` 在窗口创建后加载首个页面。

## 2. 页面入口的执行点

完整路径：

```text
entry/src/main/ets/pages
```

首个页面文件是 `entry/src/main/ets/pages/Index.ets`，用 `@Entry` 标注，
`build()` 中描述页面 UI。

## 3. 获取 Router 并返回第一页

在第二个页面的返回按钮上绑定 `onClick`，通过 `UIContext` 获取 `Router`，
调用 `back()` 返回上一页，即第一页：

```ts
import { BusinessError } from '@kit.BasicServicesKit';

Button() {
  Text('Back')
    .fontSize(30)
    .fontWeight(FontWeight.Bold)
}
.onClick(() => {
  // 获取 UIContext
  let uiContext: UIContext = this.getUIContext();
  let router = uiContext.getRouter();
  try {
    // 返回第一页
    router.back();
    console.info('Succeeded in returning to the first page.');
  } catch (err) {
    let code = (err as BusinessError).code;
    let message = (err as BusinessError).message;
    console.error(`Failed to return to the first page. Code is ${code}, message is ${message}`);
  }
})
```

两页场景下，`router.back()` 会退回页面栈中的上一页，也就是第一页。

## 4. 第二个页面的路由配置文件

完整路径：

```text
entry/src/main/resources/base/profile/main_pages.json
```

需要把第二个页面的地址写进 `src` 数组：

```json
{
  "src": [
    "pages/Index",
    "pages/Second"
  ]
}
```
