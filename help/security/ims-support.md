---
title: Adobe Experience Manager as a Cloud Service 的 IMS 支援
description: Adobe Experience Manager as a Cloud Service 的影像管理系統支援。
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
feature: Security
role: Admin
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: ht
source-wordcount: '1941'
ht-degree: 100%

---

# Adobe Experience Manager as a Cloud Service 的 IMS 支援 {#ims-support-for-aem-as-a-cloud-service}

## 簡介 {#introduction}

* AEM as a Cloud Service 包含適用於 AEM 執行個體和 Adobe 身分管理系統 (簡稱 IMS) 驗證的 Admin Console 支援。
* Admin Console 可讓管理員集中管理所有 Experience Cloud 使用者。
* 管理員可將使用者和群組指派給與 AEM as a Cloud Service 執行個體相關聯的產品設定檔，讓他們能登入該執行個體。

>[!TIP]
>
>請參閱[為管理員設定 AEM 存取權](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem_zh-hant)，了解使用者如何使用 Adobe IMS 向 AEM as a Cloud Service 進行驗證，同時了解如何使用 Adobe IMS 使用者、使用者群組和產品設定檔來控制對 AEM 及其特性和功能的存取。需要 Adobe ID。

## 重要焦點 {#key-highlights}

AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。不支援客戶網站的外部使用者，例如網站訪客。

* Admin Console 會在產品內容執行個體環境中，將客戶顯示為 IMS 組織、編寫和發佈執行個體。如此，系統和產品管理員就能妥善管理執行個體的存取權限。
* Admin Console 中的產品設定檔能決定使用者可存取的執行個體。
* 客戶可使用符合 SAML 2 的身分服務供應商 (簡稱 IDP)，完成單一登入程序。
* 僅支援客戶以 Enterprise ID 或 Federated ID 進行單一登入，不支援個人 Adobe ID。

## 架構 {#architecture}

IMS 驗證採用 OAuth 通訊協定，能在 AEM 和 Adobe IMS 端點之間運作。使用者加入 IMS 並擁有 Adobe 身分後，就能使用 IMS 憑證登入 AEM 編寫服務。

使用者登入流程如下所示，系統會將使用者重新導向至 IMS，並可選擇重新導向至客戶 IDP 以進行 SSO，然後重新導向回 AEM。

