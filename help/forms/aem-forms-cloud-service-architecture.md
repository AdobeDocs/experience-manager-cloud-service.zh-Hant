---
title: Experience Manager [!DNL AEM Forms] as a Cloud Service體系結構
description: 瞭解 [!DNL AEM Forms] as a Cloud Service瞭解平台的可擴充性、恢復性和效能方面。
source-git-commit: cb7b417b9b4898b0656e79d6f699e8d5cd611e76
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 2%

---


# [!DNL AEM] Formsas a Cloud Service建築 {#architecture}

[!DNL Adobe Experience Manager Forms] as a Cloud Service是一種雲本地解決方案，供企業建立、管理、發佈和更新複雜的數字表單和通信，同時將提交的資料與後端流程、業務規則整合在一起，並將資料保存到外部資料儲存中。 它延伸了 [!DNL Adobe Experience Manager as a Cloud Service]。 要瞭解有關擴展、部署、環境和其他基礎架構的更多資訊，請參見 [淺談建築 [!DNL Adobe Experience Manager as a Cloud Service]](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/core-concepts/architecture.html)。

AEM Formsas a Cloud Service支援兩大用例：數字註冊和客戶通信。 以下圖說明了兩種使用情形的體系結構。

## 體系結構和流圖

**Forms數字註冊**

![Forms — 數字入學](assets/forms-cloud-service-architecture-forms-digital-enrollment.svg)

**Forms通訊**

![Forms通訊](assets/forms-cloud-service-architecture-forms-communications.svg)

## 元件

Formsas a Cloud Service包括多個元件：

### CDN（內容分發網路）

每個AEM Formsas a Cloud Service項目 [內置CDN服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn.html)。 它被列入Forms作為Cloud Services的執照中。

### 作者

「作者」是在標準「作者」運行模式下運行的AEM Formsas a Cloud Service實例。 它適用於內部用戶、表單設計者和開發人員。 Author環境可啟用以下功能：

* 創作和管理表單。
* 連接到Automated forms conversion服務以將PDF或XDP表單轉換為自適應表單。
* 建立並運行以Forms為中心的工作流。
* 管理自適應表單資產。
* 管理通信資產。
* 同步REST風格的API（即時API）和批處理API，用於建立、裝配和提供面向品牌的個性化通信。
* 同步API，用於組合、重新排列和驗證PDF文檔。

### 發佈

發佈實例是在標準發佈運行模式下運行的AEM Formsas a Cloud Service。 發佈實例旨在為基於表單的應用程式的最終用戶提供，例如訪問公共網站和提交表單的用戶。 它啟用以下功能：

* 為最終用戶呈現和提交表單。
* 傳輸原始提交的表單資料，以便在最終記錄系統中進一步處理和儲存。
* 連接到客戶托管儲存以儲存資料。
* 與Adobe Sign連接，以電子簽名自適應表單提交記錄。
* 同步API以建立、裝配和提供面向品牌和個性化的通信。
* 同步API以組合、重新排列和驗證PDF文檔。

在as a Cloud Service上，「反向復AEM制」不可用，無法將內容/資料從發佈服務發送到作者服務。 但是，您可以配置在發佈上運行的自適應Forms，以將資料提交到作者上的工作流（工作流只能在作者上運行）。 這對批准使用案例很有幫助。

#### Dispatcher

[調度程式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/content-delivery/disp-overview.html) 是Adobe Experience Manager的快取和/或負載平衡工具，可與企業級Web伺服器一起使用。

### Adobe服務

**automated forms conversion服務**

[automated forms conversion服務](https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/introduction.html) 自動將PDF和XFA表單轉換為設備友好、響應快速且基於HTML5的自適應表單。

**Adobe Sign**

Adobe Sign是一種基於雲的電子簽名服務，允許用戶使用瀏覽器或移動設備發送、簽名、跟蹤和管理簽名過程。 您可以將Adobe Sign與自適應表單整合，以自動化簽名工作流、簡化單個和多個簽名過程，以及以電子方式簽署自適應表單。

<!-- **PDF Service API**
Adobe’s PDF Services API lets create, combine, export, and extract data from PDFs through powerful and flexible cloud-based APIs. -->

### 客戶托管儲存

Formsas a Cloud Service提供了將內容儲存在外部儲存系統（如Blob儲存區、資料庫或儲存服務）中的選項。 您還可以將包含敏感個人資料(SPD)元素的在製品工作流資料(AEM工作流變數資料)儲存在客戶管理的儲存庫中，以便進行安全處理。 Adobe建議僅將敏感資料儲存在客戶管理的儲存上。

