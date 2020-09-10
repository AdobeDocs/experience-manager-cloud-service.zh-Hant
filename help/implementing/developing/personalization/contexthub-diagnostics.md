---
title: ContextHub診斷
description: ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概述
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# ContextHub診斷 {#contexthub-diagnostics}

ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概述。 若要開啟頁面，請至AEM作 `contexthub.diagnostics.html` 者例項的頁面，例如：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁提供有關已建立的儲存和UI模組、已載入的客戶端庫資料夾以及到有用頁面的連結的資訊。

>[!NOTE]
>
>要返回診斷資訊，必須啟用調試模式，否則診斷頁將為空。 如需如何 [啟用除錯模式](configuring-contexthub.md#debugging-contexthub) ，請參閱本檔案。

## 商店 {#stores}

「儲存」部分列出所有已配置的ContextHub儲存。 清單中的每個項目都包含下列資訊：

* **標題：** 商店 [所依據的](sample-stores.md) 「商店」類型。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義儲存類型的儲存庫節點的路徑。
* **clientlibs:** 實施儲存類型的載入客戶端庫的類別。

## 模組 {#modules}

「模組」部分列出了已配置的所有ContextHub UI模組。 清單中的每個項目都包含下列資訊：

* **標題：** UI [模組所基於的](sample-modules.md) 「UI模組」類型。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義UI模組類型的儲存庫節點的路徑。
* **clientlibs:** 實施UI模組類型的已載入客戶端庫的類別。

## Clientlibs {#clientlibs}

Clientlibs區段會列出ContextHub已載入的所有用戶端程式庫資料夾。 客戶端庫分類如下：

* **kernel.js:** 實作ContextHub架構、區段引擎和儲存類型的用戶端程式庫。
* **ui.js:** 實作ContextHub UI和UI模組類型的用戶端程式庫。
* **style.css:** 從用戶端程式庫載入的CSS檔案。

## URL {#urls}

URL區段包含ContextHub功能的連結：

* **配置編輯器：** 開啟「 [ContextHub設定」頁面](configuring-contexthub.md) ，您可在此處設定儲存區、UI模式和UI模組。
* **ContextHub模組的設定：** 開啟檔 `/etc/cloudsettings/default/contexthub.config.kernel.js` 案，其中包含ContextHub儲存區組態的Javascript物件表示法。
* **ContextHub UI的設定：** 開啟檔 `/etc/cloudsettings/default/contexthub.config.ui.js` 案，其中包含ContextHub UI模式設定的Javascript物件表示法。
* **kernel.js:** 開啟檔 `/etc/cloudsettings/default/contexthub.kernel.js` 案，其中包含實作ContextHub架構、區段引擎和儲存類型之用戶端程式庫的原始碼。
* **ui.js:** 開啟檔 `/etc/cloudsettings/default/contexthub.ui.js` 案，其中包含實作ContextHub UI和UI模組類型之用戶端程式庫的原始碼。
* **style.css:** 開啟檔 `/etc/cloudsettings/default/contexthub.styles.css` 案，其中包含ContextHub UI和UI模組的CSS樣式。
