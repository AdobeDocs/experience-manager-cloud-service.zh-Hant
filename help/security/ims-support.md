---
title: IMS支援Adobe Experience Manager雲端服務
description: 'IMS支援Adobe Experience Manager雲端服務 '
translation-type: tm+mt
source-git-commit: bef17376f0b7de79511f9ad6ceb00e9f084f45d2

---


# IMS支援Adobe Experience Manager雲端服務 {#ims-support-for-aem-as-a-cloud-service}

## 簡介 {#introduction}

* AEM做為雲端服務，包含Admin console對AEM例項和Adobe Identity Management System（簡稱IMS）型驗證的支援。
* Admin Console可讓管理員集中管理所有Experience cloud使用者。
* 使用者和群組可以指派給與AEM相關聯的產品設定檔，做為Cloud Service例項，讓他們登入該例項。

## 主要亮點 {#key-highlights}

AEM做為雲端服務，僅針對作者、管理員和開發人員使用者提供IMS驗證支援。 它不支援客戶網站（如網站訪客）的外部使用者。

* Admin Console會將客戶表示為IMS組織、製作和發佈例項，在環境中則表示為產品內容例項。 這可讓系統和產品管理員管理例項的存取權。
* 管理控制台中的產品設定檔將決定使用者可以存取的例項。
* 客戶將可使用其自己的SAML 2相容身分提供者（簡稱IDP）進行單一登入。
* 僅支援客戶單一登入的Enterprise ID或Federated ID，不支援個人Adobe ID。

## 建築 {#architecture}

IMS驗證可在AEM和Adobe IMS端點之間使用OAuth通訊協定運作。 當使用者新增至IMS並擁有Adobe Identity後，他們就可以使用IMS憑證登入AEM作者服務。

使用者登入流程如下所示，使用者將被重新導向至IMS，並可選擇性地重新導向至SSO的客戶IDP，然後重新導向回AEM。

![IMS架構](/help/security/assets/ims1.png)

## 如何設定 {#how-to-set-up}

### 將組織上線至Adobe Admin Console {#onboarding-orgs-to-adobe-admin-console}

客戶上線至Adobe Admin Console是使用Adobe IMS進行AEM驗證的先決條件。

