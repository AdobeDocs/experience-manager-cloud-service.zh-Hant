---
title: Adobe Experience Manager as a Cloud Service 的 IMS 支援
description: Adobe Experience Manager as a Cloud Service 的 IMS 支援
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
translation-type: tm+mt
source-git-commit: 460cefde9a203b4237aedf01b01e026d37eadfe6
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 95%

---

# Adobe Experience Manager as a Cloud Service 的 IMS 支援 {#ims-support-for-aem-as-a-cloud-service}

## 簡介 {#introduction}

* AEM as a Cloud Service 包含適用於 AEM 例項和 Adobe 身分管理系統 (簡稱 IMS) 驗證的 Admin Console 支援。
* Admin Console 可讓管理員集中管理所有 Experience Cloud 使用者。
* 管理員可將使用者和群組指派給與 AEM as a Cloud Service 例項相關聯的產品設定檔，讓他們能登入該例項。

## 重要焦點 {#key-highlights}

AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。不支援客戶網站的外部使用者，例如網站訪客。

* Admin Console 會在產品內容例項環境中，將客戶顯示為 IMS 組織、作者和發佈例項。這樣一來，系統和產品管理員就能妥善管理例項的存取權限。
* Admin Console 中的產品設定檔能決定使用者可存取的例項。
* 客戶可使用符合 SAML 2 的身分服務供應商 (簡稱 IDP)，完成單一登入程序。
* 僅支援客戶以 Enterprise ID 或 Federated ID 進行單一登入，不支援個人 Adobe ID。

## 架構 {#architecture}

IMS 驗證採用 OAuth 通訊協定，能在 AEM 和 Adobe IMS 端點之間運作。使用者加入 IMS 並擁有 Adobe 身分後，就能使用 IMS 憑證登入 AEM 作者服務。

使用者登入流程如下所示，系統會將使用者重新導向至 IMS，並可選擇重新導向至客戶 IDP 以進行 SSO，然後重新導向回 AEM。

