# 圖書借閱清單展示 (BooksListView)

這是一個基於 C# Windows Forms 開發的簡單應用程式，主要用來示範如何操作 `ListView` 控制項。程式內建了經典文學書籍資料，並實作了資料展示、檢視模式切換以及簡單的模擬借書功能。

## ✨ 核心功能

* **書籍資料展示**：在程式載入時，自動將內建的書籍陣列資料（書名、作者、類別）填入 `ListView` 中，並設定對應的欄位標題與寬度。
* **多種檢視模式切換**：透過下拉式選單 (`ComboBox`)，使用者可以動態切換 `ListView` 的顯示樣式，包含：
    * 大圖示 (LargeIcon)
    * 詳細資料 (Details)
    * 小圖示 (SmallIcon)
    * 清單 (List)
    * 大圖示加詳細資料 (Tile)
* **模擬借閱機制**：
    * 當使用者在 `ListView` 中點選特定書籍時，系統會檢查該書是否已經存在於借閱清單 (`lstBorrow`) 中。
    * 若尚未借閱，系統會跳出訊息方塊 (MessageBox) 進行確認（「確定要借閱嗎?」）。
    * 點選「是」之後，該書籍名稱將會被新增到借閱清單中。

## 🛠️ 使用的控制項 (UI Components)

* `ListView` (`lvwBooks`)：用於展示主要的書籍清單資料。
* `ComboBox` (`cmbView`)：用於選擇與切換 `ListView` 的檢視模式。
* `ListBox` (`lstBorrow`)：用於存放使用者確認借閱的書籍項目。

## ⚠️ 開發注意事項

在處理 `ListView.SelectedIndexChanged` 事件時，當使用者切換選取項目，該事件會觸發兩次（一次取消舊選取，一次套用新選取）。為避免在「取消選取」時發生 `ArgumentOutOfRangeException` (索引超出範圍) 錯誤，程式碼中必須加入選取數量的判斷機制：

```csharp
private void lvwBooks_SelectedIndexChanged(object sender, EventArgs e)
{
    // 必須先確認有選取的項目，才執行讀取
    if (lvwBooks.SelectedIndices.Count > 0)
    {
        string strBookname = b_name[lvwBooks.SelectedIndices[0]];
        // ... 後續借書邏輯 ...
    }
}


<img width="989" height="546" alt="image" src="https://github.com/user-attachments/assets/32316bf4-56f5-4df3-a085-bfff3577a7d0" />
