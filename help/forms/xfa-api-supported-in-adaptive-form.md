---
title: XFA在基於XDP的自適應Forms中的支援
seo-title: XFA support in XDP-based Adaptive Forms
description: 列出Adaptive Forms中支援的XFA事件、屬性、指令碼和驗證。
seo-description: Lists supported XFA events, properties, scripts, and validation in Adaptive Forms.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '683'
ht-degree: 5%

---


# XFA在基於XDP的自適應Forms中的支援{#xfa-support-in-xdp-based-adaptive-forms}

## 簡介 {#introduction}

自適應Forms支援在XDP檔案中定義的各種XFA事件、屬性、指令碼和驗證，包括：

* 執行在XDP檔案中的事件上定義的指令碼。
* 捕獲XDP檔案中欄位的預設值和行為屬性。
* 執行XDP檔案中定義的驗證指令碼。

當基於XDP檔案建立自適應表單時，屬性、事件和驗證將在創作UI表單中自動填充。 但是，表單作者可以覆蓋其中的一些元素以建立替代體驗。

本文列出了在自適應Forms中獲得支援的XFA事件、屬性和驗證，並說明了如何在自適應Forms中覆蓋這些事件、屬性和驗證。

## 自適應Forms中支援的XFA元素及其映射 {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### 欄位 {#fields}

使用XDP檔案建立自適應表單時，可將XFA欄位拖放到自適應表單上。 下表列出了XFA欄位如何映射到「自適應表單」欄位。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA欄位或容器</strong></p> </td>
   <td><p><strong>相應的自適應表單元件</strong></p> </td>
  </tr>
  <tr>
   <td><p>按鈕 </p> </td>
   <td><p>按鈕</p> </td>
  </tr>
  <tr>
   <td><p>核取方塊 </p> </td>
   <td><p>核取方塊</p> </td>
  </tr>
  <tr>
   <td><p>清單框 </p> </td>
   <td><p>下拉式清單</p> </td>
  </tr>
  <tr>
   <td><p>日期/時間欄位 </p> </td>
   <td><p>日期挑選器</p> </td>
  </tr>
  <tr>
   <td><p>簽名Scribble</p> </td>
   <td><p>草寫簽名</p> </td>
  </tr>
  <tr>
   <td><p>數字欄位 </p> </td>
   <td><p>數值方塊</p> </td>
  </tr>
  <tr>
   <td><p>小數欄位</p> </td>
   <td><p>數值方塊</p> </td>
  </tr>
  <tr>
   <td><p>文字欄位 </p> </td>
   <td><p>文字方塊</p> </td>
  </tr>
  <tr>
   <td><p>密碼欄位 </p> </td>
   <td><p>密碼方塊</p> </td>
  </tr>
  <tr>
   <td><p>影像</p> </td>
   <td><p>影像</p> </td>
  </tr>
  <tr>
   <td><p>文字</p> </td>
   <td><p>文字</p> </td>
  </tr>
  <tr>
   <td><p>子窗體 </p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>區域（組）</p> </td>
   <td><p>面板</p> </td>
  </tr>
  <tr>
   <td><p>子窗體集 </p> </td>
   <td><p>面板</p> </td>
  </tr>
 </tbody>
</table>

### 屬性 {#properties}

