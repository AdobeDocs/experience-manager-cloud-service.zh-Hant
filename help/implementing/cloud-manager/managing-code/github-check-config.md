---
title: 私人存放庫的提取請求檢查
description: 了解如何控制自動建立的管道以驗證對私人存放庫的每個提取請求。
exl-id: 3ae3c19e-2621-4073-ae17-32663ccf9e7b
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 30%

---

# 私人存放庫的提取請求檢查 {#github-check-config}

了解如何控制自動建立的管道以驗證對私人存放庫的每個提取請求。

## 私人存放庫檢查的設定 {#configuration}

使用[私人存放庫時](private-repositories.md#using)，其會自動建立[全端程式碼品質管道](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md)。此管道會在每次提取請求更新時啟動。

您可以在私人存放庫的預設分支中建立`.cloudmanager/pr_pipelines.yml`設定檔，以控制這些檢查。

```yaml
pullRequest:
  shouldDeletePreviousComment: false
  shouldSkipCheckAnnotations: false
pipelines:
  - type: CI_CD
    template:
      programId: 1234
      pipelineId: 456
    namePrefix: Full Stack Code Quality Pipeline for PR
    importantMetricsFailureBehavior: CONTINUE
```

| 參數 | 可能的值 | 預設 | 說明 |
| --- | --- | --- | --- |
| `shouldDeletePreviousComment` | `true` 或 `false` | `false` | 是隻保留此GitHub提取請求上程式碼掃描結果的最後一個註解，還是保留全部。 將其設定為`false` （預設）表示不會刪除先前的註解。 |
| `shouldSkipCheckAnnotations` | `true` 或 `false` | `false` | GitHub提取請求檢查中是否有其他註解。 將其設為`false` （預設）表示檢查註解不會被略過，並會包含在意見反應中。 |
| `type` | `CI_CD` | N/A | 定義CI/CD （持續整合/持續部署）管道設定的行為。 |
| `template.programId` | 整數 | 沒有重複使用管道變數 | 您可以使用它來重複使用每個提取請求自動建立的現有管道上設定的[管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `template.pipelineId` | 整數 | 沒有重複使用管道變數 | 您可以使用它來重複使用每個提取請求自動建立的現有管道上設定的[管道變數](/help/implementing/cloud-manager/configuring-pipelines/pipeline-variables.md)。 |
| `namePrefix` | 字串 | `Full Stack Code Quality Pipeline for PR` | 用於設定自動建立之管道名稱的前置詞。 |
| `importantMetricsFailureBehavior` | `CONTINUE` 或 `FAIL` 或 `PAUSE` | `CONTINUE` | 設定管道的重要量度行為<br>`CONTINUE` =如果重要量度失敗，則管道會自動前進<br>`FAIL` =如果重要量度失敗，則管道會以「失敗」狀態結束<br>`PAUSE` =當重要量度失敗時，程式碼掃描步驟會收到「等待」狀態，且必須手動繼續 |




