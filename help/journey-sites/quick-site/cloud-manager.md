---
title: 瞭解Cloud Manager和快速網站建立工作流程
description: 瞭解Cloud Manager以及它如何將新的快速網站建立流程聯絡起來。
exl-id: 5d264078-e552-48ca-8d82-294a646e6b1f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 17%

---

# 瞭解Cloud Manager和快速網站建立工作流程 {#understand-cloud-manager}

瞭解Cloud Manager以及它如何將新的快速網站建立流程聯絡起來。

>[!TIP]
>
>如果您的角色僅是前端開發，您可以跳至文章 [擷取Git存放庫存取資訊](retrieve-access.md) 在此歷程中。
>
>如果您是AEM管理員、Cloud Manager管理員、負責前端開發和管理員任務，或只是想瞭解AEM中用於前端開發的端對端流程，請繼續閱讀當前檔案並繼續此歷程。

## 目標 {#objective}

本檔案可協助您瞭解AEM快速網站建立工具的運作方式，並提供您端對端流程的概觀。 閱讀本文件後，您應該：

* 瞭解AEM Sites和Cloud Manager如何共同運作以促進前端開發
* 瞭解前端自訂步驟如何與AEM完全分離且不需要AEM知識。

本檔案著重於在繼續此歷程的下一步來開始設定之前，瞭解快速網站建立解決方案的這些基本片段。

雖然我們建議您逐步完成此歷程，但如果您已瞭解AEM Sites和Cloud Manager的合作方式，並且希望直接從設定開始，您可以 [跳至歷程的下一步。](create-site.md)

## 負責角色 {#responsible-role}

此歷程的這一部分適用於AEM管理員和Cloud Manager管理員。

## 要求和先決條件 {#requirements-prerequisites}

使用「快速網站建立」工具開始建立和自訂網站之前，有幾項需求。

由於此歷程適用於前端開發人員、管理員和所有角色的組合，因此此處列出兩者的要求。

請務必瞭解，對於前端開發人員而言，無需具備AEM存取權或知識。

### 知識 {#knowledge}

| 知識 | 角色 |
|---|---|
| 瞭解前端開發的標準工具和流程 | 前端開發人員 |
| 有關如何在AEM中建立和管理網站的基本知識 | AEM 管理員 |
| Cloud Manager的基本知識 | Cloud Manager 管理員 |

對於前端開發人員而言，無需具備AEM知識。

### 工具 {#tools}

| 工具 | 角色 |
|---|---|
| 偏好的前端開發環境 | 前端開發人員 |
| npm | 前端開發人員 |
| webpack | 前端開發人員 |
| 存取Cloud Manager | Cloud Manager 管理員 |
| 成為以下專案的成員： **業務負責人** Cloud Manager中的角色 | Cloud Manager 管理員 |
| 成為Cloud Manager中的系統管理員 | Cloud Manager 管理員 |
| 存取Admin Console | Cloud Manager 管理員 |
| 成為 **部署管理員** Cloud Manager中的角色 | Cloud Manager 管理員 |
| 成為 **部署管理員** Cloud Manager中的角色 | 前端開發人員 |

對於前端開發人員而言，無需使用AEM。

>[!TIP]
>
>如果您不熟悉Cloud Manager角色和角色管理，請參閱 [其他資源](#additional-resources) 區段。

## Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，可作為平台的單一入口點。

為了支援具有企業開發設定的客戶，AEMas a Cloud Service與Cloud Manager及其專門建置的CI/CD管道完全整合。 「快速網站建立」工具延伸了這些功能，以支援專用的前端開發管道。

在此歷程中，不需要完全瞭解Cloud Manager。 從高層面來看，Cloud Manager由數個結構層級組成。

![Cloud Manager 結構](assets/cloud-manager-structure.png)

* **租使用者** - 每個客戶都佈建了一個租使用者。
* **計畫** - 每個租使用者都有一個或多個計畫，這些計畫通常反映了客戶的授權解決方案。
* **環境** - 每個計畫都有多種環境，例如用於即時內容的生產、一種用於測試、一種用於開發目的。
* **存放庫**  — 這些環境有Git存放庫，可維護應用計畫和前端計畫碼。
* **工具和工作流程** - 管道管理從存放庫到環境的計劃碼部署。

範例通常有助於內容化此階層。

* WKND Travel and Adventure Enterprises 可能是專注於旅遊相關媒體的&#x200B;**租使用者**。
* WKND Travel and Adventure Enterprises 租使用者可能有兩個&#x200B;**計畫**：一個用於 WKND Magazine 的 Sites 計畫，和一個用於 WKND Media 的 Assets 計畫。
* WKND Magazine 和 WKND Media 計畫都將有開發、測試和製作&#x200B;**環境**。

## 快速網站建立前端開發流程 {#flow}

整體流程既簡單又直覺，即使您尚未擁有豐富的Cloud Manager經驗。

1. AEM管理員登入AEM環境，並使用網站範本建立新網站。
1. Cloud Manager管理員會在Cloud Manager中建立前端管道。 管道可協調將計畫碼從Git存放庫部署到AEM環境。
1. AEM管理員會從計畫的AEM執行個體匯出網站主題，並將其提供給前端開發人員。
1. Cloud Manager管理員會授予前端開發人員可提交自訂的AEM Git存放庫的存取權。
1. 前端開發人員會擷取存取認證以存取Git和管道。
1. 前端開發人員自訂主題，並使用Proxy使用網站中的實際內容進行測試，然後將變更提交到Git存放庫。
1. 前端開發人員執行管道以將主題自訂部署到計畫的生產環境。

![快速網站建立流程](assets/qsc-flow.png)

使用「快速網站建立」工具的主要優點在於，純前端開發人員只負責實際自訂。 前端開發人員不會與AEM互動，或需要任何AEM知識。

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應：

* 瞭解AEM Sites和Cloud Manager如何共同運作以促進前端開發
* 瞭解前端自訂步驟如何與AEM完全分離且不需要AEM知識。

在此知識的基礎上繼續您的AEM快速網站建立歷程，接下來檢視檔案 [從範本建立網站，](create-site.md) 您將瞭解如何使用範本快速建立新的AEM網站。

## 其他資源 {#additional-resources}

我們建議您檢閱檔案，繼續快速網站建立歷程的下一部分 [從範本建立網站，](create-site.md) 以下是一些其他可選資源，這些資源對本文檔中提到的一些概念進行了更深入的探究，但並非繼續此歷程所必需的。

* [Cloud Manager 文件](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - 如果您想要 Cloud Manager 功能的更多詳細資訊，您可能想要直接查閱深入的技術文件。
* [角色型許可權](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager已預先設定角色，賦予適當許可權。 請參閱本檔案以瞭解這些角色的詳細資訊及管理方法。
* [npm](https://www.npmjs.com)  — 用來快速建立網站的AEM主題是以npm為基礎。
* [webpack](https://webpack.js.org)  — 用於快速建立網站的AEM主題依賴webpack。
