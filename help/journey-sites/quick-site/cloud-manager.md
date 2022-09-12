---
title: 了解Cloud Manager和快速網站建立工作流程
description: 了解Cloud Manager及其如何將新的快速網站建立程式連結在一起。
exl-id: 5d264078-e552-48ca-8d82-294a646e6b1f
source-git-commit: 940a01cd3b9e4804bfab1a5970699271f624f087
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 1%

---

# 了解Cloud Manager和快速網站建立工作流程 {#understand-cloud-manager}

了解Cloud Manager及其如何將新的快速網站建立程式連結在一起。

>[!TIP]
>
>如果您的角色只是前端開發，您可以跳至文章 [擷取Git存放庫存取資訊](retrieve-access.md) 在這個歷程中。
>
>如果您是AEM管理員、Cloud Manager管理員，負責前端開發和管理員工作，或只是想了解AEM中用於前端開發的端對端流程，請繼續閱讀目前的檔案並繼續進行此歷程。

## 目標 {#objective}

本檔案可協助您了解AEM快速網站建立工具的運作方式，並提供端對端流程的概觀。 閱讀後，您應：

* 了解AEM Sites與Cloud Manager如何共同合作以促進前端開發
* 了解前端自訂步驟如何與AEM完全分離，且不需要AEM知識。

本檔案著重於了解快速網站建立解決方案的這些基本要素，再繼續進行您開始設定的歷程的下一個步驟。

雖然建議您逐步完成此歷程，但若您已了解AEM Sites和Cloud Manager可共同運作，且想直接從設定開始，您可以 [跳至歷程的下一個步驟。](create-site.md)

## 負責角色 {#responsible-role}

此部分的歷程會同時套用至AEM管理員和Cloud Manager管理員。

## 需求與必要條件 {#requirements-prerequisites}

開始使用「快速網站建立」工具建立和自訂網站之前，有幾項需求。

由於此歷程的目標是前端開發人員、管理員以及所有角色的組合，因此這裡會列出這兩者的需求。

請務必了解，對於前端開發人員而言，不需要AEM存取權或知識。

### 知識 {#knowledge}

| 知識 | 角色 |
|---|---|
| 了解前端開發的標準工具和流程 | 前端開發人員 |
| 在AEM中建立及管理網站的基本知識 | AEM 管理員 |
| Cloud Manager基本知識 | Cloud Manager管理員 |

對於前端開發人員，不需要AEM知識。

### 工具 {#tools}

| 工具 | 角色 |
|---|---|
| 首選前端開發環境 | 前端開發人員 |
| npm | 前端開發人員 |
| webpack | 前端開發人員 |
| 存取Cloud Manager | Cloud Manager管理員 |
| 成為 **業務負責人** 在Cloud Manager中的角色 | Cloud Manager管理員 |
| 在Cloud Manager中擔任系統管理員 | Cloud Manager管理員 |
| 存取Admin Console | Cloud Manager管理員 |
| 成為 **部署管理員** 在Cloud Manager中的角色 | Cloud Manager管理員 |
| 成為 **部署管理員** 在Cloud Manager中的角色 | 前端開發人員 |

對於前端開發人員，不需要使用AEM。

>[!TIP]
>
>如果您不熟悉Cloud Manager的角色和角色管理，請參閱 [其他資源](#additional-resources) 區段。

## Cloud Manager {#cloud-manager}

Cloud Manager是AEMas a Cloud Service的必要元件，是平台的單一進入點。

為了透過企業開發設定支援客戶，AEM as a Cloud Service與Cloud Manager及其專門建立的CI/CD管道完全整合。 快速站點建立工具擴展了這些功能，以支援專用的前端開發管道。

就本歷程而言，您不需要完全了解Cloud Manager。 Cloud Manager從高層面來說由數個層級的結構組成。

![Cloud Manager結構](assets/cloud-manager-structure.png)

* **租用戶**  — 每個客戶都布建了租用戶。
* **計畫。**  — 每個租戶都有一個或多個程式，這些程式通常反映客戶的授權解決方案。
* **環境**  — 每個方案有多個環境，例如針對即時內容的生產、一個用於測試，以及一個用於開發用途。
* **存放庫**  — 環境中有Git存放庫，可維護應用程式和前端程式碼。
* **工具與工作流程**  — 管道管理從儲存庫到環境的代碼部署。

範例通常有助於將此階層與情境結合。

* WKND Travel and Adventure Enterprises可能是 **用戶** 以旅行相關媒體為主。
* WKND Travel and Adventure Enterprises租戶可能有兩個 **方案**:WKND雜誌的一個網站計畫和WKND媒體的一個資產計畫。
* WKND雜誌和WKND Media節目都有開發、預備和製作 **環境**.

## 快速站點建立前端開發流程 {#flow}

即使您尚未擁有豐富的Cloud Manager使用經驗，整體流程仍簡單且直覺。

1. AEM管理員登入AEM環境，並使用網站範本建立新網站。
1. Cloud Manager管理員會在Cloud Manager中建立前端管道。 管道可協調從Git存放庫到AEM環境的程式碼部署。
1. AEM管理員會從程式的AEM例項匯出網站主題，並提供給前端開發人員。
1. Cloud Manager管理員可授予AEM Git存放庫的前端開發人員存取權，以便提交自訂內容。
1. 前端開發人員會擷取存取憑證以存取git和管道。
1. 前端開發人員可自訂主題，使用網站的實際內容透過Proxy進行測試，然後將變更提交至Git存放庫。
1. 前端開發人員執行管道，將主題自訂部署至程式的生產環境。

![快速網站建立流程](assets/qsc-flow.png)

使用「快速網站建立」工具的主要優點是，純前端開發人員只負責實際的自訂。 前端開發人員沒有與AEM互動，或需要任何AEM知識。

## 下一步 {#what-is-next}

現在您已完成AEM快速網站建立歷程的這一部分，您應：

* 了解AEM Sites與Cloud Manager如何共同合作以促進前端開發
* 了解前端自訂步驟如何與AEM完全分離，且不需要AEM知識。

基於此知識，並透過接下來檢閱檔案，繼續建立AEM快速網站的歷程 [從模板建立站點，](create-site.md) 您可在此了解如何使用範本快速建立新AEM網站。

## 其他資源 {#additional-resources}

建議您透過檢閱檔案，繼續進行快速網站建立歷程的下一個階段 [從模板建立站點，](create-site.md) 以下是一些額外的選用資源，可更深入探討本檔案中提及的一些概念，但您不需要這些資源即可繼續進行歷程。

* [Cloud Manager檔案](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html)  — 如果您想要取得Cloud Manager功能的詳細資訊，可直接參閱深入的技術檔案。
* [角色型權限](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/role-based-permissions.html) - Cloud Manager已預先設定角色，並擁有適當權限。 請參閱本檔案，了解這些角色的詳細資訊以及如何管理這些角色。
* [npm](https://www.npmjs.com)  — 用來快速建立網站的AEM主題是以npm為基礎。
* [webpack](https://webpack.js.org)  — 用於快速建立網站的AEM主題依賴webpack。
