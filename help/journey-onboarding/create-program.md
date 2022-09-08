---
title: 建立方案
description: 了解如何使用Cloud Manager建立您的第一個方案。
role: Admin, User, Developer
exl-id: ade4bb43-5f48-4938-ac75-118009f0a73b
source-git-commit: fbf1e0b7cefb1dc981d7ee106283280fb2225007
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%

---

# 建立方案 {#create-program}

在 [入門旅程，](overview.md) 您將學習如何使用Cloud Manager建立您的第一個方案。

## 目標 {#objective}

檢閱此入門歷程中的上一份檔案後， [存取Cloud Manager、](cloud-manager.md) 您已確保您擁有適當的Cloud Manager存取權。 現在您可以建立第一個方案。

閱讀本檔案後，您將：

* 了解程式是什麼。
* 了解生產與沙箱方案之間的差異。
* 能夠建立您自己的方案。

## 什麼是程式？ {#programs}

計畫是Cloud Manager中組織的最高層級。 根據您的Adobe授權，計畫允許您組織解決方案並授予對這些計畫的特定團隊成員訪問權限。

Cloud Manager程式代表一組Cloud Manager環境。 這些計畫支援邏輯的業務計畫集，通常對應於許可的服務級別協定(SLA)。 例如，一個方案可代表AEM資源，以支援組織的全域公用網站，而另一個方案則代表內部的中央DAM。

如果您回想一下WKND Travel and Adventure Enterprises（WKND Travel and Adventure Enterprises，該企業是專注於旅遊相關媒體的租戶）的理論範例，他們可能會有兩個計畫：WKND雜誌部的一個網站項目和WKND媒體部的一個資產項目。 然後，由於各自的分工要求，不同的團隊成員將能夠獲得不同方案。

有兩種不同的程式類型：

* A **生產計畫** 是為啟用網站的即時流量而建立的。 這是你的「真實」環境。
* A **沙箱方案** 通常建立的目的是提供培訓、運行演示、培訓、POC或文檔。

由於它們的用途不同，因此不同的環境有不同的選項。 不過，建立這些變數的程式很類似。 在上線過程中，我們會建立沙箱環境。

>[!NOTE]
>
>依預設，具有AEM環境存取權的使用者也會擁有「雲端>管理員」使用者角色。 此角色本身和本身不足以讓使用者存取方案詳細資料檢視。 只有Cloud Manager使用者角色的這類使用者，可透過方案功能表選項導覽至AEM環境製作URL（如果存在環境）。 如果這些用戶希望獲得程式級訪問權限，則必須與其管理員聯繫。

## 建立沙箱方案 {#create-sandbox}

請依照下列步驟建立沙箱方案。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 在Cloud Manager的登陸頁面上按一下 **添加程式** 在畫面的右上角。

   ![Cloud Manager登陸頁面](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/first_timelogin1.png)

1. 在建立程式嚮導中，選擇 **設定沙箱**，請提供方案名稱，然後按一下 **建立**.

   ![程式類型建立](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/create-sandbox.png)

隨著設定程式的進行，您會在登陸頁面上看到新的沙箱方案卡片，其中包含狀態指標。

![從概述頁面建立沙箱](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/assets/program-create-setupdemo2.png)

方案完成後，您組織的成員會指派給 **開發人員** 產品設定檔可登入Cloud Manager並管理Cloud Manager git存放庫。

## 下一步 {#whats-next}

現在，您已建立第一個程式，便可為其建立環境。 您應繼續進行上線歷程，繼續檢閱此檔案 [建立環境。](create-environments.md)

## 其他資源 {#additional-resources}

請依照其他資源了解：

* [方案和方案類型](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md)  — 了解Cloud Manager的階層，以及不同類型的程式如何配合其結構，以及其差異。
* [建立沙箱方案](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-sandbox-programs.md)  — 了解如何使用Cloud Manager建立您自己的沙箱計畫，以用於訓練、示範、POC或其他非生產用途。
* [建立生產計畫](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/creating-production-programs.md)  — 了解如何使用Cloud Manager建立您自己的生產程式來托管即時流量。
* [使用AdobeCloud Manager — 方案](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html) - Cloud Manager計畫表示一組支援業務計畫邏輯集的AEM環境，通常對應於購買的服務級別協定(SLA)。
