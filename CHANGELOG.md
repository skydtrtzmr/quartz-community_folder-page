# Changelog

## [Unreleased]

### Changed

- fork 改名：`quartz.name` → `folder-page-pro`、`displayName` → `Folder Page Pro`（避免与社区版抢同一个
  `.quartz/plugins/<name>` 安装位）；`pageType` 仍为 `FolderPage` / `layout: "folder"`。
- 文件夹页文件列表的排序改为消费宿主注入的 `configuration.listingSort`（目录级 `field` + `order`，
  逐级向上继承），并由宿主比较器补齐日期兜底（`frontmatter[field]` → `dates[field]` → `dates.modified`
  → `dates.date`，仅对 `date/published/modified/created` 生效）；插件侧无比较器实现，`options.sort` 原样消费。
- 未移植：v4 的分批加载（`batchLoad` / 「加载更多」）与列表外观改造。

## 1.0.0

### Major Changes

- Stable 1.0 release. All `@quartz-community/*` dependencies now use `^1.0.0` ranges.

  Pre-1.0 caret ranges pinned the minor version (`^0.2.1` means `>=0.2.1 <0.3.0`), so
  published fixes to shared packages could never be resolved by dependents. Moving the
  ecosystem to 1.0 makes caret ranges behave conventionally.

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/)
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Respect the `file.data.unlisted` convention in both folder discovery (virtual page generation) and folder listings (the page-list inside a folder index). Unlisted pages are never shown in folder listings and never contribute folder/subfolder entries.
- Exported `pagesFromAllFiles` helper for reuse and testing.
- Unit tests for `pagesFromAllFiles` covering the unlisted-filter behavior.

- Initial Quartz community plugin template.
