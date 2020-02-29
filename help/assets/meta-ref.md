---
title: 中繼資料圖式參考
description: '瞭解描述資產中繼資料的標準慣例，包括Dublin Core、IPTC和其他中繼資料結構。 '
contentOwner: AG
translation-type: tm+mt
source-git-commit: f2e257ff880ca2009c3ad6c8aadd055f28309289

---


# 中繼資料圖式參考 {#metadata-schemata-reference}

以下參考包括關於特定元資料方案的資訊（按字母順序）以及屬性清單及其定義。

## Dublin Core {#dublin-core}

Dublin Core中繼資料提供一組標準化的慣例，用於描述資產，以便更容易找到。 在AEM Assets中，Dublin Core說明數位資產，包括視訊、音效、影像和檔案。

簡單的Dublin Core Metadata Element Set(DCMES)包含15個中繼資料元素，如下表所列。 每個Dublin core元素都是選用的，可重複。 您可以像新增或刪除媒體類型特定中繼資料一樣，新增或刪除Dublin Core中繼資料資訊。

除了DCMES之外，還有Dublin Core Initiative（都柏林核心計畫）建立的其他元資料元素。 如需詳細 [資訊，請參閱Dublin Core](https://dublincore.org/) Initiative。

<table>
 <tbody>
  <tr>
   <td><strong>屬性</strong></td> 
   <td><strong>說明</strong></td> 
  </tr>
  <tr>
   <td>contributor</td> 
   <td>負責對內容作出貢獻的人士或公司。</td> 
  </tr>
  <tr>
   <td>覆蓋率</td> 
   <td>資產涵蓋的地理位置或時段。<br /> </td> 
  </tr>
  <tr>
   <td>製造者</td> 
   <td>負責建立內容的人員或公司。</td> 
  </tr>
  <tr>
   <td>日期</td> 
   <td>與資產相關的日期或期間。<br /> </td> 
  </tr>
  <tr>
   <td>說明</td> 
   <td>資產的詳細資訊。</td> 
  </tr>
  <tr>
   <td>格式</td> 
   <td>資產的檔案格式、實體媒體或尺寸。 AEM使 <code>dc:format</code> 用來表示資產的MIME類型。<br /> </td> 
  </tr>
  <tr>
   <td>識別碼</td> 
   <td>資產的唯一參考。</td> 
  </tr>
  <tr>
   <td>語言</td> 
   <td>資產的語言（例如，英文為en）。</td> 
  </tr>
  <tr>
   <td>publisher</td> 
   <td>負責使資產可供使用的人員或公司。</td> 
  </tr>
  <tr>
   <td>關係</td> 
   <td>相關資產。</td> 
  </tr>
  <tr>
   <td>權利</td> 
   <td>關於誰有權使用此資產的資訊。</td> 
  </tr>
  <tr>
   <td>source</td> 
   <td>資產衍生自之相關資產。</td> 
  </tr>
  <tr>
   <td>主旨</td> 
   <td>資產的主題。<br /> </td> 
  </tr>
  <tr>
   <td>標題</td> 
   <td>資產的名稱。</td> 
  </tr>
  <tr>
   <td>類型</td> 
   <td>資產的性質或類別。</td> 
  </tr>
 </tbody>
</table>

## IPTC {#iptc}

國際新聞通訊委員會(IPTC)是由全球新聞機構組成的聯合體，其目標之一是制定和維護技術標準。 IPTC為影像定義了一套像片中繼資料標準，在攝影師中幾乎被普遍接受。 這些元資料標準是20世紀90年代建立的更廣泛標準的一部分，即IPTC資訊交換模型(IIM)。

雖然IPTC標題資訊已大部份被XMP取代，但XMP可使用IPTC核心架構和擴充架構。 在影像程式中，XMP和IPTC屬性都會同步。
