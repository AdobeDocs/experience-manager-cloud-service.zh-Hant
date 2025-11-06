---
title: 管理自訂網域名稱
description: 了解如何使用 Cloud Manager 查看、更新、取代和刪除自訂網域名稱。
exl-id: 6cab8cf2-22c0-4f4b-9c54-a1425e74ddd0
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 21%

---


# 管理自訂網域名稱 {#managing-custom-domain-names}

Cloud Manager可讓您編輯、更新、取代、驗證和刪除自訂網域名稱。

## 編輯自訂網域名稱設定 {#view-and-update}

在Adobe Cloud Manager中，您可能會因為下列原因想要編輯自訂網域名稱設定：

* **切換環境**：若要根據您是提供內容給一般使用者（發佈）還是內部使用者（作者）來套用正確的設定。
* **安全性更新**：若要升級至較新的SSL憑證，以增強安全性或法規遵循目的。
* **變更部署策略**：確保將正確的SSL憑證套用至特定環境，以進行適當的加密和網站存取。

**若要編輯自訂網域名稱組態：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織。

1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」控制台中，選取程式。

1. 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。

1. 在&#x200B;**服務**&#x200B;標題下，按一下![社交網路圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **網域對應**。

1. 在&#x200B;**網域對應**&#x200B;頁面上，在您要編輯其CDN的資料列結尾按一下![顯示功能表圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 按一下「**編輯**」。

1. 在&#x200B;**編輯網域組態**&#x200B;對話方塊中，執行下列動作：

   * 在&#x200B;**層**&#x200B;下拉式清單中，選取您要使用的層（發佈或預覽）。
   * 在&#x200B;**SSL憑證**&#x200B;下拉式清單中，選取您要使用的SSL憑證。

1. 按一下&#x200B;**更新**。


## 更新自訂網域名稱的SSL憑證 {#update-cert}

按照上述相同步驟更新自訂網域名稱的SSL憑證。

>[!NOTE]
>
>SSL憑證必須有效，[已設定](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md)，並包含您要更新的自訂網域名稱。


## 驗證自訂網域名稱 {#verify-custom-domain-name}

另請參閱[新增自訂網域名稱](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)。

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。

1. 從&#x200B;**總覽**&#x200B;畫面瀏覽至&#x200B;**網域設定**&#x200B;頁面。

1. 識別您要驗證的自訂網域名稱列。

1. 按一下該列最右端的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 在下拉式功能表中，按一下&#x200B;**驗證**。

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，在&#x200B;**您打算搭配此網域使用哪種憑證型別？**&#x200B;下拉式清單，選取下列其中一個選項：

   | 憑證型別選項 | 說明 |
   | --- | --- |
   | Adobe Managed (DV) SSL憑證 | 如果您要使用DV （網域驗證）憑證，請選取此憑證型別。 此選項適用於大多數的情況，可提供基本網域驗證。 Adobe會自動管理和更新憑證。 |
   | 客戶管理的(OV/EV) SSL憑證 | 如果您想要使用EV/OV SSL憑證來保護網域，請選取此憑證型別。 此選項提供OV （組織驗證）或EV （延伸驗證）的增強式安全性。 若需要更嚴格的驗證、更高的信任層級或自訂的憑證控制，請使用。 |

1. 在&#x200B;**驗證網域**&#x200B;對話方塊中，根據您選取的憑證型別，執行下列其中一項作業：

   | 如果您選取憑證型別 | 說明 |
   | --- | ---  |
   | Adobe 管理的憑證 | a.完成[Adobe管理的憑證步驟](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-steps)。 當您完成&#x200B;**驗證網域**&#x200B;對話方塊中的步驟時，請按一下&#x200B;**驗證**。<ul><li>由於 DNS 傳播延遲，DNS 驗證可能需要幾個小時才能完成。</li><li>Cloud Manager最終會驗證網域名稱所有權，並更新&#x200B;**網域設定**&#x200B;資料表中的狀態。 如需詳細資訊，請參閱[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li>![驗證網域狀態](/help/implementing/cloud-manager/assets/domain-settings-verified.png)</li></ul>b.您現在已準備好[新增Adobe Managed (DV) SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-adobe-managed-ssl-cert)。</li></ul> |
   | 客戶管理的憑證 | a.按一下&#x200B;**確定**。<br>b。您現在已準備好[新增客戶管理的(OV/EV) SSL憑證](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#add-customer-managed-ssl-cert)。<br>新增憑證後，您的網域名稱在&#x200B;**網域設定**&#x200B;表格中標示為已驗證。 如需詳細資訊，請參閱[檢查自訂網域名稱狀態](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md)。</li></ul><br>![驗證客戶管理的 EV/OV 憑證的網域](/help/implementing/cloud-manager/assets/verify-domain-customer-managed-step.png) |


## 從所有關聯環境刪除自訂網域名稱 {#deleting}

具有&#x200B;**業務負責人**&#x200B;或&#x200B;**部署管理員**&#x200B;角色的使用者可以使用 Cloud Manager 刪除自訂網域名稱。

### 從所有關聯環境刪除自訂網域名稱 {#delete-cdn-all}

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，並選取適當的組織和方案。

1. 從&#x200B;**總覽**&#x200B;畫面瀏覽至&#x200B;**網域設定**&#x200B;頁面。

1. 識別要刪除自訂網域名稱的列。

1. 按一下該列最右端的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 選取&#x200B;**刪除**。

1. 確認您的提交。


### 從特定環境刪除自訂網域名稱 {#delete-cdn-specific}

>[!WARNING]
>
>在&#x200B;*刪除Cloud Manager中的網域之前，先透過您的DNS提供者移除網域的DNS記錄*。 捨棄的（懸浮） DNS專案可能會被劫持並帶來安全性風險。

**若要從特定環境刪除自訂網域名稱：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager 並選取適當的組織和計畫。

1. 從&#x200B;**概觀**&#x200B;頁面瀏覽到&#x200B;**環境**&#x200B;畫面。

1. 從&#x200B;**環境**&#x200B;頁面，瀏覽至感興趣環境的詳細資訊畫面。

1. 從「網域對應」表格中，識別要刪除自訂網域名稱的列。

1. 按一下該列最右端的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。

1. 選取&#x200B;**刪除**。

1. 確認您的提交。
