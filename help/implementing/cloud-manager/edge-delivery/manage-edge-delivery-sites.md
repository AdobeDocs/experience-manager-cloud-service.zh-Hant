---
title: 在 Cloud Manager 中管理 Edge Delivery 網站
description: 了解如何將內容傳遞網路設定新增至 Edge Delivery 網站或刪除 Edge Delivery 網站。
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 960aa3c6-27b9-44b1-81ea-ad8c5bbc99a5
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 100%

---

# 在 Cloud Manager 中管理 Edge Delivery 網站 {#manage-edge-delivery-sites}

了解如何將內容傳遞網路設定新增至現有網站，藉此在 Cloud Manager 中管理 Edge Delivery 網站。或了解如何刪除 Edge Delivery 網站。

## 將網域對應新增至現有的 Edge Delivery 網站 {#add-cdn-to-edge-delivery-site}

請參閱[新增網域對應](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md)。

## 重新命名 Edge Delivery 網站 (#rename-edge-delivery-site)

在 Adobe Cloud Manager 中，您可能會因為多種原因而想要重新命名 Edge Delivery 網站：

* **清晰度和組織性**：以更好的方式說明網站的用途或其相關環境 (例如生產、中繼)。
* **避免混淆**：如果正在使用多個網站，重新命名有助於輕鬆區分它們，進而減少將設定或更新套用到錯誤網站上的機會。
* **標準化**：遵循與組織指導方針相符的一致命名慣例，以便更輕鬆管理和稽核。

**若要重新命名 Edge Delivery 網站：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」主控台中，選取設定有 Edge Delivery Services 且您要在其中新增 Edge Delivery 網站的程式。
1. 執行下列任一項：

   * 在「**程式概觀**」頁面上，按一下「**Edge Delivery**」索引標籤。在 Edge Delivery 網站表格中，按一下要重新命名之網站所在列尾的省略符號。
按一下「**重新命名**」。
   * 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。在「**服務**」標頭下方，按一下 ![網頁頁面圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery 網站**」。在 Edge Delivery 網站表格中，按一下要重新命名之網站所在列尾的![「更多」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。按一下「**重新命名**」。

1. 在「**編輯 Edge Delivery 網站**」對話框中，於「**網站名稱**」文字欄位輸入網站的新名稱。

1. 按一下「**編輯**」。

## 刪除 Edge Delivery 網站 {#delete-edge-delivery-site}

如果刪除 Edge Delivery Services 網站，所有關聯的內容傳遞網路設定也都會移除。此動作會中斷自訂網域和網站之間的連線。如需更多詳細資訊，請參閱內容傳遞網路設定。<!-- https://wiki.corp.adobe.com/display/DMSArchitecture/%5BKT%5D+Cloud+Manager+2024.9.0+Release -->

**若要刪除 Edge Delivery 網站：**

1. 在 [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) 登入 Cloud Manager，然後選取適當的程式。
1. 在「**[我的程式](/help/implementing/cloud-manager/navigation.md#my-programs)**」主控台中，選取設定有 Edge Delivery Services 且您要在其中新增 Edge Delivery 網站的程式。
1. 執行下列任一項：

   * 在「**程式概觀**」頁面上，按一下「**Edge Delivery**」索引標籤。在 Edge Delivery 網站表格中，按一下要移除之網站所在列尾的![「更多」圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。
按一下![刪除 Edge Delivery 網站圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)「**刪除**」，然後再按一下「**刪除**」以確認移除網站。

     ![從「Edge Delivery」索引標籤新增 Edge Delivery 網站](/help/implementing/cloud-manager/assets/cm-eds-delete1.png)

   * 在頁面左上角，按一下 ![顯示選單圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) 以顯示左側選單。在「**服務**」標題下方，按一下 ![Edge Delivery 網站的網頁圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg)「**Edge Delivery 網站**」。在 Edge Delivery 網站表格中，按一下要移除之網站所在列尾的![更多圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg)。按一下![刪除 Edge Delivery 網站圖示](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Delete_18_N.svg)「**刪除**」，然後再按一下「**刪除**」以確認移除網站。

     ![從「Edge Delivery 網站」按鈕新增 Edge Delivery 網站](/help/implementing/cloud-manager/assets/cm-eds-delete2.png)

## 管理在 Helix 4 和 Helix 5 之間移轉的 Edge Delivery 網站

使用 `/program/{programId}/site/{siteId}` API 端點，在 Helix 4 和 Helix 5 之間移轉的 Edge Delivery 網站。

>[!IMPORTANT]
>
>Helix 4 網站的 CDN 設定無法自動移轉到 Helix 5。此限制存在的原因是客戶的生產環境可能仍在 Helix 4 上執行，而其 Helix 5 版本仍在開發中。

**先決條件**

* `sitename` 必須已經存在。
* 知道適當的 `branchName`、Helix `version`和 `repo` 值。
* 移轉僅會修改 `branchName`、Helix `version`和 `repo`。所有者欄位無法變更。

**API 格式**

```http
PUT /api/program/{programId}/site/{siteId}
```

**請求內文參數**
為 Edge Delivery 網站建立覆寫，以強制執行請求內文中指定的來源。

```json
{
  "sitename": "<required site name>",
  "branchName": "<git branch>",
  "version": "v4" | "v5",
  "repo": "<git repository name>"
}
```

### 範例 1：移轉至 Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix5",
  "branchName": "branch",
  "version": "v5",
  "repo": "my-website"
}
```

**來源 URL 結果**
傳回具有以下來源 URL 的 Edge Delivery 網站：

`"origin": "branch--my-website–Teo48.aem.live"`


### 範例 2：移轉至 Helix 4

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-site-new-helix4",
  "branchName": "branch",
  "version": "v4",
  "repo": "my-website"
}
```

**來源 URL 結果**
傳回具有以下來源 URL 的 Edge Delivery 網站：

`"origin": "branch--my-website--Teo48.hlx.live"`

### 範例 3：將無存放庫網站移轉至 Helix 5

**http**

```http
PUT /api/program/{programId}/site/{siteId}
```

**json**

```json
{
  "sitename": "test-reposless-website",
  "branchName": "main",
  "version": "v5",
  "repo": "my-reposless-website"
}
```

**來源 URL 結果**
傳回具有以下來源 URL 的 Edge Delivery 網站：

`"origin": "main--my-repoless-website--Teo48.aem.live"`

## 記錄支援服務單 {#eds-support-ticket}

{{support-ticket}}