下表捕獲了在XDP檔案中定義的各種XFA指令碼在AdaptiveForms中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA元件屬性</strong></p> </td>
   <td><p><strong>自適應Forms中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>som表達式 </p> </td>
   <td><p>映射到Adaptive Form中的Bind引用(bindRef)屬性。</p> </td>
  </tr>
  <tr>
   <td><p>存在 </p> </td>
   <td><p>映射到自適應表單中的可見屬性。 可以使用「可見性」(Visibility)表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>訪問 </p> </td>
   <td><p>映射到Adaptive Form中的enabled屬性。 可以使用Access表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：角色 </p> </td>
   <td><p>映射到自適應表單中的角色屬性。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：講話優先順序 </p> </td>
   <td><p>映射到Adaptive Form中的speakPriority屬性。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：講話文本</p> </td>
   <td><p>映射到自適應表單中的自定義輔助功能文本。</p> </td>
  </tr>
  <tr>
   <td><p>輔助功能：工具提示 </p> </td>
   <td><p>映射到Adaptive Form中的簡短說明屬性。</p> </td>
  </tr>
  <tr>
   <td><p>字幕<em> （所有欄位類型）</em></p> </td>
   <td><p>映射到自適應表單中的Title屬性。</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> （所有欄位類型）</em></p> </td>
   <td><p>映射到「自適應」窗體中的「顯示模式」。</p> </td>
  </tr>
  <tr>
   <td><p>原始值<em> （所有欄位類型）</em></p> </td>
   <td><p>映射到自適應表單中的值屬性。</p> </td>
  </tr>
  <tr>
   <td><p>項目<em> （清單框，複選框）</em></p> </td>
   <td><p>映射到Adaptive Form中的選項屬性。 可以使用「選項」表達式覆蓋它。</p> </td>
  </tr>
  <tr>
   <td><p>最大字元<em> （文本欄位）</em></p> </td>
   <td><p>映射到自適應表單中允許的最大字元數屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多線<em> （文本欄位）</em></p> </td>
   <td><p>映射到「自適應表單」中的「允許多行」屬性。</p> </td>
  </tr>
  <tr>
   <td><p>frac數字<em> （數字欄位、小數欄位）</em></p> </td>
   <td><p>映射到自適應表單中的Frac數字屬性。</p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> （數字欄位、小數欄位）</em></p> </td>
   <td><p>映射到Adaptive Form中的Lead digits屬性。</p> </td>
  </tr>
  <tr>
   <td><p>多選擇<em> （清單框）</em></p> </td>
   <td><p>映射到「自適應表單」中的「允許多個選擇」屬性。</p> </td>
  </tr>
 </tbody>
</table>

### 指令碼 {#scripts}

下表說明了在XDP檔案中定義的各種XFA指令碼在AdaptiveForms中的行為。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA指令碼事件</strong></p> </td>
   <td><p><strong>自適應Forms中的對應行為</strong></p> </td>
  </tr>
  <tr>
   <td><p>初始化 </p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>計算</p> </td>
   <td><p>映射到自適應表單中的計算表達式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證 </p> </td>
   <td><p>映射到自適應表單中的驗證表達式。</p> </td>
  </tr>
  <tr>
   <td><p>驗證狀態 </p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。<br /> </p> </td>
  </tr>
  <tr>
   <td><p>退出 </p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>按一下（按鈕欄位）</p> </td>
   <td><p>映射到按鈕的「按一下」表達式。</p> </td>
  </tr>
  <tr>
   <td><p>支援伺服器端指令碼</p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>支援Web服務</p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。</p> </td>
  </tr>
  <tr>
   <td><p>更改（Scribble欄位、單選按鈕、複選框）</p> </td>
   <td><p>此指令碼在運行時執行，無法在自適應表單中覆蓋。</p> </td>
  </tr>
 </tbody>
</table>

### 驗證 {#validations}

下表捕獲了XFA驗證如何映射到Adaptive Forms中的驗證。

<table>
 <tbody>
  <tr>
   <td><p><strong>XFA驗證</strong></p> </td>
   <td><p><strong>自適應表單中的相應驗證</strong></p> </td>
  </tr>
  <tr>
   <td><p>驗證模式(formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>驗證模式消息(formatTestMessage)</p> </td>
   <td><p>驗證圖片消息</p> </td>
  </tr>
  <tr>
   <td><p>必需（空測試）</p> </td>
   <td><p>強制 </p> </td>
  </tr>
  <tr>
   <td><p>空消息(nullTestMessage) </p> </td>
   <td><p>強制消息</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼(scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>驗證指令碼消息(scriptTestMessage)</p> </td>
   <td><p>驗證消息</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>不能覆蓋綁定到XFA複選框的Adaptive Form單選按鈕和複選框組的強制屬性。

