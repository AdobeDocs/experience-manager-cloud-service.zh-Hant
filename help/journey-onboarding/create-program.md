---
title: 建立程式
description: 瞭解如何使用Cloud Manager建立第一個程式。
role: Admin, User, Developer
source-git-commit: 709a80683357b0d56280ff14aa5f4ba6bf2c6b23
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---


# 建立程式 {#create-program}

在 [登機之旅，](overview.md) 您將學習如何使用雲管理器建立第一個程式。

## 目標 {#objective}

在審閱了上次登機旅程的檔案後， [訪問雲管理器，](cloud-manager.md) 您已確保您有適當的訪問雲管理器的權限。 現在，您可以建立第一個程式。

閱讀此文檔後，您將：

* 瞭解程式是什麼。
* 瞭解生產程式和沙盒程式之間的區別。
* 能夠建立自己的程式。

## 什麼是程式？ {#programs}

程式是雲管理器中組織級別最高的程式。 根據您的Adobe許可，程式允許您組織解決方案並授予特定團隊成員對這些程式的訪問權限。

Cloud Manager程式表示Cloud Manager環境集。 這些計畫支援邏輯的業務計畫集，通常對應於許可的服務級別協定(SLA)。 例如，一個方案可以表示支AEM持組織的全球公共網站的資源，而另一個方案則表示內部的中央DAM。

如果你回想一下WKND旅遊和冒險企業理論的例子，它們可能有兩個項目：其WKND雜誌部的一個網站方案和WKND媒體部的一個資產方案。 然後，由於各自的分工要求，不同的團隊成員將能夠參加不同的方案。

有兩種不同的程式類型：

* A **生產程式** 建立以啟用站點的即時通信。 這是你的&quot;真實&quot;環境。
* A **沙盒程式** 通常建立目的是為培訓、運行演示、支援、POC或文檔提供服務。

由於它們用於不同的目的，因此不同的環境有不同的選項。 但建立它們的過程是相似的。 在此登機過程中，我們將建立沙盒環境。

## 建立沙盒程式 {#create-sandbox}

按照以下步驟建立沙盒程式。

1. 登錄到Cloud Manager(位於 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選擇相應的組織。

1. 在Cloud Manager的登錄頁上按一下 **添加程式** 在螢幕右上角。

   ![雲管理器登錄頁](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. 在建立程式嚮導中，選擇 **設定沙盒**，提供程式名，然後按一下 **建立**。

   ![程式類型建立](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

在安裝過程進行時，您將在登錄頁上看到一個新的沙盒程式卡，其中帶有狀態指示器。

![從概述頁建立沙盒](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

程式完成後，您組織的成員將分配給 **開發人員** 產品配置檔案可以登錄到Cloud Manager並管理Cloud Manager git儲存庫。

## 下一步是什麼 {#whats-next}

現在，您已建立了第一個程式，您可以為它建立環境。 您應通過下次查看文檔來繼續登機旅程 [建立環境。](create-environments.md)

## 其他資源 {#additional-resources}

按照其他資源瞭解：

* [程式和程式類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)  — 瞭解Cloud Manager的層次結構以及不同類型的程式如何適應其結構以及它們有何不同。
* [建立沙盒程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)  — 瞭解如何使用雲管理器建立您自己的沙盒程式，以用於培訓、演示、POC或其他非生產目的。
* [建立生產程式](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)  — 瞭解如何使用雲管理器建立您自己的生產程式來承載即時流量。
* [使用Adobe雲管理器 — 程式](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Cloud Manager程式表示支援AEM邏輯業務計畫集的一組環境，通常對應於購買的服務級別協定(SLA)。
