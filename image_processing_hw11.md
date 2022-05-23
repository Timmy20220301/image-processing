<p align="right">
  影像處理--第11周作業
</p>

##第一題(實戰 3)
**題目**: 選取一張影像(不要與範例重複)，並加入高斯函數作為失真函數(D0 及 w 自行設定)，將失真影像利用維納濾波還原技術取得還原影像，使用 PSNR 評估還原影像的品質如何?
**要求**: (1)顯示失真的影像及 PSNR(2) 顯示還原的影像及 PSNR

![img]()

---

##第二題(實戰 4)
**題目**: 利用影像補繪技術，選取一張影像(不要與範例重複)，將不要的區域去除，並將原圖與去除後的結果顯示

![img](https://i.imgur.com/DS7j0tQ.png)

---

##第三題
**問答題**

1.  試說明影像雜訊的分析方法
    > 訊號雜訊比(Signal-to-Noise)
    > (1)總誤差(Total Error): 不常用
    > (2)均分誤差(Mean-Square Error，MSE)
    > (3)均分根誤差(Root-Mean-Square Error，RMSE)
    > (4)峰值雜訊比(Peak Signal-to-Noise Ratio，PSNR): 理想

###

2. 試解釋反濾波的技術挑戰?
   > 公式: F'(u,v) = F(u,v) + N(u,v)/H(u,v)
   > 問題一：由於 N(u,v) 無法事先得知，因此會影響影像還原的可行性 : 技術上無法克服
   > 問題二：若 H(u,v) 太小，會造成數值過大，從而干擾原始影像 F(u,v) 的資訊 : 可以將 H(u,v) 數值較小的區域設定處理範圍

###

3. 試說明影像補繪技術的使用時機?
   > 想要去除數位影像中不想要的區域的時候。

###

4. 請簡單說明 CH07 影像還原技術的課程重點 (不超過 100 字)
   > 調整數位影像到自己想要的狀態，利用雜訊、反濾波、週期性雜訊、維納濾波、影像補繪，但成效皆由主觀判斷；而影像雜訊分析給我們一個標準去判斷，通常用 PSNR 高低判斷。