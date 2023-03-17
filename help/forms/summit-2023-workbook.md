---
title: 使用核心元件和無頭式架構，打造吸引人的Forms
seo-title: Build Engaging Forms Using Core Components and Headless
description: 使用核心元件和無頭式架構，打造吸引人的Forms
seo-description: Build Engaging Forms Using Core Components and Headless
topic-tags: develop
hide: true
hidefromtoc: true
source-git-commit: f65c5241e1e61e5a0bd9981778939caa313de76a
workflow-type: tm+mt
source-wordcount: '3412'
ht-degree: 3%

---


# 使用核心元件和無頭式架構，打造吸引人的Forms

## 實驗概述

在這個實踐實驗中，您會學到：

如何使用AEM Forms，使用與AEM Sites一致的最新核心元件輕鬆建立最適化表單，將最適化表單以無頭表單形式提供至網路、行動裝置和聊天，進而實現全通路資料擷取體驗。 您也可以了解關於樣式、自訂和前端開發的最佳實務。

## 主要要點

* **業務靈活性**:身為企業使用者，我可以輕鬆為多個管道製作表單體驗。

* **前端開發人員的功能**:作為前端開發人員，我可以使用無頭表單來控制一般使用者體驗。

* **開發人員速度**:身為開發人員，我可以輕鬆且一致地自訂Sites和Forms元件。

## 必備條件


+++AEM Forms作為Cloud Service沙箱