首先，客戶需要在Adobe IMS中布建組織。 Adobe企業客戶在 [](https://helpx.adobe.com/enterprise/using/admin-console.html) Adobe Admin Console中代表為IMS組織。此入口網站是Adobe客戶用來管理其使用者和群組產品權益的入口網站。

AEM客戶應已布建組織，而作為IMS布建的一部分，客戶例項將可在Admin Console中提供，以管理使用者權益和存取權。

一旦客戶作為IMS組織存在，他們必須依以下摘要來設定其系統：

![IMS入門](/help/security/assets/ims2.png)

1. 指定的系統管理員會收到登入Cloud Manager的邀請。 登入Cloud Manager後，系統管理員可以選擇布建AEM程式和環境，或導覽至Admin Console進行管理工作。
1. 系統管理員聲明域用於確認各自域的所有權（例如acme.com）
1. 系統管理員設定用戶目錄
1. 系統管理員在Admin Console中執行IDP設定，以設定單一登入。
1. AEM管理員會照常管理本機群組和權限。

此處涵蓋Adobe Identity Management基本概念，包括IDP [設定](https://helpx.adobe.com/enterprise/using/set-up-identity.html)。

此處涵蓋「企業管理」和「管理控制台」 [的使用](https://helpx.adobe.com/enterprise/managing/user-guide.html)。

### Admin Console中的入職使用者 {#onboarding-users-in-admin-console}

根據客戶的規模及其偏好設定，有三種方式可讓使用者上線：在管理控制台中手動建立使用者、上傳。csv檔案或從客戶的企業Active Directory同步使用者。

**透過Admin Console UI手動新增**

使用者和群組可在「管理控制台」UI中手動建立。 如果您沒有大量使用者可管理，則可使用此方法。 例如，少於50名AEM使用者，或者您已使用此方法管理其他Adobe產品，例如Analytics、Target或Creative cloud應用程式。

![使用者入門](/help/security/assets/ims3.png)

**Admin Console UI中的檔案上傳**

為方便使用者建立，可上 `.csv` 傳檔案以大量新增使用者。

![檔案上傳](/help/security/assets/ims4.png)

**使用者同步工具**

使用者同步工具（簡稱UST）可讓我們的企業客戶使用Active Directory來建立和管理Adobe使用者。 這也適用於其他經測試的OpenLDAP目錄服務。 目標用戶是IT Identity Administrators（Enterprise Directory或系統管理員），他們將能夠安裝和配置此工具。 開放原始碼工具可自訂，讓客戶可依您的特定需求加以修改。

當「使用者同步」執行時，會從組織的Active Directory擷取使用者清單，並與「管理控制台」中的使用者清單進行比較。  接著會呼叫Adobe使用者管理API，讓Admin Console與組織的目錄同步。 改變流程完全是一種方式。 在「管理控制台」中所做的任何編輯都不會推送至目錄。

此工具可讓系統管理員將客戶目錄中的使用者群組與管理控制台中的產品設定和使用者群組對應。

若要設定「使用者同步」，組織必須以使用「使用者管理API」的相同方式建立一 [組認證](https://www.adobe.io/apis/experienceplatform/umapi-new.html)。

![使用者同步工具](/help/security/assets/ims5.png)

使用者同步工具是透過Adobe Github存放庫在此 [位置散發](https://github.com/adobe-apiplatform/user-sync.py/releases/latest)。

>[!NOTE]
>
> 動態群組 **建立支援提供搶鮮版2.4RC1** ，您可在此 [找到](https://github.com/adobe-apiplatform/user-sync.py/releases/tag/v2.4rc1)。

此版本的主要功能是在管理控制台中動態對應新的LDAP群組以取得使用者成員資格，以及建立動態使用者群組。

有關新群組功能的更多資訊，請 [在此處找到](https://github.com/adobe-apiplatform/user-sync.py/blob/v2/docs/en/user-manual/advanced_configuration.md#additional-group-options)。

**使用者同步檔案**

請參閱 [UST檔案](https://adobe-apiplatform.github.io/user-sync.py/en/) ，以取得詳細資訊。

使用者同步工具必須使用此處的程式註冊為Adobe I/O用戶端UMAPI [](https://adobe-apiplatform.github.io/umapi-documentation/en/UM_Authentication.html)。

Adobe I/O Console檔案可在這裡找 [到](https://www.adobe.io/apis/cloudplatform/console.html)。

此處涵蓋使用者同步工具所使用的使用者管理API [](https://www.adobe.io/apis/cloudplatform/umapi-new.html)。

## Adobe Experience雲端服務設定 {#aem-configuration}

> [!NOTE]
>
>當布建AEM環境和例項時，將自動設定所需的AEM IMS設定。 但是，管理員可依其需求使用此處所述的方法修改 [它](/help/implementing/deploying/overview.md)。

在布建AEM環境和例項時，需要的AEM IMS設定會自動設定。  客戶管理員可以根據自己的要求修改部分配置

整體方式是將Adobe IMS設為OAuth提供者。 Apache **Jackrabbit Oak Default sync處理常式** ，可像LDAP同步一樣修改。

以下是需要修改的關鍵OSGI配置，以便更改「用戶自動成員資格」或「組映射」等屬性。

<!-- Arun to provide list of osgi configs -->

## 如何使用 {#how-to-use}

### 在Admin Console中管理產品和使用者存取權 {#managing-products-and-user-access-in-admin-console}

當產品管理員登入Admin Console時，他們將會看到AEM Managed services產品內容的多個例項，如下所示：

![例項登入](/help/security/assets/ims6.png)

在此範例中，組織 **AEM-MS-Onboard** 有32個執行個體，橫跨不同的拓撲和環境，例如Stage或Prod。

![例項登入2](/help/security/assets/ims7.png)

在每個「產品內容」例項下，都會有相關聯的產品設定檔。 這些產品設定檔可用來指派具有必要權限的使用者和群組存取權。

Administrator_xxx **profile將用於授予關聯AEM實例中的管理員權限，而** User_xxx **** profile用於添加常規用戶。

在此產品設定檔下新增的任何使用者和群組都可以登入該特定例項，如下例所示：

![產品設定檔](/help/security/assets/ims8.png)

### 以雲端服務的身分登入Adobe Experience Manager(#logging-in-to-aem)

**本地管理員登錄**

AEM可繼續支援管理員使用者的本機登入。 登入畫面可選擇本機登入：

![本機登入](/help/security/assets/ims9.png)

<!-- the above image needs to be updated for skyline -->

**基於IMS的登錄**

對於其他使用者，在例項上設定IMS後，就可使用以IMS為基礎的登入。 使用者會先按一下「使用Adobe登入」按鈕，如下所示：

![IMS登入](/help/security/assets/ims10.png)

然後，會將他們重新導向至IMS登入畫面，並需要輸入其認證：

![IMS登入2](/help/security/assets/ims11.png)

![IMS登入3](/help/security/assets/ims12.png)

如果在初始Admin Console設定期間設定了同盟IDP，則會將使用者重新導向至客戶IDP以進行SSO:

![IMS登入4](/help/security/assets/ims13.png)

驗證完成後，使用者會重新導向回AEM並登入：

![IMS登入5](/help/security/assets/ims14.png)

### 以雲端服務的形式管理Adobe Experience manager中的權限和ACL {#managing-permissions-in-aem}

AEM中將繼續管理ACL和權限。 從IMS同步的使用者群組可指派給定義ACL和權限的本機群組。

在下列範例中，我們新增同步群組至本機 **Dam_Users** 群組做為範例。

使用者是IMS中下列群組的一部分：

![ACL1](/help/security/assets/ims15.png)

當使用者登入時，會同步其群組成員資格，如下所示：

![ACL2](/help/security/assets/ims16.png)

在AEM中，與IMS同步的使用者群組可以新增為現有本機群組(例如 **DAM使用者)的成員**。

![ACL3](/help/security/assets/ims17.png)

如下所示，群組 **AEM-GRP_008** 繼承 **** DAM使用者的權限和權限，這是管理同步群組權限的有效方式，也常用於LDAP型驗證方法。

![ACL3](/help/security/assets/ims18.png)