---
title: 中繼資料管理和最佳做法
description: 瞭解中繼資料最佳實務，以有效管理您的數位資產。
role: User, Admin
exl-id: d90519df-55a6-4e23-81ad-ff2365d71c0d
feature: Metadata, Best Practices
source-git-commit: c82f84fe99d8a196adebe504fef78ed8f0b747a9
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 2%

---

<!-- Keywords to focus on:
metadata best practices
aem metadata 
experience manager metadata-->

# 中繼資料管理和最佳做法 {#metadata-best-practices}

<table>
    <tr>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/dm-prime-ultimate.md"><b>Dynamic Media Prime和Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/assets-ultimate-overview.md"><b>AEM Assets Ultimate</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md"><b>AEM Assets與Edge Delivery Services整合</b></a>
        </td>
        <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/aem-assets-view-ui-extensibility.md"><b>UI擴充性</b></a>
        </td>
          <td>
            <sup style= "background-color:#008000; color:#FFFFFF; font-weight:bold"><i>新</i></sup> <a href="/help/assets/dynamic-media/enable-dynamic-media-prime-and-ultimate.md"><b>啟用Dynamic Media Prime和Ultimate</b></a>
        </td>
    </tr>
    <tr>
        <td>
            <a href="/help/assets/search-best-practices.md"><b>搜尋最佳實務</b></a>
        </td>
        <td>
            <a href="/help/assets/product-overview.md"><b>Content Hub</b></a>
        </td>
        <td>
            <a href="/help/assets/dynamic-media-open-apis-overview.md"><b>具有 OpenAPI 功能的 Dynamic Media</b></a>
        </td>
        <td>
            <a href="https://developer.adobe.com/experience-cloud/experience-manager-apis/"><b>AEM Assets 開發人員文件</b></a>
        </td>
    </tr>
</table>

若要讓您的企業脫穎而出，並吸引更多客戶，運用影像、視訊和其他數位資產等高品質視覺效果至關重要。 為此，您需要可讓您將中繼資料新增到所有數位資產的程式，以便輕鬆搜尋。 中繼資料是提供有關數位資產的重要詳細資訊，包括資產名稱、型別、存放庫內的位置、修改日期和關聯標籤。 中繼資料可簡化資產管理、改善搜尋能力和協助工具，並確保有效的版本控制。

瞭解如何在數位資產管理(DAM)系統中使用中繼資料，以有效[管理您數位資產的中繼資料](manage-metadata.md)。

## 中繼資料的型別

根據資料的各個方面，中繼資料可分類為技術中繼資料、資訊中繼資料及管理中繼資料。

### 技術中繼資料

技術中繼資料包括資產的技術方面。 這類中繼資料對於使用者瞭解數位資產的內在特性至關重要，可促進有效率的處理和利用。
其中包含下列詳細資訊：

* 檔案大小
* 格式
* 解決方法
* 尺寸
* 色彩模式

### 資訊性中繼資料

資訊性中繼資料包含可增進對資產內容的瞭解的描述性資訊。 此中繼資料在內容探索、搜尋能力及資產重要性理解方面至關重要。 資訊中繼資料包括關鍵字、標題和說明。

例如，在Experience Manager Assets中管理視訊時，我們可以包含以下資訊性中繼資料：

* **關鍵字**：行銷、產品發佈、促銷
* **Caption**：介紹我們最新產品，以及令人興奮的功能
* **描述**：視訊內容的詳細概觀。

搜尋行銷相關內容的使用者可輕鬆找到並瞭解上述影片的重要意義。

### 管理中繼資料

管理中繼資料會處理數位資產的管理方面。 它可確儲存取控制、法規遵循，以及管理數位資產管理系統中資產的整體生命週期。 其中包含下列相關資訊：

* 資產所有權
* 使用許可權
* 權限
* 其他管理詳細資料

管理中繼資料可確保正確的資產管理、控制存取權，以及數位資產管理系統內的合規性。

## 中繼資料最佳實務

