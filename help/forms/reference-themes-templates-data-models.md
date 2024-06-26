---
title: 如何取得AEM表單的參考主題和範本？
description: AEM Forms提供範例調適型表單主題、範本和表單資料模型，以協助您快速建立表單。
feature: Adaptive Forms, Foundation Components
exl-id: 81588759-22da-4123-92fe-5ca97e97f1e4
role: User, Developer, Admin
source-git-commit: 2b76f1be2dda99c8638deb9633055e71312fbf1e
workflow-type: tm+mt
source-wordcount: '778'
ht-degree: 9%

---

# 參考主題、範本和表單資料模型 {#reference-themes-templates-and-data-models}


| 套用至 | 文章連結 |
| -------- | ---------------------------- |
| 根據核心元件的最適化表單 | [按一下這裡](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components.html) |
| 根據Foundation元件的最適化表單 | 本文章 |

<span class="preview">Adobe 建議使用新式且可擴充的資料擷取[核心元件](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)，用來[建立新的最適化表單](/help/forms/creating-adaptive-form-core-components.md)或[將最適化表單新增到 AEM Sites 頁面](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)。這些元件代表最適化表單建立方面的重大進步，可確保令人印象深刻的使用者體驗。本文會介紹使用基礎元件編寫最適化表單的舊方法。</span>

AEM Formsas a Cloud Service提供多種參考主題、範本和表單資料模型(FDM)，可幫助您快速開始建立最適化Forms。 您可以下載 [來自軟體發佈入口網站的參考內容套件](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 並使用 [封裝管理員](/help/implementing/developing/tools/package-manager.md) 安裝 [參考內容封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip) 在您的生產、開發或本機開發環境中，將這些參考資產帶至您的環境。

參考內容套件中包含的主題、範本和表單資料模型(FDM)包括：


| 主題 | 範本 | 表單資料模型(FDM) |
---------|----------|---------
| Canvas 3.0 | 基本 | Microsoft Dynamics 365 |
| 寧靜 | 空白 | Salesforce |
| 城市化 |   |  |
| Ultraminary |  |  |
| 貝瑞爾 |  |  |
| 保健 |  |   |
| FSI |   |   |

## 參考主題 {#reference-themes}

[主題](/help/forms/themes.md) 讓您不具備CSS的深入知識，也能設定表單樣式。 您可以安裝 [參考內容封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* 貝瑞爾
* Canvas 3.0
* 寧靜
* 城市化
* Ultraminary
* 保健
* FSI （金融服務與保險）

每個佈景主題都包含獨特且優雅的樣式，可用來為使用者建立令人愉悅的最適化表單。 它包含面板、文字方塊、數值方塊、選項按鈕、表格和切換器等選取器的唯一樣式。 這些主題中的樣式是根據需求。 例如，在特定案例中，您需要使用簡潔字型的極簡佈景主題。 自由佈景主題可讓您達到這個效果。

![參考主題](assets/ref-themes.png)

此套裝中包含的主題為回應式主題，這些主題中的樣式是為行動裝置和桌上型顯示器所定義。 各種裝置上的大部分現代化瀏覽器都能輕鬆轉譯套用這些主題之一的表單。

如需安裝套件的詳細資訊，請參閱 [如何使用套件](/help/implementing/developing/tools/package-manager.md).

## 貝瑞爾 {#beryl}

柏瑞佈景主題強調使用背景影像、透明度與大平面圖示。 在下方熒幕擷圖中，您可以看到Beryl佈景主題的外觀，以及如何增強表單的樣式。

![柏瑞爾主題](assets/beryl.png)

## Canvas 3.0 {#canvas}

Canvas 3.0是Adaptive Forms的預設主題，並強調使用基本顏色、透明度和平坦圖示。 在下方熒幕擷圖中，您可以看到Canvas 3.0佈景主題的外觀。

![柏瑞爾主題](assets/canvas.png)


## 寧靜 {#tranquil}

寧靜的佈景主題提供寧靜色彩配置的明暗陰影，以突顯表單的不同元件。 例如，單選按鈕、面板和標籤會以不同的綠色顯示。

![寧靜的主題](assets/tranquil.png)


## 城市化 {#urbane}

城市佈景主題強調您的外型應具有極簡和功能外觀。 當您在表單上套用Urbane佈景主題時，可以看到元件是平面的。 這些面板的外框很薄，可以打造現代外觀。

![都市佈景主題](assets/urbane.png)


## Ultraminary {#ultramarine}

Ultraminary主題使用深藍色陰影來反白標示元件，例如定位點、面板、文字方塊和按鈕。

![超海洋主題](assets/ultramarine.png)

## 保健 {#healthcare}

醫療保健主題使用深綠色陰影來反白顯示標籤、面板、文字方塊和按鈕等元件。

![FSI主題](assets/healthcare.png)


## FSI （金融服務與保險）

FSI主題強調表單的極簡和功能外觀。 當您將FSI主題套用至表單時，您會看到面板元件是黃色。

![FSI主題](assets/fsi.png)

## 參考範本 {#reference-templates}


[範本](/help/forms/themes.md) 可讓您定義表單的初始表單結構、內容和動作。 您可以安裝 [參考內容封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* 基本
* 空白

基本範本可協助您快速建立登錄檔單。 您也可以用它來預覽最適化Forms基礎元件的功能。 它提供精靈版面配置，用於逐節呈現資料。 使用「空白」範本，開始在空白畫布上從建立最適化表單。


## 參考表單資料模型(FDM) {#reference-models}

最適化Forms然後可以與Microsoft Dynamics 365和Salesforce伺服器互動，以啟用業務工作流程。 例如：

* 將資料寫入Microsoft Dynamics 365和Salesforce on Adaptive Form提交。
* 透過表單資料模型(FDM)中定義的自訂實體將資料寫入Microsoft Dynamics 365和Salesforce，反之亦然。
* 查詢Microsoft Dynamics 365和Salesforce伺服器以取得資料，並預先填入Adaptive Forms。
* 從Microsoft Dynamics 365和Salesforce伺服器讀取資料。

您可安裝 [參考內容封裝](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?package=/content/software-distribution/en/details.html/content/dam/aemcloud/public/aem-forms-reference-content.ui.content-2.1.0.zip)：

* Microsoft® Dynamics 365
* Salesforce

如需使用這些模型的詳細資訊，請參閱 [設定Microsoft Dynamics 365和Salesforce雲端服務](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en#configure-dynamics-cloud-service)


## 另請參閱 {#see-also}

{{see-also}}