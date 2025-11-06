---
title: 影像編輯器
description: 影像編輯器是AEM的核心元件，元件可使用它來協助內容作者操控影像。
exl-id: c8ae4f59-75b1-49b4-8dd4-957d2e33000b
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 10%

---

# 影像編輯器 {#image-editor}

影像編輯器是AEM的核心元件，元件可使用它來協助內容作者操控影像。

## 影像地圖的相對單位 {#relative-units-for-image-map}

「影像編輯器」會以絕對和相對單位保留影像地圖區域。 在回應式影像元件的使用者端上，當提供相對單位作為資料屬性以動態調整影像地圖（相對於影像大小）的大小時，這些單位就相當實用。

### imageMap屬性 {#imagemap-property}

影像編輯器會將影像地圖座標以`imageMap`屬性的形式保留至JCR。 其格式如下。

屬性會依下列方式儲存地圖區域：

`[area1][area2][...]`

區域格式：

`[SHAPE(COORDINATES)"HREF"|"TARGET"|"ALT"|(RELATIVE_COORDINATES)]`

範例：

`[rect(0,0,10,10)"https://www.adobe.com"|"_self"|"alt"|(0,0,0.8,0.8)]`
`[circle(10,10,10)"https://www.adobe.com"|"_self"|"alt"|(0.8,0.8,0.8)]`

## 支援SVG影像 {#support-for-svg-images}

影像編輯器支援可縮放向量圖形(SVG)。

* 支援從 DAM 拖放 SVG 資產以及上傳從本機檔案系統上傳的 SVG 檔案。

## 依MIME型別啟用外掛程式 {#enabling-plugins-by-mime-type}

在某些情況下，由於伺服器端處理缺乏支援，因此必須限制特定MIME型別的編寫動作。 例如，可能不允許編輯SVG影像。

在個別外掛程式的設定節點上設定`supportedMimeTypes`屬性，MIME型別即可選擇性地啟用影像編輯器中的外掛程式。

### 範例 {#example}

例如，假設僅允許裁切功能用於GIF、JPEG、PNG、WEBP和TIFF影像。

然後，必須在影像元件的`supportedMimeTypes`節點上的外掛程式的設定節點上，將`cq:editConfig`屬性設定為允許的MIME型別字串。

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
