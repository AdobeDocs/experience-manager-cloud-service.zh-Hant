---
title: 計畫和計畫類型
description: 了解 Cloud Manager 的階層以及不同類型的計畫如何適應其結構以及它們之間的差異。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 44%

---


# 程式和程式型別 {#understanding-programs}

Cloud Manager 是圍繞實體階層建置的。詳細資訊對於您在Cloud Manager中的日常工作並不重要，但概覽這些資訊可幫助您瞭解計畫並設定您自己的計畫。

![Cloud Manager 階層](assets/program-types1.png)

* **租使用者** — 階層的頂端。 每個客戶都佈建了租用戶。
* **程式** — 每個租使用者都有一或多個程式，[通常反映了客戶的授權解決方案](introduction-production-programs.md)。
* **環境**- 每個計畫都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發用途。
   * 每個計畫只能有一個生產環境，但可能有多個非生產環境。
* **存放庫** — 計畫具有Git存放庫，可為環境維護應用計畫和前端計畫碼。
* **工具和工作流程** - 管道管理從存放庫到環境的程式碼部署，而其他工具可存取記錄、監視和環境管理。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租用戶**。
* WKND Travel and Adventure Enterprises 租用戶可能有兩個&#x200B;**方案**：一個用於 WKND Magazine 的 Sites 方案，和一個用於 WKND Media 的 Assets 方案。
* WKND Magazine 和 WKND Media 方案都將有開發、測試和生產&#x200B;**環境**。

## 原始程式碼存放庫 {#source-code-repository}

Cloud Manager程式會自動布建自己的Git存放庫。

使用者可使用具有命令列工具的Git使用者端或獨立的視覺化Git使用者端，存取Cloud Manager Git存放庫。 或者，他們也可以使用慣用的整合開發環境(IDE)，例如Eclipse、IntelliJ或NetBeans。

設定Git使用者端後，您可以從Cloud Manager使用者介面管理您的Git存放庫。 若要瞭解如何使用Cloud Manager使用者介面管理Git，請參閱[存取Git](/help/implementing/cloud-manager/managing-code/accessing-repos.md)。

若要開始開發AEM Cloud應用程式，請從Cloud Manager存放庫將應用程式程式碼簽出至您的本機電腦。

```java
$ git clone {URL}
```

工作流程會遵循標準Git程式：

1. 使用者可在本機複製遠端Git存放庫。
1. 使用者會在其本機存放庫中進行變更。
1. 準備就緒後，使用者將變更提交回遠端Git存放庫。

唯一的差異在於，遠端Git存放庫屬於Cloud Manager的一部分，對開發人員而言是透明的。

## 計畫型別 {#program-types}

使用者可以建立&#x200B;**生產**&#x200B;計畫或&#x200B;**沙箱**&#x200B;計畫。

* **生產計畫**&#x200B;是為網站啟動即時流量而建立。
   * 如需更多詳細資訊，請參閱[生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md)。
* **沙箱方案**&#x200B;通常建立的目的是提供培訓、執行示範、培訓、POC 或文件。
   * 沙箱環境並不意味著承載即時流量，並且有生產程式沒有的限制。
   * 其中包含Sites、Assets和Edge Delivery Services，並預先填入Git分支，其中包含範常式式碼、開發環境及非生產管道。
   * 如需更多詳細資訊，請參閱[沙箱方案簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md)。
