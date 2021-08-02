---
title: '休眠和解除休眠沙箱環境 '
description: 休眠和解除休眠沙箱環境
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
source-git-commit: 09d5d125840abb6d6cc5443816f3b2fe6602459f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 0%

---

# 休眠和解除休眠沙箱環境 {#hibernating-introduction}

如果在特定時間內未偵測到任何活動，沙箱方案環境會進入&#x200B;*休眠模式*。

>[!NOTE]
>休眠是沙箱方案環境專屬的。 生產程式環境不會休眠。

## 休眠 {#hibernation-introduction}

休眠可以自動或手動進行。 沙箱方案環境最多可能需要幾分鐘的時間才能進入&#x200B;*休眠模式*。 資料會在休眠期間保留。

休眠分為：

* ****  閒置8小時後，「自動沙箱方案」環境會自動休眠，這表示製作、預覽或發佈服務都不會收到請求。

* **手動**:雖然不需要手動將沙箱方案環境休眠，但身為使用者，您可以手動將其休眠，因為休眠將在特定的閒置時段（8小時）後自動發生。

>[!CAUTION]
>在最新版本中，直接從Cloud Manager連結至開發人員控制台時，無法讓您將沙箱方案環境休眠。 解決方法是在開發人員控制台中，在url `#release-cm-p1234-e5678 where 1234` 1234的結尾加上下列模式： *程式ID*，而5678是您的&#x200B;*環境ID*。

### 使用手動休眠 {#using-manual-hibernation}

您可以透過兩種不同的方式，透過開發人員控制台手動將沙箱方案休眠，方法如下：

* 環境詳細資訊畫面
* 環境清單畫面

>[!NOTE]
>Cloud Manager的任何使用者皆可存取沙箱方案的開發人員控制台。

請依照下列步驟，手動將沙箱方案環境休眠：

1. 導覽至&#x200B;**開發人員控制台**。
請參閱[存取開發人員控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) ，了解如何從&#x200B;**環境**&#x200B;卡存取&#x200B;**開發人員控制台**。
   >[!IMPORTANT]
   >直接從Cloud Manager連結至&#x200B;**開發人員控制台**&#x200B;時，無法讓您將沙箱方案環境休眠。 解決方法是在開發人員控制台中，在url `#release-cm-p1234-e5678 where 1234` 1234的結尾加上下列模式： *程式ID*，而5678是您的&#x200B;*環境ID*。

1. 按一下&#x200B;**Hibernate**，如下圖所示：

   ![](assets/hibernate-1.png)

   或,

   按一下左上角的&#x200B;**Environments**&#x200B;連結以查看環境清單，然後按一下&#x200B;**Hibernate**，如下圖所示：

   ![](assets/hibernate-1b.png)

1. 按一下&#x200B;**Hibernate**&#x200B;以確認步驟。

   ![](assets/hibernate-2.png)

1. 休眠成功後，您會在&#x200B;**開發人員控制台**&#x200B;螢幕中看到您環境的休眠進程完成通知。

   ![](assets/hibernate-4.png)


## 解除休眠 {#de-hibernation-introduction}

1. 導覽至&#x200B;**開發人員控制台**。
請參閱[存取開發人員控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) ，了解如何從&#x200B;**環境**&#x200B;卡存取&#x200B;**開發人員控制台**。

   >[!IMPORTANT]
   >直接從Cloud Manager連結至&#x200B;**開發人員控制台**&#x200B;時，無法讓您選擇將沙箱方案環境解除休眠。 解決方法是在開發人員控制台中，在url `#release-cm-p1234-e5678 where 1234` 1234的結尾加上下列模式： *程式ID*，而5678是您的&#x200B;*環境ID*。

   >[!NOTE]
   >或者，您也可以嘗試存取已休眠環境的製作、預覽或發佈服務，以導覽至&#x200B;**開發人員控制台**&#x200B;以解除休眠；在這種情況下，會出現登錄頁面，並附有開發人員控制台的連結。 請參閱下方的存取休眠環境一節。

   >[!IMPORTANT]
   >對開發人員控制台的存取由&#x200B;**Admin Console**&#x200B;中的&#x200B;**雲端管理員 — 開發人員角色**&#x200B;定義。 擁有開發人員角色權限的使用者可將沙箱方案環境解除休眠。

1. 按一下&#x200B;**De-hibernate**，如下圖所示：

   ![](assets/de-hibernation-img1.png)

   或,

   按一下左上角的&#x200B;**Environments**&#x200B;連結以檢視環境清單，然後按一下&#x200B;**De-hibernate**，如下圖所示

   ![](assets/de-hibernate-1b.png)


1. 按一下「**解除休眠**」以確認步驟。

   ![](assets/de-hibernation-img2.png)

1. 您將收到解除休眠程式已啟動的通知，並將隨此進度更新。

   ![](assets/de-hibernation-img3.png)

1. 程式完成後，沙箱方案環境會再次啟用。

   ![](assets/de-hibernation-img4.png)

### 解除休眠的權限 {#permissions-de-hibernate}

任何具有產品設定檔且能以Cloud Service身分存取AEM的使用者都應能存取&#x200B;**開發人員控制台**，讓他們將環境解除休眠。

## 存取休眠環境 {#accessing-hibernated-environment}

針對休眠環境的製作、預覽或發佈層級提出任何瀏覽器請求時，使用者會遇到說明環境休眠狀態的登錄頁面，如下圖所示：

![](assets/de-hibernation-img5.png)

## 重要考量 {#important-considerations}

與休眠和解除休眠環境相關的幾項主要考量事項為：

* 使用者可使用管道將自訂程式碼部署至休眠環境。 環境將保持休眠狀態，解除休眠後，新程式碼會顯示在環境中。

* AEM升級可套用至休眠環境，客戶可從Cloud Manager手動觸發。 環境將保持休眠狀態，解除休眠後，新版本將會顯示在環境中。

* 閒置8小時後，沙箱會放入休眠節點，等到沙箱休眠後，即可解除休眠狀態。

* 沙箱會在6個月處於連續休眠模式後刪除，經過6個月後，便可重新建立。

   >[!NOTE]
   >目前，Cloud Manager不會指出環境是否休眠。

## AEM沙箱環境的更新 {#aem-updates-sandbox}

如需詳細資訊，請參閱[AEM版本更新](/help/implementing/deploying/aem-version-updates.md) 。

使用者可以手動將AEM更新套用至沙箱方案中的環境。

請參閱[更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)了解如何更新環境。

>[!NOTE]
>* 手動更新只能在目標環境具有正確配置的管道時執行。
>* 手動更新&#x200B;*Production*&#x200B;或&#x200B;*Stage*&#x200B;環境將自動更新其他環境。 生產+預備環境集必須位於相同AEM版本上。

