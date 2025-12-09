---
title: 互動式通訊(IC)編輯器快速入門
description: 互動式通訊可讓組織設計和提供個人化的資料導向通訊。
products: SG_EXPERIENCEMANAGER/Cloud Service/FORMS
feature: Interactive Communication
role: User, Developer, Admin
source-git-commit: d24e88b545a17e50c1e80e1aedbb1d0adf55f609
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 11%

---


# 互動式通訊(IC)編輯器快速入門

>[!NOTE]
>
> 互動式通訊功能在早期採用者程式中提供。 使用您的工作郵件地址寄送電子郵件至 `aem-forms-ea@adobe.com` 請求存取權限。

>[!IMPORTANT]
>
> **文件內容可能隨時變更**：此提示庫目前正在針對產品進行測試，可能會進行更新和修訂。隨著表單體驗建立工具在早期採用者方案期間持續發展，相關的提示、範例和最佳做法可能會有所變更。

Adobe Experience Manager (AEM) Forms中的&#x200B;**互動式通訊(IC)編輯器**&#x200B;可讓組織跨數位和列印管道設計和傳遞個人化的資料導向通訊，例如報表、發票和信件。 本指南概述如何入門 — 從上線到瀏覽IC編輯器介面。


## 上線和存取

### 存取需求

若要使用互動式通訊，請確定您的AEM Forms as a Cloud Service環境包含&#x200B;**AEM Forms附加元件**，而且您的帳戶擁有適當的許可權。

### 驗證瀏覽器

若要瞭解支援的瀏覽器和使用者端平台，請遵循連結的文章[支援的使用者端平台](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/overview/supported-platforms)

>[!NOTE]
>
> **支援發行週期快速的瀏覽器：**
> Firefox、Chrome 及 Edge 定期發佈更新。Adobe 致力於對這些瀏覽器即將推出的版本維持上述支援等級。

### 設定使用者角色和許可權

對IC編輯器功能的存取權由AEM[中的](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions)使用者角色所控制。 以下是建立及管理互動式通訊的主要角色：

| **角色** | **說明** | **金鑰許可權** |
| --------------------- | ---------------------------------------------------------- | -------------------------------------------- |
| **表單作者** | 建立和編輯互動式通訊。 | 建立、編輯、預覽和發佈互動通訊。 |
| **範本作者** | 為互動式通訊設計可重複使用的範本。 | 建立並鎖定範本，定義版面。 |
| **管理員** | 管理使用者存取、許可權和設定。 | 指派角色、管理範本、發佈互動通訊。 |
| **FDM作者** | [建立和管理表單資料模型(FDM)](https://experienceleague.adobe.com/zh-hant/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/create-form-data-models)以進行資料整合。 | 建立、編輯和設定資料來源和模型。 |

>[!NOTE]
>
> 確定使用者屬於適當的AEM群組（例如，`forms-user`、`fdm-author`、`template-authors`）以存取對應的功能。

## 存取IC編輯器

1. 登入您的&#x200B;**AEM Forms as a Cloud Service**&#x200B;執行個體。
2. 導覽至&#x200B;**Forms >互動式通訊**。
3. 按一下&#x200B;**建立** → **互動式通訊**。
4. 選擇&#x200B;**範本**、設定資料來源，然後按一下&#x200B;**建立**&#x200B;以開啟&#x200B;**互動式通訊編輯器**。

編輯器提供統一的環境，用於設計、預覽和管理列印和Web版本的通訊。

## 瀏覽介面

**互動式通訊編輯器**&#x200B;介面的設計可讓作者以直覺式方式存取所有設計工具和組態選項。

![尋找IC檔案](/help/forms/interactive-communication/assets/navigate-the-interface.png)

### 1.頂端工具列

![尋找IC檔案](/help/forms/interactive-communication/assets/tool-bar.png)

**位置：**&#x200B;最上層區段

**用途：**&#x200B;提供環境存取權和全域動作。

**包含：**

顯示&#x200B;**Adobe Experience Cloud環境** （例如，預備），以及管理使用者設定和環境存取許可權的&#x200B;**專案標題**、**Beta意見**、**通知**&#x200B;和&#x200B;**設定檔控制項**。

### 2.標籤列（設計/主標籤與檔案控制項）

![尋找IC檔案](/help/forms/interactive-communication/assets/tab-bar.png)

**位置：**&#x200B;在頂端標題下方

**用途：**&#x200B;管理檢視和通訊檔案。

**包含：**

**索引標籤：**&#x200B;在&#x200B;**設計檢視**&#x200B;和&#x200B;**主版頁面檢視**&#x200B;之間切換，以進行配置和可重複使用的元素設計

**檔案名稱：**&#x200B;顯示目前通訊的標題（例如，ic-11）

**檢視控制項：**&#x200B;選項，例如規則、建立、縮放(85%)、還原/重做、刪除、PDF預覽和儲存

### 3.左側面板（導覽與元件工具）

![尋找IC檔案](/help/forms/interactive-communication/assets/left-panel.png)

**位置：**&#x200B;介面左側

**用途：**&#x200B;存取專案結構、可重複使用的資產和資料繫結。

**包含：**

* **首頁：**&#x200B;將使用者帶至互動式通訊(IC)主畫面，您可以在此檢視及管理現有的IC和資料夾。

* **功能表面板：**&#x200B;顯示檢視相關選項，例如「尺標」、「物件邊界」、「貼齊格點」、「貼齊功能物件」和「匯入XDP功能」。

* **階層檢視：**&#x200B;顯示通訊的元件結構，顯示頁面、面板和子表單的組織。

* **元件庫：**&#x200B;包含可拖曳至畫布的設計元素，例如文字、影像、子表單和條碼。

* **片段：**&#x200B;可重複使用多個通訊中預先定義的設計和內容區塊。

* **資料模型：**&#x200B;將通訊連線至基礎表單資料模型(FDM)，以繫結動態資料。

### 4.中部Workspace （設計畫布）

![尋找IC檔案](/help/forms/interactive-communication/assets/canvas.png)

**位置：**&#x200B;介面中心

**用途：**&#x200B;設計互動式通訊的主要工作區。

**功能：**

* 從程式庫中拖放元件

* 排列和格式化視覺版面

* 新增或編輯頁面、子表單和欄位

* 使用左下方的控制項，在頁面之間導覽（例如「1/1」）

* 發佈前預覽最終版面

### 5.右側面板（「屬性」面板）

![尋找IC檔案](/help/forms/interactive-communication/assets/right-panel.png)

**位置：**&#x200B;畫面右側

**用途：**&#x200B;自訂元件行為和樣式。

**包含：**

* 一般設定（名稱、型別、流動/定位）

* 版面與外觀選項

* 分頁、位置、顯示和資料繫結控制項