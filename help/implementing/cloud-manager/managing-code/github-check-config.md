---
title: 適用於私人存放庫的GitHub檢查設定
description: 瞭解如何控制自動建立的管道，以驗證每個對私有存放庫的提取請求。
source-git-commit: 73bd693d47f37b453209208816dfed15d65e9e09
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 7%

---


# 適用於私人存放庫的GitHub檢查設定 {#github-check-config}

瞭解如何控制自動建立的管道，以驗證每個對私有存放庫的提取請求。

## GitHub檢查設定 {#configuration}

使用時 [私人存放庫，](private-repositories.md#using) a [完整棧疊計畫碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md) 將會自動建立。 此管道在每次提取要求更新時啟動。

您可以透過建立 `.cloudmanager/pr_pipelines.yml` 私人存放庫預設分支中的檔案。

```yaml
github:
  shouldDeletePreviousComment: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR 
    importantMetricsFailureBehavior: CONTINUE
```

| 參數 | 可能的值 | 預設 | 說明 |
|---|---|---|---|
| `shouldDeletePreviousComment` | `true` 或 `false` | `false` | 是要僅保留其github提取請求上的程式碼掃描結果的最後一個註解，還是保留全部 |
| `type` | `CI_CD` | N/A | 定義CI/CD管道的行為 |
| `template.programID` | 整數 | 沒有可重複使用的管道變數 | 可用於重複使用 [管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 於每個PR自動建立的其中一個現有管道上設定的。 |
| `template.pipelineID` | 整數 | 沒有可重複使用的管道變數 | 可用於重複使用 [管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md) 於每個PR自動建立的其中一個現有管道上設定的。 |
| `namePrefix` | 字串 | `Full Stack Code Quality Pipeline for PR` | 用於設定自動建立的管道名稱 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或 `FAIL` 或 `PAUSE` | `CONTINUE` | 設定管道的重要量度行為<br>`CONTINUE` =如果重要量度失敗，管道將自動前進<br>`FAIL` =如果重要量度失敗，管道將完成並顯示「失敗」狀態<br>`PAUSE` =當重要量度失敗且必須手動繼續時，程式碼掃描步驟會收到「等待中」狀態 |
