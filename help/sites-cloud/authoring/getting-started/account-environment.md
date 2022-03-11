---
title: 配置帳戶環境
description: 為AEM您提供了配置帳戶和作者環境某些方面的能力
exl-id: 1b948f0b-85b9-478a-8b7e-61495c1d57b6
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 10%

---

# 配置帳戶環境 {#configuring-your-account-environment}

為您AEM提供了配置帳戶和作者環境某些方面的功能。

使用頁 [首和相關「我的首選項](#user-settings) 」對話框中的「用戶」選項 [](/help/sites-cloud/authoring/getting-started/basic-handling.md#the-header)[](#my-preferences) ，可以修改用戶選項，例如。

從訪問 [用戶](#user-settings) 的子菜單。

## 使用者設定 {#user-settings}

的 **用戶** 設定對話框允許您訪問：

* 模擬為
   * 使用「模擬」功能，用戶可以代表其他用戶工作。 <!--With the [Impersonate as](/help/sites-administering/security.md#impersonating-another-user) functionality, a user can work on behalf of another user.-->
* 設定檔
   * 提供指向用戶設定的方便連結 <!--Offers a convenient link to your [user settings](/help/sites-administering/security.md))-->
* [我的喜好設定](#my-preferences)
   * 指定用戶唯一的各種首選項設定

![用戶設定](/help/sites-cloud/authoring/assets/user-settings.png)

### 我的喜好設定 {#my-preferences}

的 **我的首選項** 對話框通過 [用戶](#user-settings) 的子菜單。

每個用戶都可以為自己設定某些屬性。

![我的喜好設定](/help/sites-cloud/authoring/assets/user-preferences.png)

* **語言**

   這定義了用於創作環境的UI的語言。 從可用清單中選擇所需的語言。

* **視窗管理**

   這定義了行為或開啟窗口。 選擇以下任一項：

   * **多個窗口** （預設）

      * 將在新窗口中開啟頁面。
   * **單一視窗**

      * 將在當前窗口中開啟頁面。


* **顯示資產桌面動態**

   此選項需AEM要案頭應用。

* **附註顏色**

   這定義了在進行注釋時使用的預設顏色。

   * 按一下顏色塊以開啟色板選擇器以選擇顏色。
   * 或者，在欄位中輸入所需顏色的十六進位代碼。

* **相對日期顯示**

   為了提高可讀性AEM，將過去七天內的日期作為相對日期（如三天前）和較早的日期作為確切日期（如2017年3月20日）進行渲染。

   此選項定義系統中日期的顯示方式。 以下選項可用：

   * **始終顯示確切日期**:始終顯示確切日期（從不顯示相對日期）。
   * **1天**:在一天內顯示日期的相對日期，否則顯示確切的日期。
   * **7天（預設）**:在七天內顯示日期的相對日期，否則顯示確切日期。
   * **1個月**:在一個月內顯示日期的相對日期，否則顯示確切日期。
   * **1年**:顯示一年內日期的相對日期，否則顯示確切日期。
   * **始終顯示相對日期**:從不顯示確切日期，只顯示相對日期。

* **啟用快捷方式**

   支AEM持許多使創作更高效的鍵盤快捷鍵。

   * [用於編輯頁面的鍵盤快捷鍵](/help/sites-cloud/authoring/fundamentals/keyboard-shortcuts.md)
   * [控制台的鍵盤快捷鍵](/help/sites-cloud/authoring/getting-started/keyboard-shortcuts.md)

   此選項啟用鍵盤快捷鍵。 預設情況下，它們處於啟用狀態，但可以禁用，例如，如果用戶有某些輔助功能要求，則可以禁用它們。

* **啟用資產首頁**

   僅當系統管理員為整個組織啟用了資產首頁體驗時，此選項才可用。

* **Stock 設定**

   此選項允許指定首選的Adobe Stock配置，並且僅當系統管理員已啟用時才可用 [Adobe Stock整合](/help/assets/aem-assets-adobe-stock.md)。
