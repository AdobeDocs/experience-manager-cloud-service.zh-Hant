---
title: 設計高效能Forms的最佳作法
description: 瞭解使用AEM Forms建立方便使用、可存取且高效能表單的基本最佳實務。 改善資料品質、使用者體驗和提交成功率。
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 建立Forms的最佳實務

打造絕佳表單不僅僅是技術。 以下說明如何確保您的表單方便使用者使用並達成其目標：

## 設計方便使用者且易於存取的Forms

* **使用清晰、可見的標籤：**&#x200B;每個表單欄位都需要`<label>`。 請勿僅依賴預留位置文字（輸入欄位內的文字），因為當使用者輸入時，預留位置文字會消失，且對協助工具不利。
   * *好：* `<label for="email">Email Address:</label> <input type="email" id="email" placeholder="you@example.com">`
   * *錯誤：* `<input type="email" placeholder="Email Address">`
* **保持簡單：**&#x200B;儘可能使用標準HTML輸入型別(`<input type="date">`、`<input type="tel">`)。 這類元件通常比複雜的自訂Widget提供更好的行動支援和協助工具。
* **邏輯順序和群組：**&#x200B;以使用者認為合理的方式排列欄位。 使用`<fieldset>`和`<legend>`將相關欄位群組在一起。
* **提供清楚的說明：**&#x200B;針對任何可能令人困惑的欄位，提供簡明的說明文字或工具提示。
* **鍵盤導覽：**&#x200B;請確定使用者僅能使用鍵盤（Tab、Shift+Tab、Enter、空格鍵）導覽整個表單。
* **錯誤處理：**&#x200B;讓錯誤變得明顯且容易修正。 在相關欄位旁顯示錯誤訊息，並說明哪些需要修正。

* **確保您的Forms載入快速且可見**

   * **將Forms置於顯眼位置：**&#x200B;如果表單很重要，請確定使用者可以輕鬆看見表單，而不需過度捲動（如果可能的話，請設為「摺頁上方」）。 Adobe的研究顯示，許多表單都隱藏起來，互動性很低。
   * **最佳化Assets：**&#x200B;將表單的任何自訂JavaScript或CSS儘可能的縮小，以確保快速載入時間。 Edge Delivery Services有助於載入基本頁面，但大型表單指令碼仍可能會拖慢速度。

* **負責處理使用者資料**
   * **只詢問您需要的資訊：**&#x200B;您要求的個人識別資訊(PII)越少越好。 每個欄位都是使用者放棄表單的潛在原因。
   * **透明：**&#x200B;請清楚說明&#x200B;*為什麼*&#x200B;您需要特定資訊，以及&#x200B;*如何使用它*。 連結至您的隱私權原則。 這會建立信任。

* **改善使用者體驗：驗證碼替代方案**

   * **重新思考可見的驗證碼：**&#x200B;那些「輸入波浪文字」或「按一下所有紅綠燈」測試可能會讓使用者（尤其是殘障人士）非常沮喪，而且經常會導致高流失率。

* **考慮替代方案：**
   * **Honeypot欄位：**&#x200B;新增只有機器人會填寫的隱藏欄位。 如果其中含有資料，提交內容很可能是垃圾訊息。
   * **以時間為基礎的檢查：**&#x200B;測量提交表單的速度。 提交太快通常是機器人。
   * **隱藏的reCAPTCHA (v3)：**&#x200B;此Google服務會分析背景的使用者行為，而且只有在使用者看起來可疑時才會提出質疑。 這通常是更好的使用者體驗。

## 表單設計有無

| ✅ Do — 為了更好的Forms | ❌不會 — 避免這些專案 |
|----------------------------------------------------------------------|------------------------------------------------------------------|
| 對所有欄位使用可見的`<label>`標籤 | 僅使用預留位置文字，而非適當的標籤 |
| 偏好標準HTML輸入型別（例如`<input type="email">`） | 使用過於複雜的自訂Widget |
| 確保完整的鍵盤導覽 | 提供模糊或遺漏的錯誤訊息 |
| 顯示清除、可操作的錯誤訊息 | 要求過多的個人資料而無正當理由 |
| 僅要求必要資訊 | 使用難以解決的可見驗證碼 |
| 說明資料的使用方式（隱私權資訊或連結） | 在頁面中隱藏深處的表單 |
| 使用隱形或行為驗證碼技術 |                                                                  |
| 讓表單更容易在頁面上找到（顯著位置） |                                                                  |


## 後續步驟

本指南提供搭配AEM Edge Delivery Services使用表單的概觀。 如需特定設定的詳細逐步指示，請參閱Adobe Experience Manager官方檔案：

* [使用Edge Delivery Services Forms進行檔案式製作](/help/edge/docs/forms/tutorial.md)
* [具有Edge Delivery Services Forms的通用編輯器](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [檔案製作(DA)與內嵌內容](https://www.aem.live/developer/da-tutorial)
* [AEM Forms提交服務](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
