---
title: 程式和程式類型
description: 瞭解Cloud Manager的層次結構以及不同類型的程式如何適應其結構以及它們有何不同。
exl-id: 507df619-a5b5-419a-9e38-db77541425a2
source-git-commit: 74e17ccb93c97dd6881c9b63d9a2d784d3add430
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# 程式和程式類型 {#understanding-programs}

Cloud Manager是圍繞實體層次構建的。 此詳細資訊對您在雲管理器中的日常工作並不重要，但是概述它將有助於您瞭解程式並設定自己的程式。

![雲管理器層次結構](assets/program-types1.png)

* **租戶**  — 這是層次結構的頂層。 每個客戶都有租戶。
* **程式。**  — 每個租戶都有一個或多個程式， [這通常反映客戶的許可解決方案。](introduction-production-programs.md)
* **環境**  — 每個計畫都有多個環境，例如為即時內容製作、一個用於試運行，一個用於開發。
   * 每個程式只能有一個生產環境，但有多個非生產環境。
* **儲存庫**  — 程式具有Git儲存庫，在該儲存庫中為環境維護應用程式和前端代碼。
* **工具和工作流**  — 管道管理從儲存庫到環境的代碼部署，而其他工具則允許訪問日誌、監視和環境管理。

一個示例通常有助於將此層次結構置於背景中。

* WKND旅行和冒險企業可能是 **租戶** 以旅行相關媒體為主。
* WKND旅遊和冒險企業租戶可能有兩個 **方案**:WKND雜誌的一個網站項目和WKND媒體的一個資產項目。
* WKND雜誌和WKND媒體項目都將具有開發、舞台和製作 **環境**。

## 原始碼存放庫 {#source-code-repository}

Cloud Manager程式將自動配置其自己的Git儲存庫。

要訪問Cloud Manager Git儲存庫，用戶需要使用帶有命令行工具的git客戶端、獨立的visual git客戶端或用戶選擇的IDE。

設定Git客戶端後，您可以從雲管理器UI管理Git儲存庫。 要瞭解如何使用Cloud Manager UI管理Git，請參閱文檔 [訪問Git。](/help/implementing/cloud-manager/managing-code/accessing-repos.md)

要開始開發AEM雲應用程式，必須將應用程式碼從Cloud Manager儲存庫簽出到本地電腦上的某個位置，從而建立其本地副本。

```java
$ git clone {URL}
```

因此，工作流是標準Git工作流。

1. 用戶克隆Git儲存庫的本地副本。
1. 用戶在本地代碼儲存庫中進行更改。
1. 準備好後，用戶將更改提交回遠程Git儲存庫。

唯一的區別是遠程Git儲存庫是Cloud Manager的一部分，對開發人員來說是透明的。

## 程式類型 {#program-types}

用戶可以建立 **生產** 程式或 **沙坑** 的子菜單。

* A **生產程式** 建立以啟用站點的即時通信。
   * 請參閱文檔 [生產計畫簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-production-programs.md) 的子菜單。
* A **沙盒程式** 通常建立目的是為培訓、運行演示、支援、POC或文檔提供服務。
   * 沙盒環境不是用來承載即時通信的，並且將具有生產程式不會受到的限制。
   * 它將包括站點和資產，並將自動填充一個包含示例代碼、開發環境和非生產流水線的Git分支來交付。
   * 請參閱文檔 [沙盒程式簡介](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/introduction-sandbox-programs.md) 的子菜單。
