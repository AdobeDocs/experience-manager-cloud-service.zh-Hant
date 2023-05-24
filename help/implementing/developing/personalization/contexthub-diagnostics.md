---
title: ContextHub 診斷
description: ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# ContextHub 診斷 {#contexthub-diagnostics}

ContextHub提供診斷頁面，您可在其中檢視ContextHub架構的概觀。 若要開啟頁面，請前往 `contexthub.diagnostics.html` AEM編寫執行個體的頁面，例如：

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

「ContextHub診斷」頁面提供有關已建立的存放區和UI模組、已載入的使用者端程式庫資料夾，以及實用頁面的連結的資訊。

>[!NOTE]
>
>為了傳回診斷資訊，必須啟用偵錯模式，否則診斷頁面將為空白。 請參閱 [本檔案](configuring-contexthub.md#debugging-contexthub) 以取得如何啟用偵錯模式的詳細資訊。

## 商店 {#stores}

存放區區段會列出所有已設定的ContextHub存放區。 清單中的每個專案都包含下列資訊：

* **標題：** 此 [存放區型別](sample-stores.md) 存放區所根據的。
* **路徑：** 存放設定的存放庫節點的路徑。
* **resourceType：** 定義存放區型別的存放庫節點的路徑。
* **clientlibs：** 已載入且實作存放區型別的使用者端程式庫的類別。

## 模組 {#modules}

模組區段會列出所有已設定的ContextHub UI模組。 清單中的每個專案都包含下列資訊：

* **標題：** 此 [UI模組型別](sample-modules.md) UI模組所根據。
* **路徑：** 存放設定的存放庫節點的路徑。
* **resourceType：** 定義UI模組型別的存放庫節點的路徑。
* **clientlibs：** 已載入且實作UI模組型別的使用者端程式庫的類別。

## Clientlibs {#clientlibs}

Clientlibs區段會列出所有的 [使用者端資料庫資料夾](/help/implementing/developing/introduction/clientlibs.md) ContextHub已載入。 使用者端程式庫可依下列方式分類：

* **kernel.js：** 實作ContextHub架構、區段引擎和存放區型別的使用者端資料庫。
* **ui.js：** 實作ContextHub UI和UI模組型別的使用者端程式庫。
* **style.css：** 從使用者端程式庫載入的CSS檔案。

## URL {#urls}

URL區段包含ContextHub功能的連結：

* **設定編輯器：** 開啟 [ContextHub設定頁面](configuring-contexthub.md) 您可以在此處設定存放區、UI模式和UI模組。
* **ContextHub模組的設定：** 開啟 `/etc/cloudsettings/default/contexthub.config.kernel.js` 檔案，其中包含ContextHub存放區設定的Javascript物件表示。
* **ContextHub UI的設定：** 開啟 `/etc/cloudsettings/default/contexthub.config.ui.js` 檔案，其中包含ContextHub UI模式設定的Javascript物件表示。
* **kernel.js：** 開啟 `/etc/cloudsettings/default/contexthub.kernel.js` 檔案，其中包含實作ContextHub架構、區段引擎和存放區型別的使用者端程式庫原始碼。
* **ui.js：** 開啟 `/etc/cloudsettings/default/contexthub.ui.js` 檔案，其中包含實作ContextHub UI和UI模組型別的使用者端程式庫原始碼。
* **style.css：** 開啟 `/etc/cloudsettings/default/contexthub.styles.css` 檔案，其中包含ContextHub UI和UI模組的CSS樣式。
