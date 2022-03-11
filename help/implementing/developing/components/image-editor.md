---
title: 影像編輯器
description: 影像編輯器是核心部分AEM，可由元件利用，以便於內容作者對影像的操作。
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# 影像編輯器 {#image-editor}

影像編輯器是核心部分AEM，可由元件利用，以便於內容作者對影像的操作。

## 影像映射的相對單位 {#relative-units-for-image-map}

影像編輯器將影像映射區域保留為絕對和相對單位。 當提供相對單元作為資料屬性用於在響應影像元件中動態調整客戶端上的影像映射（相對於影像大小）的大小時，相對單元是有用的。

### imageMap屬性 {#imagemap-property}

將影像映射坐標保持為JCR `imageMap` 屬性。 它具有以下格式。

該屬性按如下方式儲存地圖區域：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例:

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG映像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從DAM拖放SVG資產和從本地檔案系統上載SVG檔案。

## 按MIME類型啟用插件 {#enabling-plugins-by-mime-type}

在某些情況下，由於在伺服器端處理中缺乏支援，某些MIME類型的創作操作必須受到限制。 例如，可能不允許編輯SVG影像。

通過設定MIME類型，可以有選擇地啟用影像編輯器中的插件 `supportedMimeTypes` 單個插件的配置節點上的屬性。

### 範例 {#example}

例如，我們假設只應允許GIF、JPEG、PNG、WEBP和TIFF影像具有裁剪能力。

的 `supportedMimeTypes` 然後，必須將屬性設定為插件配置節點上允許的MIME類型的字串 `cq:editConfig` 影像元件的節點。

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