<table>
        <thead>
            <tr><th>實驗ID</th><th>製作執行個體URL</th><th>發佈執行個體URL</th></tr>           
        </thead>
        <tbody>
            <tr><td>L716001</td><td>https://author-p105303-e986623.adobeaemcloud.com</td><td>https://publish-p105303-e986623.adobeaemcloud.com</td></tr><tr><td>L716002</td><td>https://author-p106405-e993047.adobeaemcloud.com</td><td>https://publish-p106405-e993047.adobeaemcloud.com</td></tr><tr><td>L716003</td><td>https://author-p106406-e993049.adobeaemcloud.com</td><td>https://publish-p106406-e993049.adobeaemcloud.com</td></tr><tr><td>L716004</td><td>https://author-p106398-e993114.adobeaemcloud.com</td><td>https://publish-p106398-e993114.adobeaemcloud.com</td></tr><tr><td>L716005</td><td>https://author-p106407-e993048.adobeaemcloud.com</td><td>https://publish-p106407-e993048.adobeaemcloud.com</td></tr><tr><td>L716006</td><td>https://author-p106408-e993155.adobeaemcloud.com</td><td>https://publish-p106408-e993155.adobeaemcloud.com</td></tr><tr><td>L716007</td><td>https://author-p106343-e993067.adobeaemcloud.com</td><td>https://publish-p106343-e993067.adobeaemcloud.com</td></tr><tr><td>L716008</td><td>https://author-p106399-e993108.adobeaemcloud.com</td><td>https://publish-p106399-e993108.adobeaemcloud.com</td></tr><tr><td>L716009</td><td>https://author-p106344-e993064.adobeaemcloud.com</td><td>https://publish-p106344-e993064.adobeaemcloud.com</td></tr><tr><td>L716010</td><td>https://author-p106409-e993051.adobeaemcloud.com</td><td>https://publish-p106409-e993051.adobeaemcloud.com</td></tr><tr><td>L716011</td><td>https://author-p106345-e993060.adobeaemcloud.com</td><td>https://publish-p106345-e993060.adobeaemcloud.com</td></tr><tr><td>L716012</td><td>https://author-p106346-e993061.adobeaemcloud.com</td><td>https://publish-p106346-e993061.adobeaemcloud.com</td></tr><tr><td>L716013</td><td>https://author-p106410-e993153.adobeaemcloud.com</td><td>https://publish-p106410-e993153.adobeaemcloud.com</td></tr><tr><td>L716014</td><td>https://author-p106502-e993073.adobeaemcloud.com</td><td>https://publish-p106502-e993073.adobeaemcloud.com</td></tr><tr><td>L716015</td><td>https://author-p106401-e993112.adobeaemcloud.com</td><td>https://publish-p106401-e993112.adobeaemcloud.com</td></tr><tr><td>L716016</td><td>https://author-p106452-e993115.adobeaemcloud.com</td><td>https://publish-p106452-e993115.adobeaemcloud.com</td></tr><tr><td>L716017</td><td>https://author-p106453-e993113.adobeaemcloud.com</td><td>https://publish-p106453-e993113.adobeaemcloud.com</td></tr><tr><td>L716018</td><td>https://author-p106411-e993050.adobeaemcloud.com</td><td>https://publish-p106411-e993050.adobeaemcloud.com</td></tr><tr><td>L716019</td><td>https://author-p106454-e993116.adobeaemcloud.com</td><td>https://publish-p106454-e993116.adobeaemcloud.com</td></tr><tr><td>L716020</td><td>https://author-p106347-e993063.adobeaemcloud.com</td><td>https://publish-p106347-e993063.adobeaemcloud.com</td></tr><tr><td>L716021</td><td>https://author-p106455-e993109.adobeaemcloud.com</td><td>https://publish-p106455-e993109.adobeaemcloud.com</td></tr><tr><td>L716022</td><td>https://author-p106456-e993110.adobeaemcloud.com</td><td>https://publish-p106456-e993110.adobeaemcloud.com</td></tr><tr><td>L716023</td><td>https://author-p106466-e993291.adobeaemcloud.com</td><td>https://publish-p106466-e993291.adobeaemcloud.com</td></tr><tr><td>L716024</td><td>https://author-p106413-e993156.adobeaemcloud.com</td><td>https://publish-p106413-e993156.adobeaemcloud.com</td></tr><tr><td>L716025</td><td>https://author-p106348-e993066.adobeaemcloud.com</td><td>https://publish-p106348-e993066.adobeaemcloud.com</td></tr><tr><td>L716026</td><td>https://author-p106414-e993154.adobeaemcloud.com</td><td>https://publish-p106414-e993154.adobeaemcloud.com</td></tr><tr><td>L716027</td><td>https://author-p106349-e993065.adobeaemcloud.com</td><td>https://publish-p106349-e993065.adobeaemcloud.com</td></tr><tr><td>L716028</td><td>https://author-p106415-e993152.adobeaemcloud.com</td><td>https://publish-p106415-e993152.adobeaemcloud.com</td></tr><tr><td>L716029</td><td>https://author-p106350-e993068.adobeaemcloud.com</td><td>https://publish-p106350-e993068.adobeaemcloud.com</td></tr><tr><td>L716030</td><td>https://author-p106351-e993062.adobeaemcloud.com</td><td>https://publish-p106351-e993062.adobeaemcloud.com</td></tr><tr><td>L716031</td><td>https://author-p106417-e993158.adobeaemcloud.com</td><td>https://publish-p106417-e993158.adobeaemcloud.com</td></tr><tr><td>L716032</td><td>https://author-p106418-e993159.adobeaemcloud.com</td><td>https://publish-p106418-e993159.adobeaemcloud.com</td></tr><tr><td>L716033</td><td>https://author-p106503-e993080.adobeaemcloud.com</td><td>https://publish-p106503-e993080.adobeaemcloud.com</td></tr><tr><td>L716034</td><td>https://author-p106457-e993125.adobeaemcloud.com</td><td>https://publish-p106457-e993125.adobeaemcloud.com</td></tr><tr><td>L716035</td><td>https://author-p106504-e993081.adobeaemcloud.com</td><td>https://publish-p106504-e993081.adobeaemcloud.com</td></tr><tr><td>L716036</td><td>https://author-p106458-e993120.adobeaemcloud.com</td><td>https://publish-p106458-e993120.adobeaemcloud.com</td></tr><tr><td>L716037</td><td>https://author-p106419-e993160.adobeaemcloud.com</td><td>https://publish-p106419-e993160.adobeaemcloud.com</td></tr><tr><td>L716038</td><td>https://author-p106420-e993162.adobeaemcloud.com</td><td>https://publish-p106420-e993162.adobeaemcloud.com</td></tr><tr><td>L716039</td><td>https://author-p106517-e993235.adobeaemcloud.com</td><td>https://publish-p106517-e993235.adobeaemcloud.com</td></tr><tr><td>L716040</td><td>https://author-p106506-e993079.adobeaemcloud.com</td><td>https://publish-p106506-e993079.adobeaemcloud.com</td></tr><tr><td>L716041</td><td>https://author-p106507-e993074.adobeaemcloud.com</td><td>https://publish-p106507-e993074.adobeaemcloud.com</td></tr><tr><td>L716042</td><td>https://author-p106508-e993075.adobeaemcloud.com</td><td>https://publish-p106508-e993075.adobeaemcloud.com</td></tr><tr><td>L716043</td><td>https://author-p106421-e993163.adobeaemcloud.com</td><td>https://publish-p106421-e993163.adobeaemcloud.com</td></tr><tr><td>L716044</td><td>https://author-p106459-e993121.adobeaemcloud.com</td><td>https://publish-p106459-e993121.adobeaemcloud.com</td></tr><tr><td>L716045</td><td>https://author-p106467-e993292.adobeaemcloud.com</td><td>https://publish-p106467-e993292.adobeaemcloud.com</td></tr><tr><td>L716046</td><td>https://author-p106518-e993234.adobeaemcloud.com</td><td>https://publish-p106518-e993234.adobeaemcloud.com</td></tr><tr><td>L716047</td><td>https://author-p106511-e993076.adobeaemcloud.com</td><td>https://publish-p106511-e993076.adobeaemcloud.com</td></tr><tr><td>L716048</td><td>https://author-p106512-e993077.adobeaemcloud.com</td><td>https://publish-p106512-e993077.adobeaemcloud.com</td></tr><tr><td>L716049</td><td>https://author-p106460-e993124.adobeaemcloud.com</td><td>https://publish-p106460-e993124.adobeaemcloud.com</td></tr><tr><td>L716050</td><td>https://author-p106519-e993237.adobeaemcloud.com</td><td>https://publish-p106519-e993237.adobeaemcloud.com</td></tr><tr><td>L716051</td><td>https://author-p106513-e993084.adobeaemcloud.com</td><td>https://publish-p106513-e993084.adobeaemcloud.com</td></tr><tr><td>L716052</td><td>https://author-p106461-e993122.adobeaemcloud.com</td><td>https://publish-p106461-e993122.adobeaemcloud.com</td></tr><tr><td>L716053</td><td>https://author-p106514-e993082.adobeaemcloud.com</td><td>https://publish-p106514-e993082.adobeaemcloud.com</td></tr><tr><td>L716054</td><td>https://author-p106462-e993123.adobeaemcloud.com</td><td>https://publish-p106462-e993123.adobeaemcloud.com</td></tr><tr><td>L716055</td><td>https://author-p106463-e993127.adobeaemcloud.com</td><td>https://publish-p106463-e993127.adobeaemcloud.com</td></tr><tr><td>L716056</td><td>https://author-p106515-e993083.adobeaemcloud.com</td><td>https://publish-p106515-e993083.adobeaemcloud.com</td></tr><tr><td>L716057</td><td>https://author-p106464-e993126.adobeaemcloud.com</td><td>https://publish-p106464-e993126.adobeaemcloud.com</td></tr><tr><td>L716058</td><td>https://author-p106520-e993236.adobeaemcloud.com</td><td>https://publish-p106520-e993236.adobeaemcloud.com</td></tr><tr><td>L716059</td><td>https://author-p106423-e993161.adobeaemcloud.com</td><td>https://publish-p106423-e993161.adobeaemcloud.com</td></tr><tr><td>L716060</td><td>https://author-p106516-e993078.adobeaemcloud.com</td><td>https://publish-p106516-e993078.adobeaemcloud.com</td></tr><tr><td>L716061</td><td>https://author-p106521-e993240.adobeaemcloud.com</td><td>https://publish-p106521-e993240.adobeaemcloud.com</td></tr><tr><td>L716062</td><td>https://author-p106424-e993308.adobeaemcloud.com</td><td>https://publish-p106424-e993308.adobeaemcloud.com</td></tr><tr><td>L716063</td><td>https://author-p106468-e993295.adobeaemcloud.com</td><td>https://publish-p106468-e993295.adobeaemcloud.com</td></tr><tr><td>L716064</td><td>https://author-p106425-e993309.adobeaemcloud.com</td><td>https://publish-p106425-e993309.adobeaemcloud.com</td></tr><tr><td>L716065</td><td>https://author-p106426-e993314.adobeaemcloud.com</td><td>https://publish-p106426-e993314.adobeaemcloud.com</td></tr><tr><td>L716066</td><td>https://author-p106469-e993293.adobeaemcloud.com</td><td>https://publish-p106469-e993293.adobeaemcloud.com</td></tr><tr><td>L716067</td><td>https://author-p106522-e993238.adobeaemcloud.com</td><td>https://publish-p106522-e993238.adobeaemcloud.com</td></tr><tr><td>L716068</td><td>https://author-p106470-e993299.adobeaemcloud.com</td><td>https://publish-p106470-e993299.adobeaemcloud.com</td></tr><tr><td>L716069</td><td>https://author-p106427-e993311.adobeaemcloud.com</td><td>https://publish-p106427-e993311.adobeaemcloud.com</td></tr><tr><td>L716070</td><td>https://author-p106428-e993310.adobeaemcloud.com</td><td>https://publish-p106428-e993310.adobeaemcloud.com</td></tr><tr><td>L716071</td><td>https://author-p106471-e993298.adobeaemcloud.com</td><td>https://publish-p106471-e993298.adobeaemcloud.com</td></tr><tr><td>L716072</td><td>https://author-p106429-e993315.adobeaemcloud.com</td><td>https://publish-p106429-e993315.adobeaemcloud.com</td></tr><tr><td>L716073</td><td>https://author-p106523-e993239.adobeaemcloud.com</td><td>https://publish-p106523-e993239.adobeaemcloud.com</td></tr><tr><td>L716074</td><td>https://author-p106472-e993300.adobeaemcloud.com</td><td>https://publish-p106472-e993300.adobeaemcloud.com</td></tr><tr><td>L716075</td><td>https://author-p106430-e993312.adobeaemcloud.com</td><td>https://publish-p106430-e993312.adobeaemcloud.com</td></tr><tr><td>L716076</td><td>https://author-p106524-e993241.adobeaemcloud.com</td><td>https://publish-p106524-e993241.adobeaemcloud.com</td></tr><tr><td>L716077</td><td>https://author-p106431-e993313.adobeaemcloud.com</td><td>https://publish-p106431-e993313.adobeaemcloud.com</td></tr><tr><td>L716078</td><td>https://author-p106473-e993294.adobeaemcloud.com</td><td>https://publish-p106473-e993294.adobeaemcloud.com</td></tr><tr><td>L716079</td><td>https://author-p106474-e993297.adobeaemcloud.com</td><td>https://publish-p106474-e993297.adobeaemcloud.com</td></tr><tr><td>L716080</td><td>https://author-p106475-e993296.adobeaemcloud.com</td><td>https://publish-p106475-e993296.adobeaemcloud.com</td></tr><tr><td>L716081</td><td>https://author-p106476-e993353.adobeaemcloud.com</td><td>https://publish-p106476-e993353.adobeaemcloud.com</td></tr><tr><td>L716082</td><td>https://author-p106525-e993247.adobeaemcloud.com</td><td>https://publish-p106525-e993247.adobeaemcloud.com</td></tr><tr><td>L716083</td><td>https://author-p106526-e993244.adobeaemcloud.com</td><td>https://publish-p106526-e993244.adobeaemcloud.com</td></tr><tr><td>L716084</td><td>https://author-p106527-e993243.adobeaemcloud.com</td><td>https://publish-p106527-e993243.adobeaemcloud.com</td></tr><tr><td>L716085</td><td>https://author-p106477-e993356.adobeaemcloud.com</td><td>https://publish-p106477-e993356.adobeaemcloud.com</td></tr><tr><td>L716086</td><td>https://author-p106478-e993355.adobeaemcloud.com</td><td>https://publish-p106478-e993355.adobeaemcloud.com</td></tr><tr><td>L716087</td><td>https://author-p106528-e993245.adobeaemcloud.com</td><td>https://publish-p106528-e993245.adobeaemcloud.com</td></tr><tr><td>L716088</td><td>https://author-p106432-e993316.adobeaemcloud.com</td><td>https://publish-p106432-e993316.adobeaemcloud.com</td></tr><tr><td>L716089</td><td>https://author-p106529-e993242.adobeaemcloud.com</td><td>https://publish-p106529-e993242.adobeaemcloud.com</td></tr><tr><td>L716090</td><td>https://author-p106436-e993320.adobeaemcloud.com</td><td>https://publish-p106436-e993320.adobeaemcloud.com</td></tr><tr><td>L716091</td><td>https://author-p106480-e993301.adobeaemcloud.com</td><td>https://publish-p106480-e993301.adobeaemcloud.com</td></tr><tr><td>L716092</td><td>https://author-p106530-e993246.adobeaemcloud.com</td><td>https://publish-p106530-e993246.adobeaemcloud.com</td></tr><tr><td>L716093</td><td>https://author-p106481-e993352.adobeaemcloud.com</td><td>https://publish-p106481-e993352.adobeaemcloud.com</td></tr><tr><td>L716094</td><td>https://author-p106482-e993354.adobeaemcloud.com</td><td>https://publish-p106482-e993354.adobeaemcloud.com</td></tr><tr><td>L716095</td><td>https://author-p106531-e993248.adobeaemcloud.com</td><td>https://publish-p106531-e993248.adobeaemcloud.com</td></tr><tr><td>L716096</td><td>https://author-p106483-e993357.adobeaemcloud.com</td><td>https://publish-p106483-e993357.adobeaemcloud.com</td></tr><tr><td>L716097</td><td>https://author-p106433-e993318.adobeaemcloud.com</td><td>https://publish-p106433-e993318.adobeaemcloud.com</td></tr><tr><td>L716098</td><td>https://author-p106532-e993249.adobeaemcloud.com</td><td>https://publish-p106532-e993249.adobeaemcloud.com</td></tr><tr><td>L716099</td><td>https://author-p106434-e993317.adobeaemcloud.com</td><td>https://publish-p106434-e993317.adobeaemcloud.com</td></tr><tr><td>L716100</td><td>https://author-p106435-e993319.adobeaemcloud.com</td><td>https://publish-p106435-e993319.adobeaemcloud.com</td></tr>
        </tbody>
