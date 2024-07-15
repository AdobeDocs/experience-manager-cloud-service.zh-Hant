---
title: 設定帳戶環境
description: Adobe Experience Manager (AEM)提供您設定帳戶與製作環境某些方面的功能。
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 5%

---

# 設定帳戶環境 {#configuring-your-account-environment}

Adobe Experience Manager (AEM)提供您設定帳戶與製作環境某些方面的功能。

使用頁 [首和相關「我的首選項](#user-settings) 」對話框中的「用戶」選項 [](/help/sites-cloud/authoring/basic-handling.md#the-header)[](#my-preferences) ，可以修改用戶選項，例如。

首先，存取標頭中的[使用者](#user-settings)選項。

## 用戶設定 {#user-settings}

**使用者**&#x200B;設定對話方塊可讓您存取：

* 模擬為
   * 藉助「模擬為」功能，使用者可以代表其他使用者工作。<!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* 設定檔
   * 它提供您使用者設定<!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->的便利連結
* [我的喜好設定](#my-preferences)
   * 指定使用者專屬的各種偏好設定設定

![使用者設定](/help/sites-cloud/authoring/assets/user-settings.png)

### 我的喜好設定 {#my-preferences}

透過標題中的[使用者](#user-settings)選項存取&#x200B;**我的偏好設定**&#x200B;對話方塊。

每個使用者都可以設定自己的偏好屬性。

![我的喜好設定](/help/sites-cloud/authoring/assets/user-preferences.png)

* **語言**

  這會定義用於編寫環境UI的語言。 從可用清單中選取所需的語言。

* **視窗管理**

  這會定義開啟視窗的行為。 選取：

   * **多個Windows** （預設）

      * 頁面會在新視窗中開啟。

   * **單一視窗**

      * 頁面會在目前視窗中開啟。

* **顯示Assets的案頭動作**

  此選項需要AEM案頭應用程式才能使用。

* **註解色彩**

  這會定義製作註解時使用的預設顏色。

   * 按一下顏色區塊，即可開啟色票選取器以選取顏色。
   * 或者，在欄位中輸入所需顏色的十六進位代碼。

* **相對日期顯示**

  為了改善可讀性，AEM會將過去七天內的日期轉譯為相對日期（例如3天前），並將較舊的日期轉譯為確切日期（例如2017年3月20日）。

  此選項定義系統中日期的顯示方式。 下列選項可供使用：

   * **一律顯示確切日期**：一律顯示確切日期（從不顯示相對日期）。
   * **1天**：對於一天內的日期會顯示相對日期，否則會顯示確切日期。
   * **7天（預設）**：對於七天內的日期會顯示相對日期，否則會顯示確切日期。
   * **1個月**：會顯示一個月內日期的相對日期，否則會顯示確切日期。
   * **1年**：對於一年內的日期顯示相對日期，其他情況則顯示確切日期。
   * **一律顯示相對日期**：絕對不會顯示確切日期，只會顯示相對日期。

* **啟用捷徑**

  AEM支援各種鍵盤快速鍵，讓撰寫更有效率。

   * [用於編輯頁面的鍵盤快速鍵](/help/sites-cloud/authoring/page-editor/keyboard-shortcuts.md)
   * [主控台的鍵盤快速鍵](/help/sites-cloud/authoring/sites-console/keyboard-shortcuts.md)

  此選項可啟用鍵盤快速鍵。 預設會啟用這些功能，但也可以停用，例如，如果使用者有特定的協助工具要求。

* **啟用Assets首頁**

  只有在系統管理員已針對整個組織啟用Assets首頁體驗時，才可使用此選項。

* **庫存組態**

  此選項可讓您指定偏好的Adobe Stock組態，而且只有在您的系統管理員已啟用[Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)時才能使用。
