---
title: 休眠和去休眠沙箱環境
description: 了解沙箱程序的環境如何自動進入休眠模式以及如何解除休眠。
exl-id: c0771078-ea68-4d0d-8d41-2d9be86408a4
source-git-commit: 5cb58b082323293409aad08d4e5dd9289283e0a6
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 100%

---


# 休眠和去休眠沙箱環境 {#hibernating-introduction}

如果八小時內未檢測到任何活動，沙箱程序的環境將進入休眠模式。休眠是沙箱計劃環境所獨有的。生產程序環境不會休眠。

## 休眠 {#hibernation-introduction}

休眠可以自動或手動發生。

* **自動的**- 沙箱計劃環境在八小時不活動後自動休眠。不活動被定義為既不創作服務也不預覽或發布服務接收請求。
* **手動**- 作為使用者，您可以手動休眠沙箱計劃環境。不需要這樣做，因為休眠會自動發生，如前所述。

沙箱計劃環境最多可能需要幾分鐘才能進入休眠模式。資料在休眠期間被保留。

### 使用手動休眠 {#using-manual-hibernation}

您可以從開發者控制台手動休眠您的沙箱計劃。Cloud Manager 的任何使用者都可以使用 Access 到沙箱計劃的開發人員控制台。

按照以下步驟手動休眠您的沙箱程序環境。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 點擊要休眠的程序以顯示其詳細資訊。

1. 在&#x200B;**環境**&#x200B;卡，點擊省略符號按鈕並選擇&#x200B;**開發者控制台**。

   * 參考文件[存取開發者控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)有關開發者控制台的更多詳細資訊。

   ![開發者控制台選單選項](assets/developer-console-menu-option.png)

1. 在開發人員控制台中，點擊&#x200B;**休眠**。

   ![休眠按鈕](assets/hibernate-1.png)

1. 點擊&#x200B;**休眠**&#x200B;以確認步驟。

   ![確認休眠](assets/hibernate-2.png)

休眠成功後，您將在&#x200B;**開發人員控制台**&#x200B;畫面。

![休眠確認](assets/hibernate-4.png)

在開發人員控制台中，您還可以點擊&#x200B;**環境**&#x200B;上面階層連結中的連結 **Pod** 要休眠的環境清單的下拉式清單。

![要休眠的環境清單](assets/hibernate-1b.png)

## 取消休眠 {#de-hibernation-introduction}

您可以從開發者控制台手動休眠您的沙箱計劃。

>[!IMPORTANT]
>
>一個使用者&#x200B;**開發人員**&#x200B;角色可以解除沙箱計劃環境的休眠。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 點擊要休眠的程序以顯示其詳細資訊。

1. 在&#x200B;**環境**&#x200B;卡，點擊省略符號按鈕並選擇&#x200B;**開發者控制台**。

   * 參考文件[存取開發者控制台](/help/implementing/cloud-manager/manage-environments.md#accessing-developer-console)有關開發者控制台的更多詳細資訊。

1. 點擊&#x200B;**取消休眠**。

   ![取消休眠按鈕](assets/de-hibernation-img1.png)

1. 點擊&#x200B;**取消休眠**&#x200B;以確認步驟。

   ![確認取消休眠](assets/de-hibernation-img2.png)

1. 您會收到解除休眠過程已開始並隨進度更新的通知。

   ![休眠進度通知](assets/de-hibernation-img3.png)

1. 該過程完成後，沙箱程序環境將再次處於活動狀態。

   ![取消休眠完成](assets/de-hibernation-img4.png)


在開發人員控制台中，您還可以點擊&#x200B;**環境**&#x200B;上面階層連結中的連結 **Pod** 要取消休眠的環境清單的下拉式清單。

![休眠的 pod 清單](assets/de-hibernate-1b.png)

### 取消休眠的權限 {#permissions-de-hibernate}

任何擁有可以存取 AEM as a Cloud Service 產品設定檔的使用者，都應該能夠存取&#x200B;**開發者控制台**，以可讓他們解除環境休眠。

## 存取休眠環境 {#accessing-hibernated-environment}

當向休眠環境的作者、預覽或發布服務發出任何瀏覽器請求時，使用者將遇到一個描述環境休眠狀態的登入頁面以及一個指向開發人員控制台的鏈接，該服務可以在其中解除休眠。

![休眠服務登陸頁面](assets/de-hibernation-img5.png)

## 部署和 AEM 更新 {#deployments-updates}

休眠環境仍允許部署和手動 AEM 升級。

* 使用者可以使用管道將自訂計劃碼部署到休眠環境。環境將保持休眠狀態，一旦解除休眠，新計劃碼將出現在環境中。

* AEM 升級可應用於休眠環境，並可從 Cloud Manager 手動觸發。環境將保持休眠狀態，一旦解除休眠，新發佈內容將出現在環境中。

## 休眠和刪除 {#hibernation-deletion}

* 沙箱計劃內的環境在八小時不活動後自動休眠。
   * 不活動被定義為既不創作服務也不預覽或發布服務接收請求。
   * 一旦休眠，它們可以手動解除休眠。
* 沙箱程序在處於連續休眠模式六個月後被刪除，之後可以重新建立它們。