</table>

+++

## 第1課

### 目標

熟悉AEM Formsas a Cloud Service環境。

### 課程內容

在本課程中，您可導覽使用者介面，以熟悉AEM Formsas a Cloud Service環境。

### 練習

1. 開啟瀏覽器，然後輸入Cloud Service製作環境的URL。 例如：
   [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/start.html](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/start.html)

1. 登入Cloud Service製作環境。 實驗期間，您的製作環境的登入認證將會與您共用。

1. 登入後，導覽至AEM Forms UI。 按一下 **Forms**.

   ![](/help/forms/assets/screenshot2028113829.png)

1. 按一下 **Forms與檔案**. 關閉與首選項或資訊相關的彈出窗口。

   ![](/help/forms/assets/screenshot2028113929.png)

   所有可用的表單都會顯示。

   ![](/help/forms/assets/screenshot2028114029.png)

## 第2課

### 目標

使用最新的核心元件製作最適化表單、設定及提交表單。

### 課程內容

在本課程中，身為企業使用者，您將使用具有標準化OOTB核心元件的最適化表單製作功能，針對多個管道（例如網路、行動裝置和聊天）製作最適化表單，以利資料擷取。

### 練習

1. 為表單建立提交端點：

   1. 開啟 <https://requestbin.com/> 中的任何值。
      ![](/help/forms/assets/screenshot2028114329.png)

   1. 按一下 **建立公用筒** 並複製端點URL。
      ![](/help/forms/assets/screenshot202023-03-0120at206.10.0020pm.png)

