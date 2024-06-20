---
title: 私人存放庫的 GitHub 檢查設定
description: 瞭解如何控制自動建立的管道，以驗證每個對私有存放庫的提取請求。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 77%

---

# 私人存放庫的 GitHub 檢查設定 {#github-check-config}

瞭解如何控制自動建立的管道，以驗證每個對私有存放庫的提取請求。

## GitHub 檢查配定 {#configuration}

使用[私人存放庫時，](private-repositories.md#using)[全端程式碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)將自動建立。此管道在每次提取要求更新時啟動。

您可以透過建立一個 `.cloudmanager/pr_pipelines.yml` 檔案 (位於私有存放庫的預設分支中) 來控制這些檢查。

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
| `type` | `CI_CD` | N/A | 定義 CI/CD 管道的行為 |
| `template.programID` | 整數 | 沒有重複使用管道變數 | 可用來重複使用[管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)；這些變數是設定在由每個 PR 自動建立的現有一個管道上。 |
| `template.pipelineID` | 整數 | 沒有重複使用管道變數 | 可用來重複使用[管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)；這些變數是設定在由每個 PR 自動建立的現有一個管道上。 |
| `namePrefix` | 字串 | `Full Stack Code Quality Pipeline for PR` | 用來設定自動建立的管道名稱 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或 `FAIL` 或 `PAUSE` | `CONTINUE` | 設定管道的重要指標行為<br>`CONTINUE` = 如果某個重要指標失敗，管道就會自動向前移動<br>`FAIL` = 如果重要指標失敗，管道將以「失敗」狀態結束<br>`PAUSE` = 當重要指標失敗且必須手動恢復時，程式碼掃描步驟將收到「等待」狀態 |