![IMS 架構](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### 在 Adobe Admin Console 中佈建組織 {#onboarding-orgs-to-adobe-admin-console}

若要使用 Adobe IMS 進行 AEM 驗證，客戶必須先開始使用 Adobe Admin Console。

首先，客戶必須有佈建在 Adobe IMS 的組織。Adobe 企業客戶在 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 中會顯示為 IMS 組織。此區域是 Adobe 客戶用來管理使用者和群組之產品權益的門戶。

AEM 客戶應先有已佈建的組織，而在 IMS 佈建過程中，客戶即可在 Admin Console 中使用客戶執行個體，管理使用者權益和存取權限。

客戶成為 IMS 組織後，即可依以下摘要內容設定其系統：

![IMS 上線](/help/security/assets/ims2.png)

1. 指定的系統管理員會收到 Cloud Manager 的登入邀請函。登入 Cloud Manager 後，系統管理員可以選擇佈建 AEM 程序和環境，或導覽至 Admin Console 執行管理任務。
1. 系統管理員需先宣告網域，以確認各別網域的所有權 (例如，acme.com)
1. 系統管理員設定使用者目錄
1. 系統管理員在 Admin Console 中執行 IDP 設定，以設定單一登入。
1. AEM 管理員可照常管理本機群組、權限與高階權限。

[設定身分和單一登入](https://helpx.adobe.com/tw/enterprise/using/set-up-identity.html)中介紹包括 IDP 設定在內的 Adobe Identity Management 基礎知識。

[「歡迎使用企業和團隊管理指南」](https://helpx.adobe.com/tw/enterprise/admin-guide.html)中介紹企業管理和 Admin Console 的使用。

### 在 Admin Console 中建立使用者 {#onboarding-users-in-admin-console}

有三種建立使用者的方法。每種方法取決於客戶的規模及偏好設定。您可以在 Admin Console 中手動建立使用者、上傳 .csv 檔案，或從客戶的企業 Active Directory 同步使用者。

**透過 Admin Console UI 手動新增**

客戶可在 Admin Console UI 中手動建立使用者和群組。如果不需管理很多使用者，可使用此方法。舉例來說，如果 AEM 使用者少於 50 名，或您已使用此方法管理其他 Adobe 產品 (例如 Analytics、Target 或 Creative Cloud 應用程式)，即適合使用這個方法。

![使用者上線](/help/security/assets/ims3.png)

**在 Admin Console UI 中上傳檔案**

為方便建立使用者，可上傳 `.csv` 檔案，大量新增使用者。

![檔案上傳](/help/security/assets/ims4.png)

**使用者同步工具**

使用者同步工具 (簡稱 UST) 可方便 Adobe 企業客戶使用 Active Directory 建立及管理 Adobe 使用者。此 UST 也適用於其他通過測試的 OpenLDAP 目錄服務。目標使用者是 IT 身分管理員 (企業目錄或系統管理員)，我們能協助他們安裝及設定此工具。此開放原始碼工具可供自訂，客戶可依自身的特定需求加以修改。

執行「使用者同步」時，系統會從組織的 Active Directory 擷取使用者清單，比對 Admin Console 中的使用者清單。接著，系統會呼叫 Adobe User Management API，將 Admin Console 與組織的目錄同步。此變更流程無法復原。在 Admin Console 中完成的任何編輯都不會推送至目錄。

此工具可讓系統管理員將客戶目錄中的使用者群組，與 Admin Console 中的產品設定和使用者群組相互對應。

若要設定「使用者同步」，組織必須先透過與 [User Management API](https://developer.adobe.com/umapi/) 相同的使用方式，建立一組憑證。

![使用者同步工具](/help/security/assets/ims5.png)

使用者同步工具是透過[在此位置](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.9.0rc2)的 Adobe Github 存放庫發佈。

>[!NOTE]
>
>預發行版本 **2.4RC1** 可透過 [GitHub 上的使用者同步工具 v2.4rc1](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1) 提供的建立動態群組支援取得。

此版本的主要功能是在 Admin Console 中針對使用者會籍動態對應新 LDAP 群組，以及建立動態使用者群組。

有關新群組功能的更多資訊，請參閱[「Adobe 使用者同步工具 - 其他群組選項」](https://adobe-apiplatform.github.io/user-sync.py/en/user-manual/advanced_configuration.html#additional-group-options)。

**使用者同步文件**

請參閱：

* [UST 文件](https://adobe-apiplatform.github.io/user-sync.py/en/)

* 使用者同步工具必須透過 [API 存取權驗證](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)中的程序，註冊為 Adobe Developer 用戶端 UMAPI。

* [Adobe Developer Console 文件](https://developer.adobe.com/developer-console/)

* [使用者同步工具所採用的 User Management API](https://adobe-apiplatform.github.io/user-sync.py/en/)

## Adobe Experience as a Cloud Service 設定 {#aem-configuration}

>[!NOTE]
>
>佈建 AEM 環境和執行個體時，系統會自動設定所需的 AEM IMS 設定。不過，管理員可依其需求進行修改，請參閱[「部署至 AEM as a Cloud Service」](/help/implementing/deploying/overview.md)。

佈建 AEM 環境和執行個體時，系統會自動設定所需的 AEM IMS 設定。客戶管理員可依需求適度修改部分設定

整體方式是將 Adobe IMS 設為 OAuth 提供者，並像處理 LDAP 同步作業一樣，修改 **Apache Jackrabbit Oak Default Sync Handler**。

以下提供必須修改的重要 OSGI 設定，以變更「使用者自動成員資格」或「群組對應」等屬性。

<!-- Arun to provide list of osgi configs -->

## 使用方式 {#how-to-use}

### 在 Admin Console 中管理產品和使用者存取權限 {#managing-products-and-user-access-in-admin-console}

產品管理員登入 Admin Console 後，會看到 AEM as a Cloud Service 產品內容的多個執行個體，如下所示：例如，從「**概觀**」頁面選取任何產品：

![執行個體登入](/help/security/assets/ims6.png)

您會看到現有執行個體清單：

![執行個體登入 2](/help/security/assets/ims7.png)

在每個產品內容執行個體下，會有跨生產、階段或開發環境的編寫或發佈服務的執行個體。每個執行個體會關聯到產品設定檔或 Cloud Manager 角色。這些產品設定檔的主要功用在於指派存取權限給具有必要權限的使用者和群組。

**AEM Administrators_xxx** 設定檔用於授予相關聯 AEM 執行個體的管理員權限，而 **AEM Users_xxx** 設定檔則用於新增使用者。

此產品設定檔中新增的任何使用者和群組都可以登入該執行個體，如以下範例所示：

![產品設定檔](/help/security/assets/ims8.png)

>[!WARNING]
>
>請勿變更 **AEM 管理員**&#x200B;產品設定檔名稱。如果變更 **AEM 管理員**&#x200B;產品設定檔名稱，會將所有指派到該設定檔之使用者的管理員權限移除。

### 登入 Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**本機管理員登入**

AEM 可繼續為管理員使用者支援本機登入。此登入畫面可讓您本機登入：

![本機登入](/help/security/assets/ims9.png)

<!-- the above image must be updated for skyline -->

**IMS 登入**

若是其他使用者，在執行個體上設定 IMS 後，即可使用 IMS 登入。使用者按一下「使用 Adobe 登入」按鈕，如下所示：

![IMS 登入](/help/security/assets/ims10.png)


>[!NOTE]
>
>在 IMS 中建立的任何使用者都可使用 Adobe ID 或 Federated ID 來建立。若是使用 Federated ID 設定使用者，使用者需透過公司合作之身分服務供應商登入，以完成驗證。

系統會將使用者重新導向至 IMS 登入畫面，此時使用者必須輸入憑證：

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

如下所示，群組 **AEM-GRP_008** 會繼承 **DAM 使用者** 的權限。這種繼承可有效管理同步群組的權限，此外也常搭配 LDAP 驗證方法使用。

![ACL3](/help/security/assets/ims18.png)


### 存取 Cloud Manager {#accessing-cloud-manager}

若要能夠存取 Cloud Manager 或 AEM as a Cloud Service 環境，系統必須將您指派到 Cloud Manager 產品的設定檔。

如果您想深入了解使用者的角色 (能控制使用者能否使用 Cloud Manager 的特定功能)，請參閱角色定義。

>[!NOTE]
>Cloud Manager 已預先設定角色，賦予適當權限。若要了解各個具有特定權限的角色、預先設定的任務或每個角色的相關權限，請參閱[角色型權限](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions)。

**使用者新增步驟**

1. 您可從現有使用者或新使用者的畫面，將使用者新增至特定設定檔。

1. 或者，您也可以在&#x200B;**「綜覽」**&#x200B;畫面新增使用者，如下圖所示。

   ![ACL3](/help/security/assets/ims23.png)

   >[!NOTE]
   >您可以指派多個設定檔給同一個使用者，如下圖所示。

   ![ACL3](/help/security/assets/ims22.png)


1. 使用者新增至適當的設定檔後，應該就能從使用者介面的右上角，透過 [Adobe Experience Cloud](https://my.cloudmanager.adobe.com) 存取 Cloud Manager 的個別租用戶。


### 存取 AEM as a Cloud Service 中的執行個體 {#accessing-instance-cloud-service}

>[!IMPORTANT]
>您必須先完成前述章節所提及的步驟，才能取得 AEM as a Cloud Service 執行個體的存取權限。

若要在 **Admin Console** 中存取 AEM 執行個體，您應該會在 **Admin Console** 的產品清單中看見 Cloud Manager 程式和程式內的環境。

舉例來說，在下方螢幕擷圖中，您會看到兩個可供使用的環境，即 *dev author* 和 *publish*。

![ACL3](/help/security/assets/ims19.png)

若要存取 AEM 執行個體，使用者必須新增至適當雲端服務產品群組。

每個編寫執行個體都會有 AEM 管理員和 AEM 使用者設定檔，而每個發佈執行個體都有 AEM 使用者設定檔。您可以視需求新增其他設定檔。

若要取得管理員層級的 AEM 執行個體存取權限，使用者需新增至特定產品的 AEM 管理員設定檔。
