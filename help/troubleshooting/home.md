---
title: AEM Assets和Forms的疑難排解
description: 使用主要區域的文章連結，例如上傳、中繼資料、搜尋、傳送、表單建立、提交和整合，疑難排解常見的AEM Assets和Forms問題。
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# 疑難排解AEM Assets和Forms問題 {#troubleshoot-aem-assets-forms}

AEM as a Cloud Service透過AEM Assets提供全方位的數位資產管理解決方案，並透過AEM Forms提供強大的表單建立功能。 這兩種服務都提供雲端原生PaaS解決方案，搭配新一代智慧功能，例如AI/ML，全都可在系統內提供最新功能、隨時可用以及持續學習。

然而，複雜的企業環境可能會在不同領域遇到各種技術挑戰。

此全方位的疑難排解指南針對AEM Assets和Forms提供系統化的診斷方法、分類的解決方案，以及逐步解決路徑。 每個區段都包含快速參考指南、詳細的疑難排解方法以及廣泛的資源連結，以幫助您有效解決問題並最佳化AEM Cloud Service環境。

## AEM Assets疑難排解 {#aem-assets-troubleshooting}

AEM Assets可簡化您跨體驗管理、組織和提供數位資產的方式。 但是，可能會出現影響資產上傳、中繼資料、整合或傳送的問題。 本文提供疑難排解步驟，協助您診斷並解決常見的AEM Assets問題。 依照此處的指引，您可以有效率地還原工作流程，並確保資產保持可存取、正確且準備好供跨管道使用。

### 資產處理與轉譯 {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>上傳與處理</strong></td>
    <td><strong>轉譯</strong></td>
    <td><strong>PDF與文字擷取</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Service中大型MP4檔案的資產處理失敗</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM轉譯不符合原始檔案</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM會截斷10萬個權杖後從大型PDF擷取的文字</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-23916">具有ZIP壓縮上傳的TIFF檔案不會產生轉譯</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26233">影像未在AEM as a Cloud Service中顯示縮圖轉譯</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25518">AEM as a Cloud Service中大型PDF的文字擷取限制</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-21865">將資產資料夾拖放至AEM Assets Web UI失敗</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26528">資產輪換問題導致後續輪換無法顯示</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26450">提升Photoshop Firefly API整合的單一部分資產上傳限制</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamic Media {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>影片</strong></td>
    <td><strong>迴轉集與智慧型裁切</strong></td>
    <td><strong>傳遞與設定</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26533">修正AEM中的視訊上傳、處理和轉譯問題</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26715">迴轉集卡在處理狀態</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-17628">變更資產的Dynamic Media URL</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26677">Dynamic Media與DAM卡片檢視的視訊縮圖不相配</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26873">AEM as a Cloud Service中未產生智慧型裁切轉譯</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26367">AEM 6.5中的智慧型裁切已中斷影像問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM Dynamic Media資產處理失敗</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26637">TIFF轉譯的背景色彩問題</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25294">Dynamic Media一般設定頁面未開啟</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26197">使用Dynamic Media解決視訊檔案中的音訊問題</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25885">Dynamic Media中的資產同步失敗</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26461">解決各個環境中的資產名稱差異</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26871">Dynamic Media視訊播放器在較低環境中無法運作</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25471">Dynamic Media同步使用者建議</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26902">使用API從Dynamic Media匯出資產和中繼資料</a></td>
  </tr>
  </tbody>
</table>

### 中繼資料、標籤和共用 {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>中繼資料</strong></td>
    <td><strong>智慧標記</strong></td>
    <td><strong>存取與共用</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25828">AEM Assets中的影像中繼資料差異</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25925">自動標籤新上傳的資產</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26928">儘管擁有讀取存取權，Assets檢視中的評論仍受限</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26655">解決非管理員使用者的中繼資料結構可見性問題</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25889">JWT移轉至OAuth後智慧型標籤無法運作</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25903">解決AEM Managed Services中的共用連結問題</a></td>
  </tr>

</tbody>
</table>

### 整合與存取 {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Asset Link</strong></td>
      <td><strong>授權和自訂</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe資產連結導致InDesign中的連結無法存取</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26616">內容片段未包含在AEM Assets授權中</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25562">解決InDesign中的AEM Asset Link連線問題</a></td>
      <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25525">解決AEM as a Cloud Service中的資產處理問題</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25506">Adobe Asset Link外掛程式網路錯誤：無法連線伺服器</a></td>
      <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-25829">正在更新AEM as a Cloud Service中視訊資產的自訂縮圖</a>
      </td>
    </tr>
  </tbody>
</table>




## AEM Forms疑難排解 {#aem-forms-troubleshooting}

AEM Forms as a Cloud Service提供強大的表單建立和管理功能。 不過，在安裝、設定、建立表單或提交程式期間，您可能會遇到問題。 本節提供常見AEM Forms問題的完整疑難排解指引。

### 安裝和設定問題

<table>
  <tbody>
  <tr>
    <td><strong>設定與組態</strong></td>
    <td><strong>表單建立問題</strong></td>
    <td><strong>效能與快取</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">導覽中無法使用Forms選項</a></td>
    <td><a href="/help/forms/form-creation-failing.md">範本發佈後表單建立失敗</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">最適化Forms快取問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">建置管道失敗</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">範本發佈順序問題</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Dispatcher快取失效問題</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">套件組合啟用問題</a></td>
    <td><a href="/help/forms/known-issues.md">已知表單建立限制</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">CDN快取失敗</a></td>
  </tr>
  </tbody>
</table>

### 表單提交和整合問題

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>自訂提交動作</strong></td>
    <td><strong>整合問題</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403表單提交中禁止的錯誤</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">自訂提交動作中的502錯誤</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-27434">DRM-SAML重新導向失敗</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">CORS設定問題</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">未處理的例外狀況處理</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-27075">在AEM Sites上停用提交按鈕</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">反向連結篩選設定</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">自訂動作的最佳實務</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26532">升級後隱藏欄位的可見度</a></td>
  </tr>
  </tbody>
</table>

### Designer和開發問題

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>開發環境</strong></td>
    <td><strong>版本和相容性</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26558">Designer 6.5升級後未開啟</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-27089">定位器無法以JDK 8/11開頭</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26862">AEM Forms (AEMFD)封裝版本顯示問題</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-21018">PDF Generator JPEG 2000錯誤</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-22689">JBoss記錄路徑設定</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-26846">Windows中的版本號碼不正確</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-27406">PDF輸出中缺少按鈕</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-18084">Configuration Manager升級錯誤</a></td>
    <td><a href="https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-kcs/kbarticles/ka-17339">索引損毀因應措施</a></td>
  </tr>
  </tbody>
</table>



