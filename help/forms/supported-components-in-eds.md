---
title: AEM Forms Edge Delivery Services表單元件
description: AEM Forms Edge遞送服務專為最佳效能而打造，可讓您構想簡化資料收集和使用者參與的未來。 本文列出所有可用於EDD表單的現成可用表單元件。
feature: Edge Delivery Services
hide: true
hidefromtoc: true
source-git-commit: 53a66eac5ca49183221a1d61b825401d4645859e
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 4%

---




# Form Block Edge Delivery支援的HTML元件

AEM Forms Edge Delivery包含Form區塊。 Form Block可協助您輕鬆建立表單，以擷取及儲存擷取的資料。

表單區塊支援OOTBHTML5元件，例如文字、電子郵件、數字、日期等。 它也支援文字區域、select和fieldset元素，並包含HTML-5原生輸入驗證功能。 「表單區塊」會為所有欄位型別和容器建立統一的HTML結構，以確保一致性。 您也 [設定欄位型別的樣式](https://adobe-rnd.github.io/form-block/customization/styling_form) 使用 `form.css` 檔案。

## 表單區塊中支援的HTML5輸入型別

Form Block支援各種HTML5輸入型別，也能順暢呈現以AEM核心元件建立的表單。

下表概述核心元件對應至邊緣傳送中HTML5輸入型別的方式：

<table>
 <tbody>
  <tr>
   <td><b>核心元件</b> </td>
   <td><b>HTML5輸入型別</b> </td>
   <td><b>詳細資料</b></td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/form-container.html">表單容器</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#form">表單 </td>
   <td> 建立表單以擷取使用者輸入。
   </td>
  </tr>
  <tr>
   <td><a herf="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text-input.html">文字輸入</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/text">text</a></td>
   <td> 定義單行文字輸入欄位。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/number-input.html">數字輸入</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/number">數字</a></td>
   <td>可讓使用者輸入數字。 您也可以新增內建驗證，以拒絕非數值輸入。 可讓使用者輸入數字。 您也可以新增內建驗證，以拒絕非數值輸入。 最初，輸入欄位顯示為數字輸入。 如果使用者套用顯示模式，它會變更為文字，以允許作者套用數字格式，因為HTML5缺少對顯示模式的支援。 但是，當使用者按一下它，它返回到輸入數字。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/date-picker.html">日期挑選器</a></td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/date">日期 </a></td>
   <td> 建立輸入欄位以輸入日期。 您可以選擇透過文字方塊（驗證輸入項）或專用日期選擇器介面來輸入日期。 最初，會顯示原生日期輸入欄位。 如果使用者套用顯示模式，它會變更為文字，以允許使用者套用格式，因為HTML5缺少對顯示模式的支援。 但是，當使用者按一下它，它就會返回輸入日期。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/file-attachment.html">檔案附件</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/file">檔案</a></td>
   <td> 允許使用者從裝置儲存中選擇一或多個檔案。 它支援增強的檔案輸入驗證，例如接受的檔案型別、檔案大小限制和最小/最大檔案選取限制。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/drop-down.html"> 下拉式清單</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select">選取</a></td>
   <td> 允許使用者從預先定義的選項清單中選取一或多個選項。 選項可以是字串、數字或布林值型別。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox-group.html">核取方塊群組</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/checkbox">多個核取方塊</a></td>
   <td> 允許使用者從清單中選取一或多個選項。 系統會產生多個名稱相同的核取方塊，每個核取方塊都對應到列舉中的專案。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/radio-button.html">選項按鈕群組</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/radio">多重無線電</a></td>
   <td> 允許使用者從一組相關選項中選取一個選項。 產生多個名稱相同的選項按鈕，每個按鈕都對應到列舉中的專案。</td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/button.html">按鈕</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/button">按鈕</a></td>
   <td>使用者按一下即可觸發動作的UI元素。 </td>
  </tr>
  <tr>
   <td><a href="" https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html">面板</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">使用圖例的欄位集</a></td>
   <td> 將表單中的區段分組，其中巢狀*legend*元素會為表單新增標題。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html">精靈</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset">欄位集</a></td>
   <td>將表單中相關區段分組。 它也會控制排列方式，支援顯示選項，以將排列方式放置在頂端或左側。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/text.html">文字</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/p">p</a></td>
   <td>p標籤標籤段落。 在視覺內容中，段落是以空白行或第一行縮排分隔的文字區塊</td>
  </tr>
     <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">提交按鈕</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/submit">提交</a></td>
   <td> 使用者介面元素，可讓使用者在按一下時將表單提交至伺服器。 如果使用者將提交規則新增到按鈕，其作用就像提交按鈕。 </td>
  </tr>
     <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/reset-button.html">重設按鈕</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/reset">重設</a></td>
   <td>按一下時會重設表單的UI元素。 如果使用者將重設規則新增到按鈕，則其作用就像重設按鈕。 </td>
  </tr>
    <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/email-input.html">電子郵件輸入</td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/email">電子郵件</a></td>
   <td> 允許使用者輸入及編輯電子郵件地址。 如果使用者新增多個屬性，則可新增或編輯電子郵件地址清單。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/telephone-input.html">電話輸入</a></td>
   <td><a href ="https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/tel">電話</a></td>
   <td>允許使用者輸入和編輯電話號碼。</td>
  </tr>
   <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/header.html">頁首</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/header"> 頁首</a></td>
   <td>其中包含入門內容，通常是一組入門或導覽輔助。 在表單容器外部受支援。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/footer.html">頁尾</td>
   <td><a href = "https://developer.mozilla.org/en-US/docs/Web/HTML/Element/footer">頁尾</a></td>
   <td> 包含版權資料或相關檔案連結等資訊。 在表單容器外部受支援。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html">折疊面板<a></td>
   <td><i>表單區塊尚未支援</i></td>
   <td> 允許使用者在表單中建立可展開和可收合的區段。 </td>
  </tr>
  <tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html">水準索引標籤</a></td>
   <td><i>表單區塊尚未支援</i></td>
   <td>將表單的多個區段組織成水準顯示的個別標籤。</td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/image.html">影像</a></td>
   <td><i>表單區塊尚未支援</i></td>
   <td> 允許使用者在表單中包含影像。</td>
  </tr><tr>
   <td><a href ="https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/title.html">標題</a></td>
   <td><i>表單區塊尚未支援</i></td>
   <td> 參考表單頂端顯示的文字。 </td>
  </tr>
  <tr>
   <td><a href = "https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/submit-button.html">切換</td>
   <td><i>表單區塊尚未支援</i></td>
   <td> 雙狀態切換可讓使用者在兩個狀態之間進行選取，例如啟用或停用功能、設定或功能。</td>
  </tr>
 </tbody>
</table>


