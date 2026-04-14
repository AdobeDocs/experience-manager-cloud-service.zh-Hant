---
title: 專案檔案技能
description: 瞭解Experience現代化代理程式的檔案技能如何協助您加速專案移交。
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 90fb75c7febc8a8138e13a2f3ff872f38eeb3baa
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# 專案檔案技能 {#project-documentation}

瞭解Experience現代化代理程式的檔案技能如何協助您加速專案移交。

## 加速專案移交 {#project-handovers}

[Experience Modernization Agent](/help/ai-in-aem/agents/brand-experience/modernization/overview.md)可以自動產生AEM Edge Delivery Services專案的專案檔案指南，其功能包括：

* **專案逐步說明** — 說明專案設定、結構和慣例，無需手動完成
* **模組和元件組織** — 清楚說明區塊、模組和元件的組織方式以及它們彼此的關係
* **角色型指南** — 針對作者、開發人員和管理員提供的檔案，讓每位團隊成員都能取得他們所需的內容

這簡化了AEM Edge Delivery Services專案的專案移交。

## 先決條件 {#prerequisites}

使用此技能前，請先確認下列事項。

* 您的專案必須簽出到主控台中的工作區。
* 您必須對要建立檔案的專案具有管理員許可權。
* 主控台中必須允許代理程式許可權。
   * 在主控台設定中選取選項&#x200B;**允許LLM代表我存取admin.hlx.page** [。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   * 如果未啟用此選項，代理程式將會根據其可存取的程式碼庫產生檔案。

## 建立專案檔案 {#creating-documentation}

先決條件滿足後，您只需要求代理程式為您的專案建立檔案。

1. 在聊天中詢問「建立此專案的檔案」。
1. 如果代理程式要求，請提供專案的組織名稱。
1. 代理程式會詢問您要建立哪些檔案。 通常您會選取&#x200B;**全部**。

   ![建立檔案](assets/select-documentation.png)

1. 建立之後，參考線就會放置在您的工作區中。 選取其中一個以檢視說明，然後按一下連結以下載完整的PDF。

   ![檔案已建立](assets/documentation-created.png)

您可以直接儲存PDF以提供給您的團隊，或將其上傳為DA內容的其餘部分。

![管理員指南](assets/admin-guide.png)

>[!NOTE]
>
>如果您無權存取Edge Delivery Services admin API，或控制檯設定中的&#x200B;**允許LLM代表我存取admin.hlx.page** [選項。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)未啟用，代理程式將會根據其可存取的程式碼庫產生檔案。

## 疑難排解 {#troubleshooting}

以下是使用專案檔案技能時經常遇到的錯誤訊息，以及如何解決這些錯誤。

### 「存取遭拒」或「未獲授權」 {#unauthorized}

* **原因：**&#x200B;缺少管理員許可權或未啟用代理程式許可權
* **解決方案：**
   1. 確認您擁有專案的管理員存取權
   1. 在主控台設定中選取選項&#x200B;**允許LLM代表我存取admin.hlx.page** [。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)

### 「找不到專案」 {#not-found}

* **原因：**&#x200B;存放庫未在工作區中籤出
* **解決方案：**
   1. 簽出專案存放庫
   1. 確保您在正確的工作區

### 「設定API錯誤」 {#api-error}

* **原因：**&#x200B;無法存取Edge Delivery Services設定服務API
* **解決方案：**
   1. 在主控台設定中選取選項&#x200B;**允許LLM代表我存取admin.hlx.page** [。](/help/ai-in-aem/agents/brand-experience/modernization/console.md#settings-view)
   1. 檢查您的網路/VPN連線
   1. 確認專案的管理員存取權