1. 使用精靈介面製作最適化表單：

   1. 在第1課中使用的瀏覽器標籤中，導覽至AEM Forms作為Cloud ServiceWeb介面，並導覽至Forms和檔案。
      ![](/help/forms/assets/screenshot2028114029.png)

   1. 按一下 **建立** 並選取「最適化表單」 。
      ![](/help/forms/assets/screenshot2028114629.png)

   1. 選取 **核心元件空白** 範本選取畫面中的範本，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.1520pm.png)

   1. 按一下 **樣式** 標籤，然後選取 **wknd主題** 主題如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.2320pm.png)

   1. 按一下 **提交** 標籤，然後選取 **提交到REST終端** 卡，並指定
      **POST請求的URL** 欄位，如下所示：
      ![](/help/forms/assets/screenshot202023-03-0120at206.09.5320pm.png)

   1. 按一下&#x200B;**建立**。指定表單的名稱和標題。 例如， **聯絡圖**. 按一下&#x200B;**建立**。
      ![](/help/forms/assets/screenshot2028123329.png)

   1. 適用性表單編輯器隨即開啟。 關閉首選項或資訊的任何彈出窗口或對話框。 按一下左側邊欄上的元件瀏覽器，然後新增 **頁尾** 元件。
      ![](/help/forms/assets/screenshot2028121929.png)

   1. 標題是最適化表單範本的一部分。 它可讓您輕鬆提供所有最適化表單的一致頁首/頁尾。 或者，您也可以選擇在表單中保持其可編輯性，如下一步中的頁尾元件所示。

   1. 新增 **標題** 元件。
      ![](/help/forms/assets/screenshot2028122129.png)

   1. 新增 **文字輸入** 元件。
      ![](/help/forms/assets/screenshot2028122329.png)

   1. 新增 **數字輸入** 元件。
      ![](/help/forms/assets/screenshot2028122429.png)

   1. 新增 **提交按鈕** 元件。
      ![](/help/forms/assets/screenshot2028122529.png)

   1. 按一下 **標題** 元件 **快顯功能表** 的下界。 按一下 **編輯圖示** ，編輯標籤。
      ![](/help/forms/assets/screenshot2028122629.png)

   1. 輸入 `Contact Us` 作為標題文本。
      ![](/help/forms/assets/screenshot2028122829.png)

   1. 按一下 **文字輸入** 元件，以顯示快顯功能表。 按一下 **編輯圖示** ，編輯標籤。
      ![](/help/forms/assets/screenshot2028122929.png)

   1. 輸入 **完整名稱** 作為欄位標籤。
      ![](/help/forms/assets/screenshot2028123029.png)

   1. 按一下 **數字輸入** 元件，以顯示快顯功能表。 按一下 **編輯圖示** ，編輯標籤。
      ![](/help/forms/assets/screenshot2028123129.png)

   1. 輸入 **電話號碼** 作為欄位標籤。
      ![](/help/forms/assets/screenshot2028123829.png)


