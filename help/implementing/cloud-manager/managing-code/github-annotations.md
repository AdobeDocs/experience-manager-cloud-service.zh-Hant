---
title: GitHub檢查附註
description: 瞭解GitHub如何檢查私人存放庫的註釋PR，以提供您有用的意見回饋。
exl-id: 15178de8-8a8a-4300-8510-88875ad0fc8c
source-git-commit: f7348d388918a31d255babcfb64b3dc547153d62
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# GitHub檢查附註 {#github-annotations}

瞭解GitHub如何檢查私人存放庫的註釋PR，以提供您有用的意見回饋。

## 概觀 {#overview}

如果您使用 [私人存放庫](private-repositories.md) 對於您的Cloud Manager程式，系統會自動針對每個提取請求執行GitHub簽入。 這些註解含有實用資訊，可協助您儘快瞭解程式碼的任何問題。

![GitHub檢查註解範例](assets/github-check-annotations.png)

[程式碼品質](/help/implementing/cloud-manager/code-quality-testing.md) 偵測到的問題 [SonarQube](/help/implementing/cloud-manager/custom-code-quality-rules.md) 已清楚列出。

![程式碼問題註解的範例](assets/github-check-annotations-example.png)

已提供問題的確切程式碼行，您可以按一下它以顯示相關程式碼。 這些註解適用於所有程式碼問題，而不僅僅是提取請求中變更的問題。

![程式碼問題註解的範例](assets/github-check-annotations-example-code.png)

所有附註的行都會彙總在 **檔案已變更** 索引標籤中的「GitHub提取請求」。 提取請求中未變更之檔案的註解會顯示在其本身的區段中。

![已變更檔案標籤上的註解範例](assets/github-check-annotations-files-changed.png)

## 計畫碼品質管道 {#code-quality-pipelines}

此 [程式碼品質](/help/implementing/cloud-manager/code-quality-testing.md) 結果也會顯示在由Cloud Manager自動觸發的管道底部 **檢查** 標籤。 您也可以從以下位置存取： **詳細資料** 提取請求的檢查。

![註解範例](assets/github-check-annotations-code-quality.png)

![註解範例](assets/github-check-annotations-code-quality-2.png)

您也可以以CSV格式視覺化問題。 這可以由以下方式擷取： [在Cloud Manager中檢視管道執行的詳細資訊。](/help/implementing/cloud-manager/configuring-pipelines/managing-pipelines.md#view-details)
