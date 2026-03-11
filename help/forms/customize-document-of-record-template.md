---
title: 如何為最適化Forms自訂自動產生的記錄檔案範本？
description: 瞭解如何使用Adobe Forms Designer下載、自訂和重新上傳最適化Forms的自動產生記錄檔案(DoR)範本。
feature: Adaptive Forms, Core Components, Foundation Components
role: User, Developer
badgeSaas: label="AEM Forms" type="Positive" tooltip="適用於AEM Forms)。"
exl-id: 2416add3-0b9d-4a8d-a84d-d65c0762d8e8
source-git-commit: 89b0f2a8ca9d2f60365a5c3962b0b4e826f79b3e
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 1%

---

# 自訂自動產生的記錄檔案範本

<span class="preview">本文適用於&#x200B;**核心元件**&#x200B;和&#x200B;**基礎元件**&#x200B;的最適化Forms。</span>

當您為最適化表單自動產生記錄檔案(DoR)時，AEM Forms會根據表單結構建立預設範本。 您可以自訂此自動產生的範本，以符合貴組織的品牌和版面配置需求。

自訂工作流程涉及三個步驟：

1. 從Forms Manager下載自動產生的DoR範本。
1. 使用Adobe Forms Designer修改範本。
1. 將自訂範本重新上傳至AEM Forms，並將其設定為自訂範本。

## 先決條件 {#prerequisites}

開始之前，請確定您具備下列條件：

* 存取具有下載和上傳範本許可權的AEM Forms Manager。
* Adobe Forms Designer已安裝在您的本機電腦上。
* 已啟用&#x200B;**[!UICONTROL 產生記錄檔案]**&#x200B;的最適化表單。

## 步驟1：下載自動產生的DoR範本 {#download-auto-generated-dor-template}

若要下載為您的最適化表單自動產生的DoR範本（XDP檔案）：

1. 登入您的AEM Forms作者執行個體。
1. 導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
1. 選取您要下載DoR範本的最適化表單。
1. 開啟所選最適化表單的屬性。
1. 在屬性面板中，選取&#x200B;**[!UICONTROL 下載記錄檔案]**&#x200B;選項，即可下載自動產生的DoR範本（XDP檔案）。
1. 將下載的XDP檔案儲存至本機電腦。


## 步驟2：使用Adobe Forms Designer自訂範本 {#customize-template-using-designer}

在Adobe Forms Designer中開啟下載的XDP範本，並根據您組織的需求加以修改。

1. 在&#x200B;**Adobe Forms Designer**&#x200B;中開啟下載的XDP檔案。
1. 視需要自訂範本。 自訂範例包括：

   * **多個主版頁面**：新增其他主版頁面，以定義記錄檔案特定頁面的不同版面。 例如，使用帶有公司抬頭的不同第一頁和佈局較簡單的後續頁面。
   * **字型顏色和字型系列**：變更字型顏色、大小和系列，以符合您公司的品牌方針。
   * **自訂元素**：新增公司標誌、頁首、頁尾和免責宣告文字等元素，以建立一致的品牌識別。
   * **版面配置與樣式**：調整邊界、間距和整體頁面結構以改善可讀性。
   * **欄位樣式和位置**：修改表單欄位的外觀和位置，以符合您偏好的版面。

1. 儲存自訂的XDP範本。

>[!NOTE]
>
> 請勿移除或修改範本中存在的任何指令碼。 修改指令碼可能會影響資料繫結和記錄檔案產生。

## 步驟3：將自訂範本重新上傳至AEM {#reupload-customized-template}

自訂範本後，請將其上傳至AEM Forms並設定最適化表單來使用。

1. 將自訂的XDP範本上傳到您的AEM Forms執行個體：
   * 導覽至&#x200B;**[!UICONTROL Forms]** > **[!UICONTROL Forms和檔案]**。
   * 選取&#x200B;**[!UICONTROL 建立]** > **[!UICONTROL 檔案上傳]**&#x200B;並上傳自訂的XDP檔案。

然後設定表單以使用自訂範本。 步驟因您的表單是以核心元件或基礎元件為基礎而有所不同。

>[!BEGINTABS]

>[!TAB 核心元件]

針對根據核心元件的調適型Forms：

1. 在您要套用自訂範本的編輯器中開啟最適化表單。
1. 在內容樹狀結構中，選取&#x200B;**[!UICONTROL 參考線容器]** （根面板）。
1. 開啟&#x200B;**[!UICONTROL 屬性]**&#x200B;並按一下&#x200B;**[!UICONTROL 記錄檔案]** (DoR)圖示以開啟記錄檔案屬性。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，開啟&#x200B;**[!UICONTROL 範本]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 自訂]**。
1. 瀏覽並選取已上傳的自訂XDP範本。
1. 選取核取記號以儲存。

   ![記錄檔案屬性 — 範本設定為自訂（核心元件）](/help/forms/assets/submission-pdf-dor-custom-template.png)

>[!TAB Foundation 元件]

對於以基礎元件為基礎的最適化Forms：

1. 在您要套用自訂範本的編輯器中開啟最適化表單。
1. 選取根面板（表單容器）。
1. 開啟&#x200B;**[!UICONTROL 記錄檔案屬性]** （從屬性面板或DoR標籤）。
1. 在&#x200B;**[!UICONTROL 基本]**&#x200B;索引標籤中，開啟&#x200B;**[!UICONTROL 範本]**&#x200B;下拉式清單，並選取&#x200B;**[!UICONTROL 自訂]**。
1. 瀏覽並選取已上傳的自訂XDP範本。
1. 選取&#x200B;**[!UICONTROL 完成]**&#x200B;以儲存。

   ![記錄檔案屬性 — 範本設定為自訂（基礎元件）](/help/forms/assets/dor-custom-template-foundation-components.png)

>[!ENDTABS]

最適化表單現在會在產生記錄檔案時使用自訂範本。

## 驗證自訂範本 {#verify-customized-template}

若要確認自訂範本是否已正確套用：

1. 提交最適化表單的測試專案。
1. 產生記錄檔案。
1. 確認產生的PDF可反映您的自訂內容，包括標誌、字型、版面配置變更和其他品牌元素。

## 疑難排解 {#troubleshooting}

| 問題 | 解決方法 |
|---|---|
| 自訂範本未上傳。 | 請確定XDP檔案有效且未損毀。 確認您擁有將檔案上傳至AEM Forms的必要許可權。 |
| 自訂不會出現在產生的記錄檔案中。 | 確認您在表單屬性的&#x200B;**[!UICONTROL 記錄檔案範本組態]**&#x200B;區段中選取了正確的自訂範本。 |
| 產生的PDF中的版面配置或格式問題。 | 確認Adobe Forms Designer中的自訂遵循[基本範本慣例](/help/forms/generate-document-of-record-core-components.md#base-template-conventions)。 請確定所有元素都在範本結構內的正確位置。 |

## 另請參閱 {#see-also}

* [產生最適化Forms的記錄檔案（核心元件）](/help/forms/generate-document-of-record-core-components.md)
* [產生最適化Forms （基礎元件）的記錄檔案](/help/forms/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)
* [記錄檔案的基礎範本](/help/forms/generate-document-of-record-core-components.md#base-template-of-a-document-of-record)
* [自訂記錄檔案中的品牌資訊](/help/forms/generate-document-of-record-core-components.md#customize-the-branding-information-in-document-of-record)