1. 將驗證添加到表單中：

   1. 按一下 **電話號碼** 元件，以顯示快顯功能表。 按一下 **扳手圖示** ，以設定欄位。
      ![](/help/forms/assets/screenshot2028123429.png)

   1. 開啟 **驗證頁簽**，標籤欄位 **必填**，然後按一下 **完成**. 會顯示成功訊息。
      ![](/help/forms/assets/screenshot2028123529.png)

      ![](/help/forms/assets/screenshot2028123629.png)

   1. 按一下 **預覽** 從最終用戶的角度預覽表單。
      ![](/help/forms/assets/screenshot2028125529.png)

   1. 用虛擬資料填寫表格
      ![](/help/forms/assets/screenshot2028125629.png)

   1. 提交表單
      ![](/help/forms/assets/screenshot2028125729.png)

   1. 在「請求框」頁簽中，檢查提交的資料。
      ![](/help/forms/assets/screenshot2028125829.png)

現在，為了進行其餘練習，請使用預先建立的註冊表。

1. 開啟AEM Forms管理介面，例如 `https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments`，然後選擇註冊表單。

   ![](/help/forms/assets/screenshot2028115529.png)

1. 按一下 **發佈**.

   ![](/help/forms/assets/screenshot2028115629.png)

   會顯示成功訊息。

   ![](/help/forms/assets/screenshot2028115729.png)

   表單的發佈URL類似於 `https://publish-p105303-e986623.adobeaemcloud.com/content/forms/af/registration.html`.

1. 若要檢視已發佈的表單，請將上述URL中的方案ID(pXXXXXX)和環境ID(eXXXXXX)取代為您環境的ID。

## 第3課