### 從頭定義您的中繼資料策略

中繼資料管理首先會定義中繼資料策略，為評估長期值奠定基礎。

根據您的需求建立自訂中繼資料結構在規劃中繼資料策略時十分重要。 設計良好的結構描述提供了在Experience Manager中分類及組織資產的結構化架構。

#### 影片：新增自訂欄位至中繼資料結構

>[!VIDEO](https://video.tv.adobe.com/v/3425977)

您的中繼資料策略可能包括定義下列專案：

* **目標：**&#x200B;清楚說明中繼資料的目標和預期結果。 透過新增中繼資料，找出您想要達成的目標。

* **用途：**&#x200B;定義您擷取中繼資料的原因。 指定它新增至您的流程、系統或組織的值。

* **協助工具計畫：**&#x200B;建立計畫，讓中繼資料易於存取和發現。 說明要使用它的人員，以及要使用的工具或方法。

* **中繼資料屬性：**&#x200B;請仔細識別並定義每個中繼資料屬性。 確保每個屬性都有明確的原因可以納入，並連結到目標和目的。

為確保整個存放庫獲得一致的結果，請仔細規劃策略。 深入瞭解[中繼資料結構](metadata-schemas.md)。

### 建立中繼資料治理計畫

資料控管可確保組織的中繼資料管理工作與整體業務目標一致。
治理策略可能包括：

* 建立資料和中繼資料管理的原則和程式。
* 設定資料品質和完整性的標準。
* 定義資料管理中的角色和責任。

判斷資訊的來源，並檢查中繼資料策略的詳細資訊，包括屬性及其來源。 可依策略的複雜度調整規模。 在大型企業中，有一個主中繼資料管理系統監督主棧疊中的多個系統。

>[!NOTE]
>
>瞭解如何[管理數位資產的中繼資料](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/metadata.html)。

### 與中繼資料策略一致

一致的中繼資料策略可確保數位資產的有效組織和擷取。 採用策略方法擷取及實作中繼資料值，提供演化的彈性，避免不必要的變更。<br>

在企業範圍的中繼資料管理中，為資產命名和參照資產時，一致性很重要。 例如，同時管理多個資產時，「請考慮大量新增中繼資料。<br>

以下是一些要遵循的最佳實務：

* **避免重複值：**&#x200B;如果您擁有行銷活動的影像集合，請使用一致的名稱並避免重複。<br>
舉例來說，請實作系統性的命名慣例（例如*event_promotion*&#x200B;和&#x200B;*product_launch*），而不使用重複的名稱（如&#x200B;*campaign_image_001*&#x200B;和&#x200B;*campaign_image_002*），以確保識別清楚且有序。

* **有效使用控制辭彙：**&#x200B;使用標準化的標籤辭彙來實作控制辭彙。 瞭解如何有效實作[AEM Tagging Framework](/help/implementing/developing/introduction/tagging-framework.md)。  <br>
例如，當使用主題標籤影像以維持系統順序時，請一致使用*product_launch*&#x200B;或&#x200B;*event_promotion*&#x200B;等辭彙。

* **維持正確性和完整性：**&#x200B;若要保持中繼資料的一致性，正確性、完整性和各種來源之間的一致性至關重要。
例如，將中繼資料新增至PDF檔案時，請確認作者名稱和關鍵字等詳細資料正確且完整。

#### 影片：將大量中繼資料新增至資產

>[!VIDEO](https://video.tv.adobe.com/v/3425978)

### 評估並改善中繼資料搜尋能力

評估您的中繼資料策略以改善中繼資料搜尋能力。 簡化工作流程並增強搜尋功能，以有效重複使用。 避免處理缺乏明確目的的中繼資料。

您可以考慮以下最佳實務，以最佳化中繼資料搜尋能力：

* **關鍵字最佳化：**&#x200B;藉由最佳化與資產相關聯的關鍵字來改善中繼資料搜尋能力。 您可以依照下列步驟，改善[!UICONTROL Assets Manager]中特定資產的關鍵字關聯性：

   1. 移至&#x200B;**[!UICONTROL Assets]** > **[!UICONTROL 檔案]** > **[!UICONTROL [資產資料夾]]**。
   1. 選取您要更新中繼資料的資產，然後按一下&#x200B;**[!UICONTROL 屬性]**。
   1. 導覽至&#x200B;**[!UICONTROL 進階]**&#x200B;索引標籤，然後按一下&#x200B;**[!UICONTROL 提升搜尋關鍵字]**&#x200B;下的&#x200B;**[!UICONTROL 新增]**。 <br>您必須使用預設的中繼資料結構描述來提升搜尋關鍵字。
   1. 輸入您要增加搜尋的關鍵字，然後按一下[新增]。**&#x200B;**<br>
您可以新增多個關鍵字，並根據您的優先順序排列關鍵字。
   1. 按一下&#x200B;**[!UICONTROL 儲存並關閉]**。
使用您新增的關鍵字搜尋資產。 資產會出現在最熱門的搜尋結果中。

  瞭解如何[在Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/search-and-discovery/search-boost.html)中提升搜尋。

* **自訂中繼資料欄位：**&#x200B;自訂中繼資料欄位，以擷取有關資產的其他資訊。 例如，為專案詳細資訊、版權資訊或任何其他可增強搜尋功能的相關資料新增特定欄位。 瞭解如何在Experience Manager Assets中編輯或新增自訂中繼資料[&#128279;](meta-edit.md)。


* **中繼資料驗證：**&#x200B;實作中繼資料專案的驗證檢查，以確保一致性和準確性。 使用受控辭彙表可讓驗證程式更順暢，並減少輸入內容不清楚或不一致的機率。 這可能涉及為某些中繼資料屬性設定指導方針，以避免資訊模糊或不一致。

* **使用追蹤：**&#x200B;評估不同中繼資料屬性在一段時間內的關聯性和使用情形。 識別並排定常用中繼資料的優先順序，或大幅促進搜尋和擷取程式。

#### 影片：新增關鍵字以改善搜尋能力

>[!VIDEO](https://video.tv.adobe.com/v/3425979)

### 讓中繼資料簡單明瞭

簡化中繼資料，以提升控管能力和使用者採用程度。 保持簡明易懂，鼓勵使用者新增重要資訊。
請嘗試下列最佳實務來簡化中繼資料：

* **最佳化屬性選項：**&#x200B;著重於強調基本屬性，避免讓使用者負擔太多要填寫的中繼資料欄位。 例如，在為影像新增中繼資料時，僅包含標題、說明和標籤等關鍵欄位，以便有效分類。

* **消除不必要的預設屬性：**&#x200B;透過消除與您的使用案例無關的預設現成屬性來簡化中繼資料表單。 移除鮮少使用的預設屬性，以獲得更乾淨的介面和體驗。

* **定期檢閱和更新中繼資料：**&#x200B;定期更新中繼資料，並因應不斷變化的需求和技術，以確保使用者隨著時間提供有價值的資訊。

### 分析內容歷程

檢查內容供應鏈以尋找中繼資料來源，並動員所有利害關係人（從最高層開始）參與，以取得徹底的最佳實務方法。 讓不同的員工參與，以確保整個組織的完整支援。 <br>在不同階段合併中繼資料，以分擔在上傳期間提供資產詳細資訊的責任。 例如，整合[!DNL Experience Manager Assets]和[!DNL Workfront]可在中繼資料管理、提升內容建立與管理的效率及共同作業方面提供顯著的好處。 此整合可確保連結資產的有效中繼資料同步，在[!DNL Workfront]中進行變更時自動更新專案詳細資料。

及早溝通目標、進度、里程碑和挑戰，以接收所有利害關係人的意見與合作。 鼓勵整個組織的共同作業，建立有效率的流程和寶貴的中繼資料。

深入瞭解[中繼資料及其相關概念](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/metadata-concepts.html)，以有效管理您的Experience Manager中繼資料。
