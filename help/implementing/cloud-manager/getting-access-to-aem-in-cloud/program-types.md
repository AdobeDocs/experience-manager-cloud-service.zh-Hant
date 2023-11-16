---
title: 計畫和計畫類型
description: 了解 Cloud Manager 的階層以及不同類型的計畫如何適應其結構以及它們之間的差異。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 93%

---


# 計畫和計畫類型 {#understanding-programs}

Cloud Manager 是圍繞實體階層建置的。這方面的詳細資訊對您在 Cloud Manager 中的日常工作並不重要，但概覽這些資訊可幫助您了解計畫並設定您自己的計畫。

![Cloud Manager 階層](assets/program-types1.png)

* **租用戶** - 這是階層的頂端。每個客戶都佈建了租用戶。
* **計畫** - 每個租用戶都有一個或多個計畫，[這些計畫通常反映了客戶的授權解決方案。](introduction-production-programs.md)
* **環境**- 每個計畫都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發用途。
   * 每個計畫只能有一個生產環境，但可能有多個非生產環境。
* **存放庫** - 計畫具有 Git 存放庫，可為環境維護應用程式和前端程式碼。
* **工具和工作流程** - 管道管理從存放庫到環境的程式碼部署，而其他工具可存取記錄、監視和環境管理。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租用戶**。
* WKND Travel and Adventure Enterprises 租用戶可能有兩個&#x200B;**計畫**：一個用於 WKND Magazine 的 Sites 計畫，和一個用於 WKND Media 的 Assets 計畫。
* WKND Magazine 和 WKND Media 計畫都將有開發、測試和製作&#x200B;**環境**。

## 原始碼存放庫 {#source-code-repository}

Cloud Manager 計畫將自動佈建自己的 Git 存放庫。

若要存取Cloud Manager Git存放庫，使用者需要使用具有命令列工具的Git使用者端、獨立的可視Git使用者端或使用者選擇的IDE，例如Eclipse、IntelliJ或NetBeans。

設定 Git 用戶端後，您可以從 Cloud Manager 使用者介面管理您的 Git 存放庫。若要了解如何使用 Cloud Manager 使用者介面管理 Git，請參閱[存取 Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

要開始開發 AEM Cloud 應用程式，必須從Cloud Manager存放庫簽出應用程式程式碼的本機副本，並存放至本機電腦上的某個位置。

```java
$ git clone {URL}
```

因此，工作流程是標準的 Git 工作流程。

1. 使用者可複製 Git 存放庫的本機副本。
1. 使用者會在本機程式碼存放庫中進行變更。
1. 準備就緒後，使用者將變更提交回遠端 Git 存放庫。

唯一的差異在於，遠端的 Git 存放庫屬於 Cloud Manager 的一部分，對開發人員而言是透明的。

## 計畫類型 {#program-types}

使用者可以建立&#x200B;**生產**&#x200B;計畫或&#x200B;**沙箱**&#x200B;計畫。

* **生產計畫**&#x200B;是為網站啟動即時流量而建立。
   * 如需更多詳細資訊，請參閱[生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
* **沙箱計畫**&#x200B;通常建立的目的是提供培訓、執行示範、培訓、POC 或文件。
   * 沙箱環境並不代表能承載即時流量，並且會有生產計畫沒有的限制。
   * 其中包含 Sites 和 Assets，且會透過 Git 分支自動填入，分支中包含範例程式碼、開發環境及非生產管道。
   * 如需更多詳細資訊，請參閱[沙箱計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。
