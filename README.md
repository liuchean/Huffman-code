# Huffman code的核心目的
Huffman code 設計的目的就是在不失真的情況下，減少資料所需的位元數，達到壓縮的效果。

Huffman code的設計原則：
- **出現機率高的數 → 使用較短的編碼**
- **出現機率低的數 → 使用較長的編碼**

透過這樣的設計，整體平均下來，可用比原先字串更短的編碼完整還原原始資料。  
# Outline
This PDF explains the Huffman coding method, followed by an explanation of the Huffman MATLAB code, and concludes with an example problem to demonstrate its application.
# Huffman tree

Construct a Huffman tree
```matlab
for i=1:n-1 
    [q,l]=sort(q); %把向量 q 以從小到大排序，l為排序前的對應位置。
    m(i,:)=[l(1:n-i+1),zeros(1,i-1)]; % 由 l 建構一個m矩陣，紀錄合併時的順序，用於後面的編碼 
    q=[q(1)+q(2),q(3:n),1]; %取最小的兩個機率相加，形成新節點，其餘機率向後移，1用於保持長度。
end
```
# Huffman 編碼流程說明

1. **從最後一層開始回溯**  
   在 Huffman tree 的最後一次合併(第 n-1 層)，將兩個子節點分別指定為 `0` 與 `1`。  
   （分配邏輯：機率較小的節點編碼為 `0`，機率較大的節點編碼為 `1`。）

2. **逐層往回傳遞編碼**  
   透過迴圈回溯 Huffman tree，利用矩陣 `m` 記錄的合併順序，找到每一層的節點位置，並將上一層的編碼複製下來，再依左右子節點分別加上 `0` 或 `1`。

3. **對應回原始符號**  
   在完成所有層級的回溯後，程式使用 `m(1,:)`（初始排序紀錄）將編碼對應回原始輸入的符號順序，輸出最終的 Huffman 編碼結果。

# 簡易編碼流程圖
### ex: p={0.1,0.3,0.05,0.09,0.21,0.25}

### 可以從手畫的流程看出編碼過程
![手繪流程](https://github.com/liuchean/Huffman-code/blob/main/images/123.png)

### 用matlab產生出的結果

![matlab產生出的結果](https://github.com/liuchean/Huffman-code/blob/main/images/matlab_result.png)

由上面兩張圖的計算結果可知，用matlab計算出的結果無誤


