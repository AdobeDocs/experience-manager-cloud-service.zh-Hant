---
title: 設定通用編輯器的Assets選取器
description: 瞭解如何設定資產選擇器以用於通用編輯器。
feature: Developing
role: Admin, Developer
source-git-commit: 0ed57393afaf9af3258dacdcb043487f4a098e03
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 1%

---


# 設定通用編輯器的Assets選取器 {#configure-assets-selector}

瞭解如何設定資產選擇器以用於通用編輯器。

## 概觀 {#overview}

Universal Editor使用[資產選擇器](/help/assets/overview-asset-selector.md#using-asset-selector)來允許作者瀏覽及選取要插入其內容的資產。

可以使用[元件篩選器，在通用編輯器中設定資產選取器。](/help/implementing/universal-editor/filtering.md)本檔案說明可用的組態選項。

>[!NOTE]
>
>啟動Universal Editor專案時，資產選擇器沒有適當篩選器。 作者將有權存取其使用者許可權通常允許的所有資產。

## 篩選器定義 {#filter-definition}

資產選擇器的篩選定義有一個簡單的結構。

```json
[
  {
    "id": "assets-filter",
    "assets": {...}
   }
]
```

## 篩選器選項 {#filter-options}

`assets`篩選器可以有下列選項。

* `deliveryTier?`： — 定義要使用下列哪個傳遞層級：
   * `dm`： Dynamic Media （偏好設定），必要時可遞補為`publish`
   * `publish`： AEM發佈執行個體
* `repoNames?`：字串 — 可用來選取影像的AEM存放庫清單。
   * 預設：所有傳遞存放庫
* `selectionTier?`：字串 — 要從中選取資產的AEM層級
   * 預設： `["author", "delivery"]`
* `disableRemote?`：布林值 — 停用遠端存放庫支援
* `preselectedTypes?`：字串 — 要套用為資產選擇器中預設篩選器的預先選取檔案型別
* `minMaxDimensions?`：物件 — 提供最小和/或最大尺寸（以畫素為單位），以套用為資產選擇器中的預設濾鏡
   * `widthMin?`：數字 — 最小寬度
   * `widthMax?`：數字 — 寬度上限
   * `heightMin?`：數字 — 最小高度
   * `heightMax?`： Number — 最大高度
* `minMaxFileSize?`：物件 — 提供最小和/或最大檔案大小（以位元組為單位），以套用為資產選擇器中的預設篩選器
   * `min?`：數字 — 檔案大小下限
   * `max?`： number — 檔案大小上限
* `customFileTypeFilters?`：物件 — 提供要顯示在資產選擇器中的自訂檔案型別篩選器
   * `label`：字串 — 要在資產選取UI中顯示的標籤
   * `value`：字串 — 要篩選的檔案型別的值
* `displayFilters?`：布林值 — 用來停用資產選擇器中的篩選器UI；預設為true

## 範例 {#example}

下列範例包含大部分的選項，以供說明使用。

```json
[
  {
    "id": "assets-filter",
    "assets": {
      "deliveryTier": "dm",
      "repoNames": ["thisRepo", "thatRepo"],
      "selectionTier": ["author", "delivery"],
      "disableRemote": true,
      "preselectedTypes": ["png", "svg", "jpg", "gif"],
      "minMaxDimensions": {
        "widthMin": 640,
        "widthMax": 640,
        "heightMin": 480,
        "heightMax": 480
      },
      "minMaxFileSize": {
        "min": 1024,
        "max": 1024
      }
    }
   }
]
```

## 其他資源 {#additional-resources}

如需有關資產選擇器的詳細資訊，請參閱資產檔案中的檔案[Micro-Frontend資產選擇器](/help/assets/overview-asset-selector.md#using-asset-selector)。