![IMS 架構](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### 在 Adobe Admin Console 中佈建組織{#onboarding-orgs-to-adobe-admin-console}

若要使用 Adobe IMS 進行 AEM 驗證，客戶必須先開始使用 Adobe Admin Console。

首先，客戶需有佈建於 Adobe IMS 的組織。Adobe 企業客戶在 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 中會顯示為 IMS 組織。Adobe 客戶可使用此入口網站管理使用者和群組的產品權益。

AEM 客戶應先佈建組織，而在 IMS 佈建過程中，客戶即可在 Admin Console 中使用客戶例項，管理使用者權益和存取權限。

客戶成為 IMS 組織後，即可依以下摘要內容設定其系統：

![IMS 入門](/help/security/assets/ims2.png)

1. 指定的系統管理員會收到 Cloud Manager 的登入邀請函。登入 Cloud Manager 後，系統管理員可以選擇佈建 AEM 方案和環境，或導覽至 Admin Console 執行管理任務。
1. 系統管理員需先宣告網域，以確認各別網域的所有權 (例如 acme.com)
1. 系統管理員設定使用者目錄
1. 系統管理員在 Admin Console 中執行 IDP 設定，以設定單一登入。
1. AEM 管理員可照常管理本機群組和權限。

[此文件](https://helpx.adobe.com/tw/enterprise/using/set-up-identity.html)說明 Adobe 身分管理基本知識，包括 IDP 設定。

[此文件](https://helpx.adobe.com/tw/enterprise/managing/user-guide.html)說明企業管理和 Admin Console 使用方式。

### 在 Admin Console 中建立使用者 {#onboarding-users-in-admin-console}

根據客戶的規模及偏好設定，建立使用者共有三種方式：在 Admin Console 中手動建立使用者、上傳 .csv 檔案，或從客戶的企業 Active Directory 同步使用者。

**透過 Admin Console UI 手動新增**

客戶可在 Admin Console UI 中手動建立使用者和群組。如果不需管理大量使用者，可使用此方法。舉例來說，如果 AEM 使用者少於 50 名 ，或您已使用此方法管理其他 Adobe 產品 (例如 Analytics、Target 或 Creative Cloud 應用程式)，即適合使用這個方法。

![使用者上線](/help/security/assets/ims3.png)

**在 Admin Console UI 中上傳檔案**

為方便建立使用者，可上傳 `.csv` 檔案，大量新增使用者。

![檔案上傳](/help/security/assets/ims4.png)

**使用者同步工具**

使用者同步工具 (簡稱 UST) 可方便我們的企業客戶使用 Active Directory 建立及管理 Adobe 使用者。此工具也適用於其他通過測試的 OpenLDAP 目錄服務。目標使用者是 IT 身分管理員 (企業目錄或系統管理員)，我們能協助他們安裝及設定此工具。此開放原始碼工具可供自訂，客戶可依自身的特定需求加以修改。

執行「使用者同步」時，系統會從組織的 Active Directory 擷取使用者清單，比對 Admin Console 中的使用者清單。接著，系統會呼叫 Adobe User Management API，將 Admin Console 與組織的目錄同步。此變更流程無法復原。在 Admin Console 中完成的任何編輯都不會推送至目錄。

此工具可協助系統管理員將客戶目錄中的使用者群組，與 Admin Console 中的產品設定和使用者群組相互對應。

若要設定「使用者同步」，組織需先透過與 [User Management API](https://www.adobe.io/apis/experienceplatform/umapi-new.html) 相同的使用方式，建立一組憑證。

![使用者同步工具](/help/security/assets/ims5.png)

使用者同步工具是透過 [Adobe Github 存放庫](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)提供使用。

>[!NOTE]
>
>搶鮮版 **2.4RC1** 提供建立動態群組的相關支援，可從[此處](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)取得。

此版本的主要功能是能在 Admin Console 中動態對應新 LDAP 群組，以取得使用者成員資格，並且建立動態使用者群組。

若需新群組功能的詳細資訊，請參閱[此處](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)。

**使用者同步文件**

如需詳細資訊，請參閱 [UST 文件](https://adobe-apiplatform.github.io/user-sync.py/en/)。

使用者同步工具必須透過[此處](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)的程序，註冊為 Adobe I/O 用戶端 UMAPI。

若需 Adobe I/O Console 文件，請前往[此處](https://www.adobe.io/apis/cloudplatform/console.html)。

[此文件](https://www.adobe.io/apis/cloudplatform/umapi-new.html)說明使用者同步工具所採用的 User Management API。

## Adobe Experience as a Cloud Service 設定 {#aem-configuration}

>[!NOTE]
>
>佈建 AEM 環境和例項時，系統會自動設定所需的 AEM IMS 設定。不過，管理員可透過[此處](/help/implementing/deploying/overview.md)所述方法，依需求適度修改。

佈建 AEM 環境和例項時，系統會自動設定所需的 AEM IMS 設定。客戶管理員可依需求適度修改部分設定

整體方式是將 Adobe IMS 設為 OAuth 提供者，並像處理 LDAP 同步作業一樣，修改 **Apache Jackrabbit Oak Default Sync Handler**。

以下提供需修改的重要 OSGI 設定，以變更「使用者自動成員資格」或「群組對應」等屬性。

<!-- Arun to provide list of osgi configs -->

## 使用方式 {#how-to-use}

### 在 Admin Console 中管理產品和使用者存取權限 {#managing-products-and-user-access-in-admin-console}

當產品管理員登入Admin Console時，他們會將多個例項視為AEMCloud Service產品內容，如下所示。 例如，從&#x200B;**概述**&#x200B;頁面選擇任何產品：

![例項登入](/help/security/assets/ims6.png)

您會看到現有例項的清單：

![例項登入 2](/help/security/assets/ims7.png)

在每個「產品內容」例項下，都會有跨生產、舞台或開發環境的「作者」或「發佈」服務執行個體。 每個實例都與「產品配置檔案」或「雲端管理員」角色關聯。 這些產品設定檔可用來指派具有必要權限的使用者和群組存取權。

**Administrator_xxx** 設定檔可授與相關聯 AEM 例項的管理員權限，而 **User_xxx** 設定檔則可新增一般使用者。

此產品設定檔中新增的任何使用者和群組都可以登入該特定例項，如以下範例所示：

![產品設定檔](/help/security/assets/ims8.png)

### 登入 Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**本機管理員登入**

AEM 可繼續為管理員使用者支援本機登入。從登入畫面可選擇本機登入：

![本機登入](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS 登入**

若是其他使用者，在例項上設定 IMS 後，即可使用 IMS 登入。使用者需先按一下「使用 Adobe 登入」按鈕，如下所示：

![IMS 登入](/help/security/assets/ims10.png)


>[!NOTE]
>
>在 IMS 中建立的任何使用者都可使用 Adobe ID 或 Federated ID 來建立。若是使用 Adobe ID 設定使用者，使用者需透過公司合作之身分服務供應商登入，以完成身分驗證。

接著，系統會將使用者重新導向至 IMS 登入畫面，此時使用者需輸入憑證：

![IMS 登入 2](/help/security/assets/ims11.png)

![IMS 登入 3](/help/security/assets/ims12.png)

如果在初始 Admin Console 設定期間就已設定同盟 IDP，系統會將使用者重新導向至客戶 IDP，以執行 SSO：

![IMS 登入 4](/help/security/assets/ims13.png)

驗證完成後，系統會將使用者重新導向回 AEM 並登入：

![IMS 登入 5](/help/security/assets/ims14.png)

### 在 Adobe Experience Manager as a Cloud Service 中管理權限和 ACL {#managing-permissions-in-aem}

您能持續在 AEM 中管理 ACL 和權限。您可將從 IMS 同步的使用者群組，指派給定義 ACL 和權限的本機群組。

以下範例中，我們會示範將同步的群組新增至本機 **Dam_Users** 群組。

使用者屬於 IMS 中的下列群組：

![ACL1](/help/security/assets/ims15.png)

使用者登入後，系統會同步其群組成員資格，如下所示：

![ACL2](/help/security/assets/ims16.png)

在 AEM 中，從 IMS 同步的使用者群組可以成員身分新增至現有的本機群組，例如 **DAM Users**。

![ACL3](/help/security/assets/ims17.png)

如下所示，群組 **AEM-GRP_008** 會繼承 **DAM Users** 的權限，以這種方式管理同步群組權限的效果很棒，此外也常搭配 LDAP 驗證方法使用。

![ACL3](/help/security/assets/ims18.png)


### 存取 Cloud Manager {#accessing-cloud-manager}

若要能夠存取 Cloud Manager 或 AEM as a Cloud Service 環境，系統必須將您指派給 Cloud Manager 產品的設定檔。

請參閱角色定義深入了解使用者的角色，這些角色能控制使用者能否使用 Cloud Manager 的特定功能。

>[!NOTE]
>Cloud Manager 已預先設定角色，賦予適當權限。若要了解各個具有特定權限的角色、預先設定的任務或每個角色的相關權限，請參閱[角色型權限](https://docs.adobe.com/content/help/zh-Hant/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html)。

**使用者新增步驟**

1. 您可從現有使用者或新使用者的畫面，將使用者新增至特定設定檔。

1. 或者，您也可以在&#x200B;**「綜覽」**&#x200B;畫面新增使用者，如下圖所示。

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >您可以指派多個設定檔給同一個使用者，如下圖所示。

   ![ACL3](/help/security/assets/ims22.png)


1. 使用者新增至適當的設定檔後，應該就能從使用者介面的右上角，透過 [Adobe Experience Cloud](http://my.cloudmanager.adobe.com) 存取 Cloud Manager 的個別租用戶。


### 存取 AEM as a Cloud Service 中的例項 {#accessing-instance-cloud-service}

>[!IMPORTANT]
>您必須先完成前述章節所提及的步驟，才能取得 AEM as a Cloud Service 例項的存取權限。

若要在 **Admin Console** 中存取 AEM 例項，您應該會在 **Admin Console** 的產品清單中看見 Cloud Manager 程式和程式內的環境。

舉例來說，在下方螢幕截圖中，您會看到兩個可供使用的環境，即 *dev author* 和 *publish*。

![ACL3](/help/security/assets/ims19.png)

若要存取 AEM 例項，使用者必須新增至適當雲端服務產品群組。

每個作者例項都會有 AEM 管理員和 AEM 使用者設定檔，而每個發佈例項都有 AEM 使用者設定檔。您可以視需求新增其他設定檔。

若要取得管理員層級的 AEM 例項存取權限，使用者需新增至特定產品的 AEM 管理員設定檔。