### 目標

使用前端開發最佳實務更新樣式。

### 課程內容

在本課程中，身為前端開發人員，您可以了解如何輕鬆更新先前建立之最適化表單的樣式。

### 練習

設定主題的本地儲存庫：

1. 開啟具有管理員權限的命令提示符或shell:

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令導航到 **c:\git** 資料夾

   ```Shell
   cd c:\git
   ```

1. 使用以下命令克隆主題前端代碼：

   ```Shell
   git clone -b WKND https://github.com/adobe/aem-forms-theme-canvas
   ```


1. 請依所列順序使用下列命令來導覽至 **aem-forms-theme-canvas** 目錄，然後開啟Visual Studio Code。

   ```Shell
   cd aem-forms-theme-canvas
   code .
   ```

   ![](/help/forms/assets/screenshot2028126029.png)

1. 選擇 **信任父資料夾中所有檔案的作者** 按一下 **是的，我相信作者**.

   ![](/help/forms/assets/screenshot2028116229.png)

1. 若要呈現雲端服務發佈環境上托管的表單，請重新命名 `env_template` 檔案。  若要重新命名檔案，請以滑鼠右鍵按一下 **env_template** 檔案，然後選取 **重新命名** 選項。

   ![](/help/forms/assets/screenshot2028116429.png)

   </br>

   ![](/help/forms/assets/screenshot2028116529.png)

1. 為.env檔案中的變數設定下列值並儲存檔案：

   * **AEM_URL**:指定您的雲端服務發佈環境。 例如, `https://publish-p105303-e986623.adobeaemcloud.com/`

   * **AEM_ADAPTIVE_FORM**:指定表單的路徑。 例如，如果表單路徑為 `/content/forms/af/registration`，此變數的值會是 `registration`.

   ![](/help/forms/assets/screenshot2028116429.png)


1. 在命令提示窗口中，運行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028117029.png)

   >[!NOTE]
   >
   > * 如果您收到要求透過更新npm的訊息， `npm notice Run npm nstall -g npm@9.6.0`命令，忽略消息。
   > * 除非活頁簿中有說明，否則請勿執行其他npm命令。


1. 現在，運行以下命令以預覽表單。

   ```Shell
   npm run live
   ```

   ![](/help/forms/assets/screenshot2028117229.png)

   執行上述命令後，請等待 `webpack compiled` 訊息。 表單會顯示在瀏覽器標籤中。

   >[!NOTE]
   >
   >執行 `npm run live` 命令超過3-4分鐘，請更改 `localhost` 瀏覽器URL中找到127.0.0.1並點擊 **輸入**.


   ![](/help/forms/assets/screenshot2028115129.png)


1. 在Visual Studio代碼中，開啟 `PROJECT\src\site\_variables.scss` 檔案。 請注意 `$error` 顏色是紅色的陰影。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 在瀏覽器中，提交表單以查看 **名字** 欄位。

   ![](/help/forms/assets/screenshot2028120829.png)

1. 設定 **$error** 顏色 **#5736eb** 並儲存檔案。

   ![](/help/forms/assets/screenshot2028120729.png)

1. 重新整理瀏覽器並提交表單。 注意名字欄位上的錯誤顏色已相應更改。

   ![](/help/forms/assets/screenshot2028121129.png)

1. 在命令提示符中，按 **CTRL+C**，輸入 **Y**，然後按 **輸入** 終止npm進程的鍵。 請務必停止npm伺服器，以免與下一組練習衝突。
1. 關閉Visual Studio代碼和命令提示窗口。

## 第4課

### 目標

將表單轉譯為網頁/行動裝置和其他介面，做為無頭表單。

### 課程內容

在本課程中，您將學習如何使用react光譜設計架構，將先前建立的最適化表單轉譯為無頭表單。

### 練習

使用react入門專案設定本機存放庫：

1. 使用管理員權限開啟命令提示。

   ![](/help/forms/assets/screenshot2028115829.png)

1. 在命令提示符下，使用以下命令導航到 **c:\git** 資料夾

   ```Shell
   cd c:\git
   ```

1. 使用下列命令來複製最適化表單react啟動器專案：

   ```Shell
   git clone https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028117329.png)

1. 以下命令的順序導航到 **react-starter-kit-aem-headless forms** 目錄，然後開啟Visual Studio Code。

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028117529.png)


   將開啟「Visual Studio Code 」窗口。

   ![](/help/forms/assets/screenshot2028117429.png)

若要呈現托管於雲端服務發佈環境的表單：

1. 將env_template檔案更名為.env檔案。 若要重新命名，請以滑鼠右鍵按一下 **env_template** 檔案，然後選取 **重新命名** 選項。

   ![](/help/forms/assets/screenshot2028117629.png)

   ![](/help/forms/assets/screenshot2028117729.png)

1. 為.env檔案中的變數設定下列值。 更新變數後，儲存檔案。

   * **AEM_URL**:指定雲端服務發佈環境的URL。 例如, `https://publish-p105303-e986623.adobeaemcloud.com`

   * **AEM_FORM_PATH**:指定在上一課中建立的最適化表單路徑。 例如, `/content/forms/af/registration/`

      ![](/help/forms/assets/screenshot202023-03-0820at202.49.1820pm.png)

