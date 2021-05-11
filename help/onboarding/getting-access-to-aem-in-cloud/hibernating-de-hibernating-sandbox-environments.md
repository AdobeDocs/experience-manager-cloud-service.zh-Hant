---
title: '冬眠和冬眠沙盒環境 '
description: 冬眠和冬眠沙盒環境
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
translation-type: tm+mt
source-git-commit: 3b57acc47dd60d050ceebebb12bd9080b7fc5cf5
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---

# 冬眠和冬眠沙盒環境{#hibernating-introduction}

如果在某段時間內未檢測到任何活動，則沙箱程式環境進入&#x200B;*休眠模式*。

>[!NOTE]
>Hibernation是沙盒程式環境獨有的。 生產計畫環境不休眠。

## 休眠{#hibernation-introduction}

休眠可以自動或手動進行。 沙盒程式環境進入&#x200B;*休眠模式*&#x200B;可能需要幾分鐘的時間。 資料會在冬眠期間保留。

冬眠分為：

* **在閒置**  8小時後，AutomaticSandbox Program環境會自動休眠，這表示作者和發佈服務都不會收到請求。

* **手動**:作為用戶，您可以手動休眠沙盒程式環境，但無需手動休眠，因為休眠將在一段時間（8小時）不活動後自動發生。

>[!CAUTION]
>在最新版本中，直接從Cloud Manager連結至「開發人員主控台」時，您無法選擇讓沙盒程式環境休眠。 解決方法是在Developer Console中，將下列模式新增至url `#release-cm-p1234-e5678 where 1234` 1234的結尾是您的&#x200B;*Program ID*，而5678是您的&#x200B;*Environment ID*。

### 使用手動休眠{#using-manual-hibernation}

您可以使用下列兩種不同方式，從「開發人員主控台」手動讓沙盒程式休眠：

* 環境細節螢幕
* 環境清單螢幕

>[!NOTE]
>Cloud Manager的任何使用者都可存取沙盒程式的Developer Console。

請依照下列步驟，手動讓沙盒程式環境休眠：

1. 導覽至&#x200B;**Developer Console**。
請參閱[存取開發人員主控台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，瞭解如何從&#x200B;**環境**&#x200B;卡存取&#x200B;**開發人員主控台**。
   >[!IMPORTANT]
   >直接從Cloud Manager連結至&#x200B;**Developer Console**&#x200B;時，您無法選擇讓沙盒程式環境休眠。 解決方法是在Developer Console中，將下列模式新增至url `#release-cm-p1234-e5678 where 1234` 1234的結尾是您的&#x200B;*Program ID*，而5678是您的&#x200B;*Environment ID*。

1. 按一下&#x200B;**Hibernate** ，如下圖所示：

   ![](assets/hibernate-1.png)

   或,

   按一下左上角的&#x200B;**Environments**&#x200B;連結查看環境清單，然後按一下&#x200B;**Hibernate**，如下圖所示：

   ![](assets/hibernate-1b.png)

1. 按一下&#x200B;**Hibernate**&#x200B;確認步驟。

   ![](assets/hibernate-2.png)

1. 當休眠成功時，您會在&#x200B;**開發人員控制台**&#x200B;畫面中看到您環境的休眠程式完成通知。

   ![](assets/hibernate-4.png)


## 取消休眠{#de-hibernation-introduction}

1. 導覽至&#x200B;**Developer Console**。
請參閱[存取開發人員主控台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)，瞭解如何從&#x200B;**環境**&#x200B;卡存取&#x200B;**開發人員主控台**。

   >[!IMPORTANT]
   >直接從Cloud Manager連結至&#x200B;**Developer Console**&#x200B;時，您無法選擇解除沙盒程式環境的休眠。 解決方法是在Developer Console中，將下列模式新增至url `#release-cm-p1234-e5678 where 1234` 1234的結尾是您的&#x200B;*Program ID*，而5678是您的&#x200B;*Environment ID*。

   >[!NOTE]
   >或者，您也可以瀏覽至&#x200B;**Developer Console**&#x200B;以取消休眠，方法是嘗試存取已休眠環境的作者或發佈服務；在此情況下，將會出現著陸頁面，其中包含「開發人員主控台」的連結。 請參閱下面的訪問休眠環境部分。

   >[!IMPORTANT]
   >對Developer Console的存取權限由&#x200B;**Admin Console**&#x200B;中的&#x200B;**雲端管理員——開發人員角色**&#x200B;定義。 具有開發人員角色權限的使用者可以解除沙盒程式環境的休眠。

1. 按一下&#x200B;**De-hibernate** ，如下圖所示：

   ![](assets/de-hibernation-img1.png)

   或,

   按一下左上角的&#x200B;**環境**&#x200B;連結查看環境清單，然後按一下&#x200B;**解除休眠** ，如下圖所示

   ![](assets/de-hibernate-1b.png)


1. 按一下&#x200B;**取消休眠**&#x200B;確認步驟。

   ![](assets/de-hibernation-img2.png)

1. 您將會收到解除休眠程式已啟動的通知，並會隨進度更新。

   ![](assets/de-hibernation-img3.png)

1. 程式完成後，沙盒程式環境將再次激活。

   ![](assets/de-hibernation-img4.png)

### 取消休眠的權限{#permissions-de-hibernate}

任何擁有產品設定檔的使用者AEM，如果是Cloud Service，則應能存取&#x200B;**開發人員主控台(Developer Console)，讓他們解除環境的休眠。**

## 訪問休眠環境{#accessing-hibernated-environment}

當針對休眠環境的作者或發佈層提出任何瀏覽器請求時，使用者會遇到一個說明該環境休眠狀態的登陸頁面，如下圖所示：

![](assets/de-hibernation-img5.png)

## 重要注意事項{#important-considerations}

與冬眠和脫冬眠環境相關的幾項主要考慮事項包括：

* 使用者可使用管道將自訂程式碼部署至休眠的環境。 環境將保持休眠狀態，而新代碼將在解除休眠後出現在環境中。

* 升AEM級可套用至休眠環境，客戶可從Cloud Manager手動觸發。 該環境將保持休眠狀態，新版本將在解除休眠後出現在環境中。

* 沙盒在閒置8小時後會放入休眠節點中，在此之後，它們就可以解除休眠。

* 沙盒在連續休眠模式6個月後即會刪除，然後再重新建立。

   >[!NOTE]
   >目前，Cloud Manager不會指出環境是否已休眠。

## 沙AEM盒環境的更新{#aem-updates-sandbox}

如需詳細資訊，請參AEM閱[版本更新](/help/implementing/deploying/aem-version-updates.md)。

使用者可手動將更AEM新套用至沙盒程式中的環境。

請參閱[更新環境](/help/implementing/cloud-manager/manage-environments.md#updating-dev-environment)以瞭解如何更新環境。

>[!NOTE]
>* 手動更新只能在目標環境具有正確配置的管線時運行。
>* 手動更新&#x200B;*Production*&#x200B;或&#x200B;*Stage*&#x200B;環境將自動更新另一個環境。 Production+Stage環境集必須位於同一版AEM本。

