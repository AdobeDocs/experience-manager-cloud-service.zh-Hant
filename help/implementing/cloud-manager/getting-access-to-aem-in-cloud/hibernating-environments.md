---
title: 休眠和解除休眠沙箱環境
description: 了解沙箱程式的環境如何自動進入休眠模式，以及如何將其解除休眠。
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
source-git-commit: 5cb58b082323293409aad08d4e5dd9289283e0a6
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---


# 休眠和解除休眠沙箱環境 {#hibernating-introduction}

如果連續八小時未檢測到任何活動，沙箱方案的環境將進入休眠模式。休眠是沙箱方案環境所特有的。 生產程式環境不會休眠。

## 休眠 {#hibernation-introduction}

休眠可以自動或手動進行。

* **自動**  — 閒置8小時後，沙箱方案環境會自動休眠。 閒置定義為製作服務或預覽或發佈服務都不會收到請求。
* **手動**  — 身為使用者，您可以手動將沙箱方案環境休眠。 不需要，因為休眠將如前所述自動發生。

沙箱方案環境進入休眠模式可能需要幾分鐘的時間。 資料會在休眠期間保留。

### 使用手動休眠 {#using-manual-hibernation}

您可以從開發人員控制台手動休眠沙箱程式。 Cloud Manager的任何使用者皆可存取沙箱方案的開發人員控制台。

請依照下列步驟，手動將沙箱方案環境休眠。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下要休眠的程式以顯示其詳細資訊。

1. 在 **環境** 卡片上，按一下刪節號按鈕，然後選取 **開發人員控制台**.

   * 請參閱檔案 [存取開發人員控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) 以取得開發人員控制台的其他詳細資訊。

   ![開發人員控制台功能表選項](assets/developer-console-menu-option.png)

1. 在開發人員控制台中，按一下 **休眠**.

   ![休眠按鈕](assets/hibernate-1.png)

1. 按一下 **休眠** 確認步驟。

   ![確認休眠](assets/hibernate-2.png)

休眠成功後，您會在 **開發人員控制台** 螢幕。

![休眠確認](assets/hibernate-4.png)

在開發人員控制台中，您也可以按一下 **環境** 連結上方的階層連結 **Pod** 要休眠的環境清單的下拉式清單。

![要休眠的環境清單](assets/hibernate-1b.png)

## 解除休眠 {#de-hibernation-introduction}

您可以從開發人員控制台手動將沙箱方案休眠。

>[!IMPORTANT]
>
>使用 **開發人員** 角色可將沙箱方案環境解除休眠。

1. 登入Cloud Manager，網址為 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 並選取適當的組織。

1. 按一下要休眠的程式以顯示其詳細資訊。

1. 在 **環境** 卡片上，按一下刪節號按鈕，然後選取 **開發人員控制台**.

   * 請參閱檔案 [存取開發人員控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console) 以取得開發人員控制台的其他詳細資訊。

1. 按一下 **解除休眠**.

   ![解除休眠按鈕](assets/de-hibernation-img1.png)

1. 按一下 **解除休眠** 確認步驟。

   ![確認解除休眠](assets/de-hibernation-img2.png)

1. 您會收到解除休眠程式已開始的通知，並隨進度更新。

   ![休眠進度通知](assets/de-hibernation-img3.png)

1. 程式完成後，沙箱方案環境會再次啟用。

   ![解除休眠完成](assets/de-hibernation-img4.png)


在開發人員控制台中，您也可以按一下 **環境** 連結上方的階層連結 **Pod** 要解除休眠的環境清單的下拉式清單。

![休眠Pod清單](assets/de-hibernate-1b.png)

### 解除休眠的權限 {#permissions-de-hibernate}

任何擁有產品設定檔且可讓其存取AEMas a Cloud Service的使用者，都應該能夠存取 **開發人員控制台**，允許他們將環境解除休眠。

## 存取休眠環境 {#accessing-hibernated-environment}

針對休眠環境的作者、預覽或發佈服務提出任何瀏覽器請求時，使用者會遇到登錄頁面，說明環境的休眠狀態，以及可解除休眠服務的開發人員控制台連結。

![休眠服務登錄頁面](assets/de-hibernation-img5.png)

## 部署和AEM更新 {#deployments-updates}

休眠環境仍可部署及手動升級AEM。

* 使用者可使用管道將自訂程式碼部署至休眠環境。 環境將保持休眠狀態，解除休眠後，新程式碼會顯示在環境中。

* AEM升級可套用至休眠環境，並可從Cloud Manager手動觸發。 環境將保持休眠狀態，解除休眠後，新版本將會顯示在環境中。

## 休眠和刪除 {#hibernation-deletion}

* 沙箱程式中的環境閒置8小時後會自動休眠。
   * 閒置定義為製作服務或預覽或發佈服務都不會收到請求。
   * 休眠後，即可手動解除休眠。
* 沙箱程式在進入連續休眠模式6個月後會遭到刪除，之後可重新建立。
