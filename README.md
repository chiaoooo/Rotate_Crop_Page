# Rotate_Crop_Page

For 字體課程 138 page 使用 (一部份參考同學程式)  
如果有任何問題可以開 Issue！

## 初始化專案

### 環境 Environment

使用 Python 3.9 (版本 3 以上應該都行...吧)

### 套件 Package

-   使用 requirements.txt 安裝

```cmd
pip install -r requirements.txt
```

-   或使用 pipenv 安裝 (本機需要有 pipenv 套件)

```cmd
# 建立虛擬環境
python -m pipenv shell

# Install requirements
pipenv install -r requirements.txt
```

## 使用說明

### 校正旋轉 page

環境安裝完成後，執行以下步驟：

1. 先修改目標資料夾，改成你的稿紙圖片資料夾位置([程式碼位置](https://github.com/NTUT-kyle/Rotate_Crop_Page/blob/main/s1_rotate_page.py#L140))
2. 執行程式`python s1_rotate_page.py`
3. 等待執行完成
4. 結果可以在`rotated`資料夾中看到

結束後，如果出現`The following is the wrong file`的話，照以下步驟手動修復：

1. 找出出錯檔案後，複製到`rotated`資料夾
2. 使用各種工具把圖片轉正
3. 回到第一步，繼續把其他錯誤的檔案轉正

### 影像處理切割文字

如果旋轉完成，在做以下步驟：

1. 執行程式`python s2_crop_page.py`
2. 先輸入你要從哪個 Page 開始切割，如果是從 `30` 開始的話，就輸出 `30`(初始為 `1`)
3. 再輸入切割到哪個 Page，如果是 `30` 至 `60`，則輸入 `60` (初始為`138`)
4. 等待執行結束
5. 結果會在`1_138`資料夾中看到(如果不是初始值，則是在你設定數字的資料夾中看到)

結束後，如果出現`The following is the wrong file`的話，照以下步驟修復：

1. 找出出錯檔案(可按照[這邊](https://github.com/NTUT-kyle/Rotate_Crop_Page#切割錯誤)來處理)後，複製到`rotated`資料夾
2. 使用各種工具把圖片強化色彩，或去除污漬已讓程式更好辨識
3. 再次執行程式，但開始以及結束 page 輸入錯誤檔案的名稱，如果錯誤檔案是`20.png`，則開始以及結束輸入`20`
    - 如果沒有錯誤的話`20_20`資料夾中的圖片就是最後結果(名稱會與錯誤檔案名稱相同)
    - 如果還是錯誤的話，再從第二步開始！
4. 回到第一步，繼續把其他錯誤檔案修復

## 已知問題

通常`s1_rotate_page.py`不會有太大的問題，但`s2_crop_page.py`就不一樣了！

如果有更好的方法歡迎提出！

### 切割錯誤

如果發現結果中，有切割錯誤的地方，請找到錯誤的 Page 並照著上方步驟修復，可以使用`find_word_page.py`這支程式來找，步驟如下：

1. 在 console 中輸入`python ./find_word_page.py`並執行
2. 輸入錯誤字的 Unicode，假設錯誤的字為`絕`，其 Unicode 為 `5584`(可以看檔名)，那這邊就輸入 `5584`
3. 接下來程式就會幫你找字，會顯示`Found 5584 in page 35`，就代表字在第 35 個 Page，接下來就可以針對 Page 35 做修復或是手動切割等等。

### 單一字元錯誤

如果發現單一字元，有切割錯誤的地方，可以自行使用任何工具切割，並命名為錯誤字元的檔名(U+XXXX)，最後再把錯誤的字元圖片覆蓋成新的。

### 發生 Exception

如果發生 `Exception`，可以把錯誤訊息以及學號發 `Issue`，以便修復！(問題可能出在綠色 HSV 範圍上，因為掃描機掃出來的色彩並不是那麼 OK，所以範圍會因 Page 而異，可以調整 `L161` 的第一個參數看看)
