---
title: CI-CD管道
description: CI-CD管道
index: false
source-git-commit: 16e3280d7eaf53d8f944a60ec93b21c6676f0133
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%

---


# Cloud Manager CI-CD管道 {#intro-cicd}

## 簡介 {#introduction}

>[!NOTE]
>Cloud Manager中的CI/CD管道是由事件觸發，例如來自原始碼存放庫的提取請求、程式碼變更或定期排程以符合發行順序。

若要設定管道，您必須：
* 定義將啟動管道的觸發器
* 定義控制生產部署的參數
* 配置效能測試參數

在Cloud Manager中，有兩種管道：

* [生產管道](#prod-pipeline)
* [非生產管道](#non-prod-pipeline)

## 生產管道 {#prod-pipeline}

生產管道是專門建置的管道，包含一系列協調步驟，可將原始碼一直帶入生產環境。 這些步驟包括首先構建、打包、測試、驗證和部署到所有階段環境中。 不消說，只有建立生產和預備環境集後，才能新增生產管道。

>[!NOTE]
>如需詳細資訊，請參閱設定生產管道。


## 非生產管道 {#non-prod-pipeline}

非生產管道旨在執行程式碼品質掃描，或將原始碼部署至開發環境。

>[!NOTE]
>如需詳細資訊，請參閱僅限非生產及代碼品質的管道。
