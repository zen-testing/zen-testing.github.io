---
title: '使用gh命令下载Github自动构建生成的工件'
date: 2024-04-15 15:26:54
tags: [GitHub ]
published: true
hideInList: false
feature: 
isTop: false
---
# 下载工作流工件 - GitHub Docs

> ## Excerpt
> You can download archived artifacts before they automatically expire.

---
要了解有关 GitHub CLI 的更多信息，请参阅“[关于 GitHub CLI](https://docs.github.com/en/github-cli/github-cli/about-github-cli) ”。

GitHub CLI 将根据工件名称将每个工件下载到单独的目录中。如果仅指定单个工件，它将被提取到当前目录中。

要下载工作流运行生成的所有工件，请使用`run download`子命令。替换`run-id`为您要从中下载工件的运行的 ID。如果您不指定`run-id`，GitHub CLI 将返回一个交互式菜单，供您选择最近的运行。

```shell
gh run download RUN_ID
```

要从运行中下载特定工件，请使用`run download`子命令。替换`run-id`为您要从中下载工件的运行的 ID。替换`artifact-name`为您要下载的工件的名称。

```shell
gh run download RUN_ID -n ARTIFACT_NAME
```

您可以指定多个工件。

```shell
gh run download RUN_ID> -n ARTIFACT_NAME-1 -n ARTIFACT_NAME-2
```

要下载存储库中所有运行的特定工件，请使用`run download`子命令。

```shell
gh run download -n ARTIFACT_NAME-1 ARTIFACT_NAME-2
```
