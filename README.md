# 德州扑克（增强版）· DSH 插件

DeepSeek Harness 的六人无限注德州扑克：**你 + 5 位会说话的 LLM 智能体**。
基于 [BubblePtr/dsh-holdem](https://github.com/BubblePtr/dsh-holdem)（MIT）二次开发，改动集中在交互层。

![牌桌](docs/screenshot.png)

## 这个版本多了什么

| 能力 | 说明 |
| --- | --- |
| **小窗 ⇄ 大视图** | 标题栏 `⤢ / ⤡` 一步切换。小窗 360×520 走紧凑分区布局；放大后是完整椭圆桌 + 右侧时间线栏（最多 1280×820，居中） |
| **`×` 关闭插件** | 等价于在「插件」页关掉本插件（走宿主 `pluginManager.setBundleEnabled`），只作用于自身 bundle；重开到「插件」页点开启 |
| **关闭不落盘** | 关闭状态只存在内存里，刷新或重启会重新显示，不会把自己锁在门外 |
| **放大态记忆** | 尺寸/位置/分页写在 `localStorage` 的 `texas-holdem.mini` |

规则、下注尺度、买入与出局、亮牌动效与上游一致。

## 安装

需要已安装 DeepSeek Harness（桌面版或 `dsh` CLI）。

```sh
# 桌面版（App 自带 CLI 可管理 desktop profile）
"/Applications/DeepSeek Harness.app/Contents/Resources/runtime/cli/bin/dsh" plugin --profile desktop add <本仓库目录或包路径>

# web profile
dsh plugin --profile web add <本仓库目录或包路径>
```

从本地目录安装时使用 `link:`，改完源码 `pnpm build` 后刷新页面即可生效（Host 半区改动需重启）。

卸载：

```sh
dsh plugin --profile desktop remove @local/texas-holdem
```

## 开发

```sh
pnpm install
pnpm build          # 产出 lib/index.js 与 lib/client.js（lib/ 已随仓库提交）
node --test test/*.test.mjs
```

`lib/` 是提交进仓库的构建产物：改 `src/` 后务必重新 `pnpm build`。

## 头像

`assets/avatars/` 里的**真人肖像不随本仓库分发**（肖像权原因）。缺失时每位智能体自动回退为
按 id 生成的几何头像（identicon），玩法与界面不受影响；你上传的覆盖头像走
`$DSH_HOME/texas-holdem/avatars/`，与仓库内容无关。

想启用写真头像：把 `<id>.jpg|png|webp`（`altman` / `dario` / `musk` / `liang` / `jensen`）
放进 `assets/avatars/` 再 `pnpm build`。

## 许可与归属

MIT。原始项目版权归 BubblePtr 及贡献者所有，见 `LICENSE`。
本仓库的二次改动（小窗放大、关闭插件、自有身份与图标）同样以 MIT 发布。
