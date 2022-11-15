---
title: 計畫和計畫類型
description: 了解 Cloud Manager 的階層以及不同類型的計畫如何適應其結構以及它們之間的差異。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: ht
source-wordcount: '533'
ht-degree: 100%

---


# 計畫和計畫類型 {#understanding-programs}

Cloud Manager 是圍繞實體階層建置的。這方面的詳細資訊對您在 Cloud Manager 中的日常工作並不重要，但概覽這些資訊可幫助您了解計畫並設定您自己的計畫。

![Cloud Manager 階層](assets/program-types1.png)

* **租使用者** - 這是階層的頂端。每個客戶都佈建了租使用者。
* **計畫** - 每個租使用者都有一個或多個計畫，[這些計畫通常反映了客戶的授權解決方案。](introduction-production-programs.md)
* **環境**- 每個計畫都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發用途。
   * 每個計畫只能有一個生產環境，但可能有多個非生產環境。
* **存放庫** - 計畫具有 Git 存放庫，可為環境維護應用計劃和前端計劃碼。
* **工具和工作流程** - 管道管理從存放庫到環境的計劃碼部署，而其他工具可存取記錄、監視和環境管理。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租使用者**。
* WKND Travel and Adventure Enterprises 租使用者可能有兩個&#x200B;**計畫**：一個用於 WKND Magazine 的 Sites 計畫，和一個用於 WKND Media 的 Assets 計畫。
* WKND Magazine 和 WKND Media 計畫都將有開發、測試和製作&#x200B;**環境**。

## 原始碼存放庫 {#source-code-repository}

Cloud Manager 計畫將自動佈建自己的 Git 存放庫。

要存取 Cloud Manager Git 存放庫，使用者需要使用具有命令行工具的 Git 用戶端、獨立的是絕畫 Git 用戶端或使用者選擇的 IDE，例如 Eclipse、IntelliJ 或 NetBeans。

設定 Git 用戶端後，您可以從 Cloud Manager UI 管理您的 Git 存放庫。若要了解如何使用 Cloud Manager UI 管理 Git，請參閱文件：[存取 Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

要開始開發 AEM Cloud 應用計劃，必須從Cloud Manager存放庫簽出應用計劃計劃碼的本機副本，並存放至本機電腦上的某個位置。

```java
$ git clone {URL}
```

因此，工作流程是標準的 Git 工作流程。

1. 使用者可複製 Git 存放庫的本機副本。
1. 使用者會在本機計劃碼存放庫中進行變更。
1. 準備就緒後，使用者將變更提交回遠端 Git 存放庫。

唯一的差異在於，遠端的 Git 存放庫屬於 Cloud Manager 的一部分，對開發人員而言是透明的。

## 計畫類型 {#program-types}

使用者可以建立&#x200B;**生產**&#x200B;計畫或&#x200B;**沙箱**&#x200B;計畫。

* **生產計畫**&#x200B;是為啟用網站的即時流量而建立的。
   * 如需了解詳細資訊，請參閱文件：[生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
* **沙箱計畫**&#x200B;通常建立的目的是提供培訓、執行示範、培訓、POC 或文件。
   * 沙箱環境並不代表能承載即時流量，並且會有生產計畫沒有的限制。
   * 其中包含 Sites 和 Assets，且會透過 Git 分支自動填入，分支中包含範例計劃碼、開發環境及非生產管道。
   * 如需了解詳細資訊，請參閱文件：[沙箱計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。