您可以使用 **統一儲存連接器** 連接到Blob儲存和 **窗體資料模型** 連接到資料庫或後端服務（RESTful、SOAP、Azure Blob儲存等）。

### 文件服務

檔案服務包括：

* **輸出服務（通信 — 文檔生成API）** 幫助建立品牌批准、個性化和標準化的文檔，如業務往來、報表、理賠信函、福利通知、每月帳單或歡迎套件。

* **匯編程式服務（通信 — 文檔操作API）** 幫助合併、重新排列和驗證PDF文檔。

* **記錄文檔(DoR)服務** 幫助生成記錄文檔(DoR)。 該服務以其自己的Pod運行，Pouss形式分別為「作者」和「發佈Formsas a Cloud Service」實例。 它有助於提供更好的效能，並根據負載獨立地擴展莢。

### Cloud Manager

雲管理器是 [AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html)。 它是我們客戶的運營和開發人員形象的單一入口點。 它是管理程式和AEM環境的場所。 Cloud Manager已演變為自助服務門戶，在該門戶中可以建立AEM和配置as a Cloud Service的主要元件：

* 建立和管理程式
* 建立和管理AEM程式內的環境
* 建立和管理管道，以將客戶代碼和配置部署到特定環境
* 獲取有關這些元件的重要生命週期事件（例如，產品更新）的通知有關Cloud Manager的詳細資訊，請參閱 [瞭解Adobe雲管理器](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) 和 [雲管理器簡介](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html)。

### 開發人員控制台

開發人員控制台提供作為雲服務環境運行的每個Forms的各種詳細資訊。 這些詳細資訊有助於調試環境。 有關詳細資訊，請參閱 [使用開AEM發人員控制台調試as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)。

<!--

+++CDN (Content Delivery Network):

Every AEM Forms as a Cloud Service program has access to Fastly CDN service. It is included in the licence of Forms as a Cloud Services.

+++

+++Adaptive Forms
Adaptive Forms enable customers to author web-friendly reflowable web forms and fragments that are used by the customers for their data capture needs. This feature enables customers to manage their complex data capture needs easily, by leveraging multiple integrations with Adobe Sign, Document Services, Form Data Model, Automated Forms Conversion service, and more.

+++

+++Automated Forms Conversion Service (AFCS)
Automated Forms Conversion service helps accelerate digitization and modernization of data capture experience through automated conversion of PDF forms to adaptive forms. The service, powered by Adobe Sensei, automatically converts your PDF forms to device-friendly, responsive, and HTML5-based adaptive forms. While leveraging the existing investments in PDF Forms and XFA, the service also applies appropriate validations, styling, and layout to adaptive form fields during conversion.

+++

+++Form Data Model
The Form Data Model (FDM) feature is the standard way of creating data integrations with external/internal data sources and using them across the different Forms as a Cloud Service features. FDM provides a rich editor for customers to integrate, define, and manage relationships between the different entities and data sources and perform operations on them. Form data is stored in a data store hosted on the customer premises. Organizations can also use blob store hosted by the cloud provider and Adobe Experince Platform to store data.

+++

+++Forms Workflows
Forms-centric workflows is an extension to the default AEM Workflow and provides our customers with additional workflow capabilities like Form Data review, task assignment, and document services invocation.

+++

+++Communications
Forms as a Cloud Service offering consists of multiple services tailored specifically for document processing.

+++

+++Document of Record
A Document of Record is a PDF version of a form. It provides an ability to keep a record of the information  that you provide and submit in an Adaptive Form in PDF fromat. The service provides a default DoR template and tools to develop a custom template.

+++

## Terminologies

<!-- ## Cloud Manager{#cloud-manager}

Cloud Manager is an essential component to [AEM as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/introduction.html?lang=en). Each new tenant of the [!DNL AEM Forms] as a Cloud Service is first provisioned for Cloud Manager access. Cloud Manager is the single-entry point for the operations and developer persona of our customers. It is the place from where the AEM programs and environments can be managed. Cloud Manager has evolved as a self-service portal where the main components of the AEM as a Cloud Service can be created and configured:

