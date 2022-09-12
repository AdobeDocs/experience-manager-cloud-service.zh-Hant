---
title: ContextHub診斷
description: ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概觀
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# ContextHub診斷 {#contexthub-diagnostics}

ContextHub提供診斷頁面，您可在其中查看ContextHub架構的概觀。 若要開啟頁面，請前往 `contexthub.diagnostics.html` AEM author例項的頁面，例如：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁提供了有關已建立的儲存和UI模組、已載入的客戶端庫資料夾以及指向有用頁的連結的資訊。

>[!NOTE]
>
>要返回診斷資訊，必須啟用調試模式，否則診斷頁將為空。 請參閱 [此文檔](configuring-contexthub.md#debugging-contexthub) 以取得如何啟用偵錯模式的詳細資訊。

## 商店 {#stores}

「儲存」區段會列出所有已設定的ContextHub儲存。 清單中的每個項目都包含下列資訊：

* **標題：** 此 [儲存類型](sample-stores.md) 店的基礎。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義儲存類型的儲存庫節點的路徑。
* **clientlibs:** 載入的用戶端程式庫類別，用於實作儲存類型。

## 模組 {#modules}

「模組」區段會列出所有已設定的ContextHub UI模組。 清單中的每個項目都包含下列資訊：

* **標題：** 此 [UI模組類型](sample-modules.md) UI模組所依據之資訊。
* **路徑：** 保存配置的儲存庫節點的路徑。
* **resourceType:** 定義UI模組類型的儲存庫節點路徑。
* **clientlibs:** 載入並實作UI模組類型的用戶端程式庫的類別。

## Clientlibs {#clientlibs}

「Clientlibs」區段會列出 [客戶端庫資料夾](/help/implementing/developing/introduction/clientlibs.md) ContextHub已載入。 用戶端程式庫的分類如下：

* **kernel.js:** 實作ContextHub架構、區段引擎和儲存類型的用戶端程式庫。
* **ui.js:** 實作ContextHub UI和UI模組類型的用戶端程式庫。
* **style.css:** 從用戶端程式庫載入的CSS檔案。

## URL {#urls}

「URL」區段包含ContextHub功能的連結：

* **配置編輯器：** 開啟 [「ContextHub配置」頁](configuring-contexthub.md) 您可以在此設定商店、UI模式和UI模組。
* **ContextHub模組的設定：** 開啟 `/etc/cloudsettings/default/contexthub.config.kernel.js` 檔案，其中包含ContextHub存放區設定的Javascript物件表示。
* **ContextHub UI的設定：** 開啟 `/etc/cloudsettings/default/contexthub.config.ui.js` 檔案，其中包含ContextHub UI模式設定的Javascript物件表示。
* **kernel.js:** 開啟 `/etc/cloudsettings/default/contexthub.kernel.js` 檔案，包含實作ContextHub架構、區段引擎和儲存類型之用戶端程式庫的原始碼。
* **ui.js:** 開啟 `/etc/cloudsettings/default/contexthub.ui.js` 檔案，包含實作ContextHub UI和UI模組類型的用戶端程式庫的原始碼。
* **style.css:** 開啟 `/etc/cloudsettings/default/contexthub.styles.css` 檔案，其中包含ContextHub UI和UI模組的CSS樣式。
