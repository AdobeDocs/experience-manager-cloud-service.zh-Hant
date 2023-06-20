---
title: Adobe Experience Manager as a Cloud Service 的 IMS 支援
description: Adobe Experience Manager as a Cloud Service 的 IMS 支援
exl-id: fb563dbd-a761-4d83-9da1-58f8e462b383
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '2035'
ht-degree: 80%

---

# Adobe Experience Manager as a Cloud Service 的 IMS 支援 {#ims-support-for-aem-as-a-cloud-service}

## 簡介 {#introduction}

* AEM as a Cloud Service 包含適用於 AEM 執行個體和 Adobe 身分管理系統 (簡稱 IMS) 驗證的 Admin Console 支援。
* Admin Console 可讓管理員集中管理所有 Experience Cloud 使用者。
* 管理員可將使用者和群組指派給與 AEM as a Cloud Service 執行個體相關聯的產品設定檔，讓他們能登入該執行個體。

>[!TIP]
>
>查看我們的 Experience League 課程[為管理員設定 AEM 存取權](https://experienceleague.adobe.com/?recommended=ExperienceManager-A-1-2020.1.aem)，了解使用者如何使用 Adobe IMS 向 AEM as a Cloud Service 進行驗證，以及如何使用 Adobe IMS 使用者、使用者群組和產品設定檔來控制對 AEM 及其特性和功能的存取。需要 Adobe ID。

>[!NOTE]
>
>AEM 目前不支援指派群組到設定檔。應單獨新增使用者。

## 重要焦點 {#key-highlights}

AEM as a Cloud Service 僅針對「作者」、「管理員」和「開發」使用者提供 IMS 驗證支援。不支援客戶網站的外部使用者，例如網站訪客。

* Admin Console 會在產品內容執行個體環境中，將客戶顯示為 IMS 組織、作者和發佈執行個體。這樣一來，系統和產品管理員就能妥善管理執行個體的存取權限。
* Admin Console 中的產品設定檔能決定使用者可存取的執行個體。
* 客戶可使用符合SAML 2的身分識別服務提供者（簡稱IDP）進行單一登入。
* 僅支援客戶單一登入的Enterprise ID或Federated ID，不支援個人AdobeID。

## 架構 {#architecture}

IMS 驗證採用 OAuth 通訊協定，能在 AEM 和 Adobe IMS 端點之間運作。使用者加入 IMS 並擁有 Adobe 身分後，就能使用 IMS 憑證登入 AEM 作者服務。

使用者登入流程如下所示，系統會將使用者重新導向至IMS，並可選擇重新導向至客戶IDP以進行SSO，然後重新導向回AEM。

![IMS 架構](/help/security/assets/ims1.png)

## 設定方法 {#how-to-set-up}

### 在 Adobe Admin Console 中佈建組織 {#onboarding-orgs-to-adobe-admin-console}

若要使用 Adobe IMS 進行 AEM 驗證，客戶必須先開始使用 Adobe Admin Console。

首先，客戶需有佈建於 Adobe IMS 的組織。Adobe 企業客戶在 [Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html) 中會顯示為 IMS 組織。Adobe 客戶可使用此入口網站管理使用者和群組的產品權益。

AEM客戶應先布建組織，而在IMS布建過程中，客戶執行個體可在Admin Console中管理使用者權益和存取許可權。

客戶成為 IMS 組織後，即可依以下摘要內容設定其系統：

![IMS 上線](/help/security/assets/ims2.png)

1. 指定的系統管理員會收到 Cloud Manager 的登入邀請函。登入 Cloud Manager 後，系統管理員可以選擇佈建 AEM 程序和環境，或導覽至 Admin Console 執行管理任務。
1. 系統管理員需先宣告網域，以確認各別網域的所有權 (例如 acme.com)
1. 系統管理員設定使用者目錄
1. 系統管理員在Admin Console中執行IDP設定以設定單一登入。
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

使用者同步工具 (簡稱 UST) 可方便我們的企業客戶使用 Active Directory 建立及管理 Adobe 使用者。此工具也適用於其他通過測試的 OpenLDAP 目錄服務。目標使用者是IT身分管理員（企業目錄或系統管理員），他們能夠安裝和設定此工具。 此開放原始碼工具可供自訂，客戶可依自身的特定需求加以修改。

「使用者同步」執行時，會從組織的Active Directory擷取使用者清單，並與Admin Console內的使用者清單進行比較。  然後它會呼叫Adobe使用者管理API，以便Admin Console與組織的目錄同步。 此變更流程無法復原。在 Admin Console 中完成的任何編輯都不會推送至目錄。

此工具可讓系統管理員將客戶目錄中的使用者群組與Admin Console中的產品設定和使用者群組對應。

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
>布建AEM環境和執行個體時，系統會自動設定所需的AEM IMS設定。 不過，管理員可透過[此處](/help/implementing/deploying/overview.md)所述方法，依需求適度修改。

布建AEM環境和執行個體時，系統會自動設定所需的AEM IMS設定。  客戶管理員可依需求適度修改部分設定

整體方式是將 Adobe IMS 設為 OAuth 提供者，並像處理 LDAP 同步作業一樣，修改 **Apache Jackrabbit Oak Default Sync Handler**。

以下是需要修改以變更「使用者自動成員資格」或「群組對應」等屬性的重要OSGI設定。

<!-- Arun to provide list of osgi configs -->

## 使用方式 {#how-to-use}

### 在 Admin Console 中管理產品和使用者存取權限 {#managing-products-and-user-access-in-admin-console}

產品管理員登入 Admin Console 後，會看到 AEM as a Cloud Service 產品內容的多個執行個體，如下所示：例如，從「**概觀**」頁面選取任何產品：

![執行個體登入](/help/security/assets/ims6.png)

您將看到現有的執行個體清單：

![執行個體登入 2](/help/security/assets/ims7.png)

在每個產品內容例項下，都有例項橫跨生產、階段或開發環境的作者或發佈服務。 每個執行個體都與產品設定檔或Cloud Manager角色相關聯。 這些產品設定檔的主要功用在於指派存取權限給具有必要權限的使用者和群組。

此 **AEM管理員_xxx** 設定檔是用來授與相關聯AEM執行個體的管理員許可權，而 **AEM使用者_xxx** 設定檔用於新增一般使用者。

在此產品設定檔中新增的任何使用者和群組都可以登入該特定執行個體，如以下範例所示：

![產品設定檔](/help/security/assets/ims8.png)

>[!WARNING]
>
>**AEM 管理員**&#x200B;產品設定檔名稱不得變更。如果變更 **AEM 管理員**&#x200B;產品設定檔名稱，會將所有指派到該設定檔之使用者的管理員權限移除。

### 登入 Adobe Experience Manager as a Cloud Service {#logging-in-to-aem}

**本機管理員登入**

AEM 可繼續為管理員使用者支援本機登入。從登入畫面可選擇本機登入：

![本機登入](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**IMS 登入**

若是其他使用者，在執行個體上設定 IMS 後，即可使用 IMS 登入。使用者需先按一下「使用 Adobe 登入」按鈕，如下所示：

![IMS 登入](/help/security/assets/ims10.png)


>[!NOTE]
>
>在 IMS 中建立的任何使用者都可使用 Adobe ID 或 Federated ID 來建立。若是使用 Federated ID 設定使用者，使用者需透過公司合作之身分服務供應商登入，以完成驗證。

接著，系統會將使用者重新導向至 IMS 登入畫面，此時使用者需輸入憑證：

![IMS 登入 2](/help/security/assets/ims11.png)

![IMS 登入 3](/help/security/assets/ims12.png)

如果在初始Admin Console設定期間設定了同盟IDP，則會將使用者重新導向至客戶IDP以進行SSO：

![IMS 登入 4](/help/security/assets/ims13.png)

驗證完成後，系統會將使用者重新導向回AEM並登入：

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
>Cloud Manager 已預先設定角色，賦予適當權限。若要了解各個具有特定權限的角色、預先設定的任務或每個角色的相關權限，請參閱[角色型權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/what-is-required/role-based-permissions.html)。

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

若要在中存取AEM執行個體 **Admin Console**，您應該會在的產品清單中看見Cloud Manager計畫和計畫內的環境 **Admin Console**.

舉例來說，在下方螢幕擷圖中，您會看到兩個可供使用的環境，即 *dev author* 和 *publish*。

![ACL3](/help/security/assets/ims19.png)

若要存取 AEM 執行個體，使用者必須新增至適當雲端服務產品群組。

每個作者執行個體都會有 AEM 管理員和 AEM 使用者設定檔，而每個發佈執行個體都有 AEM 使用者設定檔。您可以視需求新增其他設定檔。

若要取得管理員層級的 AEM 執行個體存取權限，使用者需新增至特定產品的 AEM 管理員設定檔。
