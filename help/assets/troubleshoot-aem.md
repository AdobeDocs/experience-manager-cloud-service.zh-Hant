---
title: AEM Assets的疑難排解
description: 使用主要AEM Assetss=區域的文章連結，例如上傳、中繼資料、搜尋、傳送等，疑難排解常見AEM Assets問題。
hidefromtoc: true
hide: true
source-git-commit: 60667c265cf480521fe0c0d646c2665540f110d0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# AEM Assets的疑難排解 {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service為企業提供雲端原生PaaS解決方案，不僅可用於執行數位資產管理和Dynamic Media作業，亦可使用新一代智慧功能，例如AI/ML。 所有功能都來自一律最新、永遠可用且永遠學習的系統。

不過，可能會發生影響資產上傳、中繼資料、搜尋或傳送及其他AEM Assets重要區域的問題。 本文提供疑難排解步驟，協助您診斷並解決這些常見的AEM Assets問題。

<table>
  <tbody>
  <tr>
    <td>在AEM的資產下載ZIP檔案中遺失<a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-27140">轉譯</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26616">內容片段未包含在AEM Assets授權中</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26928">儘管擁有讀取存取權，但在Assets檢視中受到限制發表評論</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26715">(Dynamic Media)迴轉集在AEM Dynamic Media</a>中卡在處理狀態 </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26639">數位資產管理(DAM)轉譯不符合AEM中的原始檔案</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26873">AEMaaCS中未產生智慧型裁切轉譯</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamic Media)修正AEM中的視訊上傳、處理和轉譯問題</a> </td>
    <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26922">(Asset Link) Adobe Asset Link讓連結在使用InDesign時處於無法存取狀態</a> </td>
    <td>AEMaaCS中Dynamic Media與DAM卡片檢視之間的<a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26677">視訊縮圖不相符</a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26610">AEM as a Cloud Service中大型MP4檔案的資產處理失敗</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) Dynamic Media視訊播放器在較低環境中無法運作</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26103">（具有OpenAPI的Dynamic Media）使用以IMS使用者群組為基礎的Open API啟用受限的Assets對Dynamic Media的存取</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-23916">當具有ZIP壓縮格式的Tiff檔案上傳到AEM Assets時，不會產生轉譯</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM會截斷10萬個權杖後從大型PDF擷取的文字</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media)變更DM Assets的Dynamic Media URL</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26655">解決AEMaaCS中非管理員使用者的中繼資料結構可見性問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Dynamic Media中TIFF影像轉譯的背景色彩變更問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26528">AEMaaCS資產輪換問題導致後續輪換無法顯示</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media)解決Adobe Experience Manager 6.5 Dynamic Media中智慧型裁切的損壞影像問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26450">提升Photoshop Firefly API整合的單一部分資產上傳限制</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media)針對PDF檔案解決AEM環境中的Dynamic Media資產名稱差異</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26233">Adobe Experience Manager (AEM) as a Cloud Service — 資產中的某些影像未顯示縮圖轉譯</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media) Dynamic Media一般設定頁面未開啟</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media)使用AEM中的Dynamic Media解決視訊檔案中的音訊問題</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25925">在AEM as a Cloud Service中自動標籤新上傳的資產</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25889">在AEM中將JWT移轉至OAuth後，智慧標籤功能無法運作</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25903">解決AEM Managed Services中的共用連結問題</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) AEM Dynamic Media資產處理失敗</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Adobe Experience Manager (AEM) Dynamic Media的資產同步失敗</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25829">更新AEM as a Cloud Service中視訊資產的自訂縮圖</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25828">Adobe Experience Manager (AEM) Assets中的影像中繼資料差異</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-21865">將資產資料夾拖放至AEM Assets Web UI失敗</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media)解決AEM as a Cloud Service中的資產處理問題</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25518">Adobe Experience Manager as a Cloud Service中大型PDF的文字擷取限制</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25562">(Asset Link)解決InDesign中的Adobe Experience Manager (AEM)資產連結連線問題</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25506">(Asset Link) Adobe Asset Link外掛程式網路錯誤：無法連線伺服器</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-25471">(Dynamic Media) Dynamic Media同步使用者建議</a></td>
  <td><a href="https://experienceleague.adobe.com/en/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media)使用API從Dynamic Media匯出資產和中繼資料</a></td>
  <td></td>
</tr>

</tbody>
  <table>


