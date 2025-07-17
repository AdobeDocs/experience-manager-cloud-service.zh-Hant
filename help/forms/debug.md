---
title: 偵錯HTML5 forms
description: 本檔案列出疑難排解各種已知問題的步驟。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
feature: HTML5 Forms,Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# 偵錯HTML5 forms {#debugging-html-forms}

本檔案包含數個疑難排解案例。 對於每種情況，都提供了疑難排解問題的一些步驟。 請按照以下步驟操作，如果問題仍然存在，請設定記錄器以取得並檢閱記錄檔中的錯誤/警告。 如需HTML5表單記錄的詳細資訊，請參閱[產生HTML5表單的記錄](/help/forms/enable-logs.md)。

## 問題：轉譯表單時，我看到org.apache.sling.api.SlingException例外狀況頁面 {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

在例外狀況詳細資訊中，搜尋由&#x200B;**引起的單字**。

可能的原因是URL中的一個或多個引數不正確。

檢查下列引數：

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br />注意：路徑定義了資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

## 問題：無法轉譯表單（顯示錯誤訊息） {#problem-unable-to-render-form}

1. 請確定指定的引數正確無誤。 如需引數的詳細資訊，請參閱[轉譯引數](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page)。
1. 登入CRX Package Manager(位於https://&lt;server>：&lt;port>/crx/packmgr/index.jsp)，然後檢查是否已正確安裝下列套件：

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. 在https://&lt;server>：&lt;port>/system/console/bundles登入CQ網頁主控台（Felix主控台）。

   確認下列套件組合的狀態為「作用中」：

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * Adobe XFA Forms轉譯器

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：表單轉譯器沒有樣式 {#problem-form-renders-without-styles}

1. 在瀏覽器中，開啟&#x200B;**開發人員工具**。 確保profile.css可供使用。
1. 如果profile.css檔案無法使用，請登入CRX DE https://&lt;server>：&lt;port>/crx/de。
1. 在左側的資料夾階層中，導覽至/etc/clientlibs/fd/xfaforms/。 開啟資料夾中列出的css.txt檔案。

   * 側面像
   * 執行階段
   * scrollnav
   * 工具列
   * xfalib

1. 確認css.txt內提及的檔案存在於CRX DE Lite的/libs/fd/xfaforms/clientlibs/xfalib/css中。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 如果上述檔案無法使用，請再次安裝adobe-lc-forms-runtime-pkg-&lt;version>.zip套件。

### 問題：發生非預期的錯誤 {#problem-unexpected-error-encountered}

1. 在表單URL中，新增查詢引數debugClientLibs並將其值設為true (例如： https://&lt;server>：&lt;port>/content/xfaforms/profiles/test.html？contentRoot=&lt;some path>&amp;template=&lt;name of xdp file>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. 在案頭瀏覽器（如Chrome）中，前往「開發人員工具」 > 「主控台」 。
1. 開啟記錄檔以識別錯誤型別。 如需有關記錄的詳細資訊，請參閱HTML5表單的[記錄](/help/forms/enable-logs.md)。
1. 前往「開發人員工具>主控台」。 使用棧疊追蹤來找出導致錯誤的程式碼。 對錯誤進行偵錯以解決問題。

   >[!NOTE]
   >
   >如果指令碼失敗，請檢查在表單PDF轉譯期間是否也發生相同問題。 如果是，則表示表單指令碼邏輯有問題。

## 問題：無法提交表單 {#problem-unable-to-submit-the-form}

1. 確保您有權存取AEM伺服器，且已連線至伺服器。
1. 檢查引數submitUrl是否正確。
1. 使用偵錯選項作為[1-a5-b5-c5](/help/forms/enable-logs.md)，啟用HTML5表單&#x200B;**的**&#x200B;記錄檔中提及的使用者端記錄檔。 然後轉譯表單並按一下提交。 開啟瀏覽器偵錯主控台並檢查是否有錯誤。
1. 找到在[HTML5表單](/help/forms/enable-logs.md)的記錄檔中提到的伺服器記錄檔。 檢查在提交期間伺服器記錄中是否有任何錯誤。

## 問題：未顯示本地化的錯誤訊息 {#problem-localized-error-messages-do-not-display}

1. 在案頭瀏覽器中使用其他查詢引數&#x200B;**debugClientLibs=true**&#x200B;來轉譯表單，然後前往「開發人員工具>資源」並檢查檔案I18N.css。
1. 如果檔案無法使用，請在https://&lt;server>：&lt;port>/crx/de登入CRX DE。
1. 在左側的資料夾階層中，導覽至/libs/fd/xfaforms/clientlibs/I18N，並確認下列檔案和資料夾存在：

   * Namespace.js
   * LogMessages.js
   * 語言資料夾

1. 如果以上任何檔案或資料夾不存在，請再次安裝&#x200B;**adobe-lc-forms-runtime-pkg-&lt;version>.zip**&#x200B;套件。
1. 瀏覽到與地區設定名稱相同的資料夾，並檢查其內容。 資料夾必須包含下列檔案：

   * I18N.js
   * js.txt

1. 檢查js.txt的內容，確認其中包含下列專案。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：影像未顯示 {#problem-image-not-showing-up}

1. 請確定影像URL正確無誤。
1. 檢查您的瀏覽器是否支援此型別的影像。
1. 在例外狀況詳細資訊中，搜尋由&#x200B;**引起的單字**。

   可能的原因是URL中的一個或多個引數不正確。

   檢查下列引數：
步驟文字

<table>
 <tbody>
  <tr>
   <td><strong>參數</strong></td>
   <td><strong>說明</strong></td>
  </tr>
  <tr>
   <td>範本</td>
   <td>範本的檔案名稱</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>範本和相關資源所在的路徑</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>與範本合併之資料檔案的絕對路徑。<br />注意：路徑定義了資料檔案的絕對路徑。</td>
  </tr>
  <tr>
   <td>資料</td>
   <td>與範本合併的UTF-8編碼資料位元組。</td>
  </tr>
 </tbody>
</table>

1. 在案頭瀏覽器中，前往「開發人員工具」 > 「資源」 。

   在「影格」的左側勾選該影像。