* Creating and managing programs
* Creating and managing the AEM environments within the programs
* Creating and managing the pipelines for deploying the customer code and configuration to a particular environment
* Getting notified of important lifecycle events for these components (e.g. product updates)
For more information about Cloud Manager, see [Understand Adobe Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/cloud-manager/understand-cloud-manager-for-aem.html) and [Introduction to Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/introduction-to-cloud-manager.html).

## Users and Authentication {#users-and-authentication}

AEM as a Cloud Service includes Admin Console support for AEM instances and Adobe Identity Management System (IMS) based authentication. The Admin Console allows administrators to centrally manage all Experience Cloud users. Users and Groups can be assigned to product profiles associated with AEM as a Cloud Service instances, allowing them to log in to that instance. For more information about users, authentication, and, and accessing an instance of AEM as a Cloud Service, see [IMS Support for [!DNL Adobe Experience Manager] as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html?lang=en#introduction).

Various personas are involved in a typical [!DNL AEM Forms] project. After you log in to your [!DNL AEM Forms] as a Cloud Service instance, you can [add users in admin console](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/security/ims-support.html) for personas applicable to your organization or project and [assign users to built-in groups](forms-groups-privileges-tasks.md) to provide them required privileges.

To learn various in-built [!DNL AEM Forms] specific user groups and privileges available on [!DNL AEM Forms] as a Cloud Services instance, see [Configure, user, roles and groups](forms-groups-privileges-tasks.md). 

## Developer Experience {#developer-experience}

The new architecture supporting AEM as a Cloud Service brings some key changes to the overall developer experience. One of the major goals for the changes to developer experience is to allow migration to AEM as a Cloud Service as quickly as possible, with little modifications to existing custom code.

## Cloud development {#cloud-development}

Here are the guidelines to run your existing code smoothly on AEM as a Cloud Service environment:

* Store your code and configurations to the Git repository of the associated Cloud Manager program. It makes managing and integrating code with CI/CD a breeze.  
* Make application code and configuration compatible with the baseline [!DNL AEM Forms] images. Using the latest APIs helps to build faster and secure applications.
* Use the Cloud Manager pipeline associated with the Cloud Manager environment to build and deploy applications. It helps you bring the latest features and bug fixed for [!DNL AEM Forms] as a Cloud Service to your environment.
* Try that your custom applications pass all the code quality, security, and performance gates enforced in the pipeline. It helps build secure and better performing applications which leads to better customer experience. You can always use Cloud Manager UI to skip some checks.
This process is commonly referred to as cloud-first development. [!DNL AEM Forms] as a Cloud Service also provides an SDK to support rapid development before the pending code and configuration changes are attempted in the cloud.
Some interfaces that were previously part of the AEM QuickStart are no longer available to the users of the AEM as a Cloud Service environment. For instance, the Web Console where OSGI bundles and their associated configuration are managed. The CRXDE Lite content repository browser becomes only accessible on non-production environment types. A subset of the Web Console functionalities that developers require, especially when it comes to diagnostics and status purposes, is made available via a new developer console.
Also, one of the most common requirements for developers is quick access to the log files of the various environments. With [!DNL AEM Cloud Service], the log files of the different nodes in the Author, Publish are made available via the Cloud Manager, either in the form of files that can be downloaded or via APIs for tailing the logs. Due to the clear separation of code and content, developers can leverage a particular process for updating content as part of a deployment. The typical use cases for mutable content are:
* Standard “default” content that is part of the customer project (e.g. folders, templates, workflows...)
* Search index definitions
* ACLs and permissions
* Service users and user groups
Set up your development environment, [Configure your CI/CD Pipeline](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/configuring-pipeline.html), and learn to [deploy your code](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/deploying-code.html) on the environment. -->

### 自適應表單創作 {#local-development}

設定和配置 [!DNL AEM Forms] as a Cloud Service環境，您可以設定開發、試運行和生產環境。 此外，還設定和配置本地開發環境，以便快速重複和開發。 您可以下載並設定AEMSDK和 [!DNL AEM Forms] 附加功能存檔以設定本地 [!DNL Forms] as a Cloud Service發展環境。  有關詳細說明，請參見 [設定本地開發環境](setup-local-development-environment.md)。

## 偵錯 {#debugging}

AEMas a Cloud Service運行在自助服務、可擴展的雲基礎架構上。 它要求開AEM發人員瞭解和調試as a Cloud Service的各個方面，AEM從構建和部署到獲取運行應用程式的詳細AEM資訊。 有關詳細資訊，請參見 [調試AEMas a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/overview.html)。