1. 開啟命令視窗，確認您位於react-starter-kit-aem-headless-forms目錄，然後執行下列命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028118029.png)


1. 在命令提示窗口中，運行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028118129.png)

   上述命令會啟動本機開發伺服器，透過react-spectrum前端程式庫，以無頭方式轉譯從AEM擷取的表單定義。

   >[!NOTE]
   >
   > 
   > 執行 `npm start` 命令超過3-4分鐘，請更改 `localhost` 瀏覽器URL中找到127.0.0.1並點擊 **輸入**.

   ![](/help/forms/assets/screenshot2028118229.png)

讓我們以此無頭形式檢查規則的執行：

1. 選取 **核取方塊即可獲得5%的優惠** 選項。 後續的信用卡應用選項將被禁用。

   ![](/help/forms/assets/screenshot2028126229.png)

1. 取消選中 **核取方塊即可獲得5%的優惠** 啟用信用卡選項。

   ![](/help/forms/assets/screenshot2028126329.png)

讓我們以業務用戶的身份在伺服器上對表單進行更改，並自動查看無頭表單中反映的更改。

1. 在瀏覽器中開啟AEM Forms管理介面。 例如， [https://author-p105303-e986623.adobeaemcloud.com/ui#/aem/aem/forms.html/content/dam/formsanddocuments](https://author-p105303-e986623.adobeaemcloud.com/ui%23/aem/aem/forms.html/content/dam/formsanddocuments).

1. 選取 **註冊** 表單並按一下 **編輯。** 它會在最適化表單編輯器中開啟表單。

   ![](/help/forms/assets/screenshot2028118529.png)

1. 選取 **電話號碼** 欄位，然後按一下 **編輯圖示（鉛筆圖示）** 的下一頁。 如果看不到彈出工具欄，請按一下「編輯」模式 **編輯** 按鈕，從左到右 **預覽** 按鈕。

   ![](/help/forms/assets/screenshot2028119629.png)

1. 將標籤變更為行動電話號碼。 按一下表單中的任何空白字元，便會儲存對表單所做的變更。

   ![](/help/forms/assets/screenshot2028119729.png)

讓我們發佈更新後的表單，將變更傳播至發佈環境。

1. 在AEM Forms管理介面索引標籤中，選取註冊表單，然後按一下 **取消發佈**. 如果您沒有看到 **取消發佈** 按鈕，跳至步驟3直接發佈變更。

   ![](/help/forms/assets/screenshot2028119829.png)

1. 按一下 **取消發佈**. 按一下 **關閉** 對話方塊。

   ![](/help/forms/assets/screenshot2028119929.png)

   ![](/help/forms/assets/screenshot2028120029.png)


1. 瀏覽器重新整理後，選取註冊表單並按一下 **發佈**.

   ![](/help/forms/assets/screenshot2028120129.png)


1. 按一下 **發佈**. 按一下 **關閉** 在相應對話框中。

   ![](/help/forms/assets/screenshot2028120329.png)

   ![](/help/forms/assets/screenshot2028120429.png)

1. 重新整理瀏覽器標籤，並顯示無標題表單。 請注意，電話號碼標籤已變更為行動電話號碼。

   ![](/help/forms/assets/screenshot2028120529.png)

1. 開啟用於啟動 **react-starter-kit-aem-headless forms** 項目，按 **CTRL+C**，然後輸入 **Y** 按Enter鍵終止npm進程。 請務必停止npm伺服器，以免與下一組練習衝突。

1. 關閉Visual Studio代碼和命令提示窗口。


## 第5課

### 目標

使用Google Material UI將表單轉譯為無頭表單

### 課程內容

在本課程中，您身為前端開發人員，了解如何使用Google材料UI，將先前建立的最適化表單轉譯為無頭表單。

### 練習

使用材料UI入門項目設定本地儲存庫：

1. 使用管理員權限開啟命令提示。

   ![](/help/forms/assets/screenshot2028115829.png)


1. 在命令提示符下，使用以下命令導航到 **c:\git** 資料夾：

   ```Shell
   cd c:\git
   ```

1. 按列出順序運行以下命令，以建立名為mui的資料夾，並使用以下命令導航到mui資料夾：

   ```Shell
   mkdir mui
   
   cd mui
   ```

1. 使用下列命令來複製最適化表單react啟動器專案：

   ```Shell
   git clone -b mui https://github.com/adobe/react-starter-kit-aem-headless-forms
   ```

   ![](/help/forms/assets/screenshot2028126529.png)

1. 請依所列順序使用下列命令來導覽至 **react-starter-kit-aem-headless forms** 資料夾，並在Visual Studio代碼中開啟代碼：

   ```Shell
   cd react-starter-kit-aem-headless-forms
   
   code .
   ```

   ![](/help/forms/assets/screenshot2028126829.png)

若要呈現托管於雲端服務發佈環境的表單：

1. 重新命名 **env_template** 檔案 **.env** 檔案。 若要重新命名，請以滑鼠右鍵按一下 **env_template** 檔案和選取 **重新命名**.

   ![](/help/forms/assets/screenshot2028126629.png)

1. 為.env檔案中的變數設定下列值。 更新變數後，儲存檔案。 使用 **CTRL + S** 切換組合以儲存檔案。

   * **AEM_URL**:指定雲端服務發佈環境的URL。 例如， [https://publish-p105303-e986623.adobeaemcloud.com](https://publish-p105303-e986623.adobeaemcloud.com/)

   * **AEM_FORM_PATH**:指定在上一課中建立的最適化表單路徑。 例如， /content/forms/af/registration/

      ![](/help/forms/assets/screenshot2028126929.png)

1. 開啟命令視窗，確定您位於 **react-starter-kit-aem-headless forms** 目錄，然後運行以下命令：

   ```Shell
   npm install
   ```

   ![](/help/forms/assets/screenshot2028127029.png)

1. 在命令提示窗口中，運行以下命令：

   ```Shell
   npm start
   ```

   ![](/help/forms/assets/screenshot2028127129.png)

   命令會啟動本機開發伺服器，並使用Google Material UI前端程式庫以無頭方式轉譯從AEM擷取的表單定義。

   >[!NOTE]
   >
   >執行 `npm start` 命令超過3-4分鐘，請更改 `localhost` 瀏覽器URL中找到127.0.0.1並點擊 **輸入**.

   ![](/help/forms/assets/screenshot2028127229.png)

1. 要在此表單格式副本中評估相同業務邏輯的執行：

   選擇 **核取方塊即可獲得5%的優惠**. 後續選項 **是否申請We.Finance公司信用卡表？** 被禁用。

   ![](/help/forms/assets/screenshot2028127329.png)

## 第6課

### 目標

使用「材料」UI元件變數建立無頭表單的替代外觀和風格

### 課程內容

在本課程中，身為前端開發人員，您將學習如何針對商業使用者先前建立的最適化表單，使用材料UI，建立不同元件的替代表示。

### 練習

更新無頭專案中元件的變化。 將材料UI文本輸入元件的變體更改為 `OutlinedInput`:

1. 在可視代碼中，通過開啟 `index.tsx` 檔案位置 `src/components/textinput/index.tsx`.

1. 新增 `//` 在代碼行103的開頭。 它會將行轉換為註解。

   ```Shell
   //const Cmp = \'outlined\' === appliedCssClassNames ? OutlinedInput: Input;
   ```

1. 在第104行新增下列項目，以使用不同的元件變體並儲存檔案。 使用 **CTRL + S** 切換組合以儲存檔案。

   ```Shell
   const Cmp = OutlinedInput;
   ```

   ![](/help/forms/assets/screenshot2028127629.png)

   必須對&#39;HoreadInput&#39;變體使用正確的大寫，否則編譯將會失敗。 本地開發環境編譯在命令提示符中自動開始。 等到您看到下列訊息為止

   `webpack 5.75.0 compiled with 3 warnings in 6659 ms`
   `inside proxy req`
   `setting new origin header`

1. 重新整理瀏覽器（如果瀏覽器未自動重新整理），以查看使用不同變體的文字輸入元件。

   ![](/help/forms/assets/screenshot2028127729.png)


   這項變更適用於一般使用者，而AEM Forms伺服器的表單定義沒有任何變更，且專屬於考慮中的無頭通道。 例如，本實驗中的Web通道。

   ![](/help/forms/assets/screenshot2028127529.png)


1. 關閉Visual Studio代碼和命令提示窗口。

## 常見問題集(FAQ)

+++ 適用性表單精靈是否可公開使用？

是的，可搭配AEM FormsCloud Service。

+++


+++ 核心元件是否已公開提供？

是的，適用性Forms核心元件以AEM Forms為Cloud Service提供。

+++

+++ 無頭式表單是否可公開提供？

是，無頭表單以AEM Forms為Cloud Service。

+++

+++ 無頭式表單是否需要單獨的授權？

否，無頭表單使用相同的授權值量度、表單提交數量。

+++

+++ AEM 6.5 Forms是否提供核心元件和無頭表單？

是的，AEM Forms 6.5 Service Pack 16以上版本均提供最適化表單核心元件和無頭表單。

+++


## 後續步驟

現在您已了解如何使用無頭表單建立最適化表單並將其傳遞至多個管道，因此您應嘗試運用新的技巧。 快樂地前行，大規模地為您的最終用戶建立並提供卓越的資料捕獲體驗！

## 資源

* [適用性表單核心元件簡介](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)

* [使用核心元件建立最適化表單](https://experienceleague.corp.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)

* [更新核心元件型AF的樣式](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components.html?lang=en)

* [無頭式最適化表單](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=en)

* [使用無頭式React入門套件](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/get-started/create-and-publish-a-headless-form.html?lang=en)


