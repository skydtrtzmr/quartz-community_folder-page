# @quartz-community/folder-page

> **本仓库是 fork**：本地以 submodule 挂在 `plugins-local/folder-page-pro`，`quartz.name = folder-page-pro`
> （与社区版同名会抢 `.quartz/plugins/<name>` 安装位，见 `QUARTZ5-COMMANDS.md` §四）。
>
> - **与社区版的差异**：文件夹页文件列表的排序比较器**不在本插件内**——由宿主
>   `quartz5/quartz/plugins/loader/config-loader.ts` 按插件名注入
>   `plugin.options.sort = createFolderPageSort(configuration.listingSort)`（目录级 `field` + `order`，
>   逐级向上继承；含日期兜底）。`FolderContent`/`PageList` 原样消费 `options.sort`。
> - `pageType` 仍导出 `name: "FolderPage"`、`layout: "folder"`（`layout.byPageType.folder` 依赖，勿改）。
> - 文件夹页向 `aggregation-page-pro` 的统一列表脚本提供直属文件、真实子目录、frontmatter 和排序配置。
>   运行期按右上角面板选择的字段展示嵌套分类，每个文件列表先显示 20 条，可继续加载。
>   运行期数据加载失败时保留原有 SSR `PageList`。两插件需要同时启用。
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
