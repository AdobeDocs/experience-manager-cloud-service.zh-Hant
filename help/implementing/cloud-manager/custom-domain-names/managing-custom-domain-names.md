---
title: 管理自訂網域名稱
description: 了解如何使用 Cloud Manager 查看、更新、取代和刪除自訂網域名稱。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 8e2fc0d4ee82e79d1a822a528b1a46acce3c192a
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 34%

---


# 管理自訂網域名稱 {#managing-custom-domain-names}

Cloud Manager可讓您編輯、更新、取代和刪除自訂網域名稱。

## 編輯自訂網域名稱設定 {#view-and-update}

在AdobeCloud Manager中，您可能會因為下列原因想要編輯自訂網域名稱設定：

* **切換環境**：若要根據您是提供內容給一般使用者(Publish)還是內部使用者（作者）來套用正確的設定。
* **安全性更新**：若要升級至較新的SSL憑證，以增強安全性或法規遵循目的。
* **變更部署策略**：確保將正確的SSL憑證套用至特定環境，以進行適當的加密和網站存取。

**若要編輯自訂網域名稱組態：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在頁面的左上角，按一下漢堡圖示以顯示左側導覽功能表。
1. 在&#x200B;**服務**&#x200B;標題下，按一下&#x200B;**CDN組態**。
1. 在&#x200B;**CDN設定**&#x200B;頁面上，按一下您要編輯其CDN之資料列結尾的省略符號。
1. 按一下&#x200B;**編輯**。
1. 在&#x200B;**編輯CDN組態**&#x200B;對話方塊中，執行下列動作：
   * 在&#x200B;**層**&#x200B;下拉式清單中，選取您要使用的層(作者或Publish)。
   * 在&#x200B;**SSL憑證**&#x200B;下拉式清單中，選取您要使用的SSL憑證。
1. 按一下&#x200B;**更新**。


## 更新自訂網域名稱的SSL憑證 {#update-cert}

你可以遵循[與檢視和更新自訂網域名稱的相同步驟](#view-and-update)來更新自訂網域名稱的 SSL 憑證。

>[!NOTE]
>
>SSL憑證必須有效，[已設定](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，並包含您要更新的自訂網域名稱。


## 刪除自訂網域名稱 {#deleting}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以使用 Cloud Manager 刪除自訂網域名稱。

### 從所有關聯環境刪除自訂網域名稱 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和方案。

1. 從&#x200B;**總覽**&#x200B;畫面瀏覽至&#x200B;**網域設定**&#x200B;頁面。

1. 識別要刪除自訂網域名稱的列。

1. 按一下該列最右端的省略符號按鈕。

1. 選取&#x200B;**刪除**。

1. 確認您的提交。


### 從特定環境刪除自訂網域名稱 {#delete-cdn-specific}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。
1. 從&#x200B;**概觀**&#x200B;頁面，瀏覽到&#x200B;**環境**&#x200B;畫面。
1. 從&#x200B;**環境**&#x200B;頁面，瀏覽至感興趣環境的詳細資訊畫面。
1. 從網域名稱表格中，識別要刪除自訂網域名稱的列。
1. 按一下該列最右端的省略符號按鈕。
1. 選取&#x200B;**刪除**。
1. 確認您的提交。
