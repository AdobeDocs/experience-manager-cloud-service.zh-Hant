---
title: 影像編輯器
description: 影像編輯器是AEM的一項核心功能，元件可運用它來協助內容作者操控影像。
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# 影像編輯器 {#image-editor}

影像編輯器是AEM的一項核心功能，元件可運用它來協助內容作者操控影像。

## 影像地圖的相對單位 {#relative-units-for-image-map}

「影像編輯器」會將影像地圖區域以絕對和相對單位持續儲存。 當提供相對單位作為資料屬性以動態調整回應式影像元件中使用者端影像地圖（相對於影像大小）的大小時，相對單位會很有用。

### imageMap屬性 {#imagemap-property}

影像地圖座標會持續儲存至JCR做為 `imageMap` 屬性。 其格式如下。

屬性會將地圖區域儲存如下：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG影像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從DAM拖放SVG資產以及從本機檔案系統上傳SVG檔案。

## 依MIME型別啟用外掛程式 {#enabling-plugins-by-mime-type}

在某些情況下，由於伺服器端處理缺乏支援，因此必須限制特定MIME型別的編寫動作。 例如，可能不允許編輯SVG影像。

MIME型別可以設定影像編輯器中的外掛程式，選擇性地啟用 `supportedMimeTypes` 屬性（在個別外掛程式的設定節點上）。

### 範例 {#example}

例如，我們假設僅允許裁切功能用於GIF、JPEG、PNG、WEBP和TIFF影像。

此 `supportedMimeTypes` 然後，屬性必須設定為外掛程式之設定節點上允許的MIME型別字串， `cq:editConfig` 影像元件的節點。

`/apps/core/wcm/components/image/v2/image/cq:editConfig`

```xml
 jcr:primaryType="cq:EditConfig">
     <cq:dropTargets jcr:primaryType="nt:unstructured">
         <image ...>
            ...
         </image>
     </cq:dropTargets>
     <cq:inplaceEditing
         jcr:primaryType="cq:InplaceEditingConfig"
         active="{Boolean}true"
         editorType="image">
         <config jcr:primaryType="nt:unstructured">
             <plugins jcr:primaryType="nt:unstructured">
                 <crop
                     jcr:primaryType="nt:unstructured"
                     supportedMimeTypes="[image/gif,image/jpeg,image/png,image/webp,image/tiff]"
                     features="*">
                     <aspectRatios jcr:primaryType="nt:unstructured">
                        ...
                     </aspectRatios>
                 </crop>
                 ...
             </plugins>
             <ui jcr:primaryType="nt:unstructured">
                 ...
             </ui>
         </config>
     </cq:inplaceEditing>
 </jcr:root>
```
