# @quartz-community/folder-page

> **本仓库是 fork**：本地以 submodule 挂在 `plugins-local/folder-page-pro`，`quartz.name = folder-page-pro`
> （与社区版同名会抢 `.quartz/plugins/<name>` 安装位，见 `QUARTZ5-COMMANDS.md` §四）。
>
> - **与社区版的差异**：文件夹页文件列表的排序比较器**不在本插件内**——由宿主
>   `quartz5/quartz/plugins/loader/config-loader.ts` 按插件名注入
>   `plugin.options.sort = createFolderPageSort(configuration.listingSort)`（目录级 `field` + `order`，
>   逐级向上继承；含日期兜底）。`FolderContent`/`PageList` 原样消费 `options.sort`。
> - `pageType` 仍导出 `name: "FolderPage"`、`layout: "folder"`（`layout.byPageType.folder` 依赖，勿改）。
> - **未移植**：v4 的「分批加载 + 加载更多」按钮；v4 的列表外观改造（`folder-item`/`file-item` 项类与字重、
>   两列网格、隐藏 tags）。
> - upstream = `quartz-community/folder-page`；增量改动提交到 `dev` 分支（`main` 保持镜像上游）。

Renders folder index pages showing a listing of all pages within that folder. Automatically generates virtual index pages for folders that don't have one.

## Installation

```bash
npx quartz plugin add github:quartz-community/folder-page
```

## Usage

```yaml title="quartz.config.yaml"
plugins:
  - source: github:quartz-community/folder-page
    enabled: true
```

For advanced use cases, you can override in TypeScript:

```ts title="quartz.ts (override)"
import * as ExternalPlugin from "./.quartz/plugins";

ExternalPlugin.FolderPage({
  showFolderCount: true,
  showSubfolders: true,
  prefixFolders: false,
});
```

## Configuration

| Option            | Type      | Default     | Description                                                                            |
| ----------------- | --------- | ----------- | -------------------------------------------------------------------------------------- |
| `showFolderCount` | `boolean` | `undefined` | Whether to show the number of items in the folder.                                     |
| `showSubfolders`  | `boolean` | `undefined` | Whether to show subfolders in the listing.                                             |
| `sort`            | `SortFn`  | `undefined` | A function to sort the pages in the folder.                                            |
| `prefixFolders`   | `boolean` | `false`     | Whether to prefix generated folder page titles with "Folder: " (e.g. "Folder: notes"). |

## Documentation

See the [Quartz documentation](https://quartz.jzhao.xyz/plugins/FolderPage) for more information.

## License

MIT
