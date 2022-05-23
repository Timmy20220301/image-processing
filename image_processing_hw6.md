<p align="right">
  影像處理--第6周作業
</p>

##第一題
**題目**：給定數位訊號為：
`x[n]={1,2,3,1,1,1}, n=0,1,...6 `
`h[n]={1,2,2,-1,1}, n=0,1,2,3,4`
**要求**：假設輸入與輸出的樣本數相同，求卷積運算的結果，並用程式驗證。

![img](https://i.imgur.com/NGuvy8Z.jpg)
![img](https://i.imgur.com/kPXwV6S.png)

---

##第二題
**題目**：假設數位影像與濾波器的大小均為 3x3，試求**二維卷積運算**的結果，並用程式驗證
**提示**：from scipy.signal import convolve2d

![img](https://i.imgur.com/WhlY1Tk.jpg)
![img](https://i.imgur.com/n5KCuyq.png)

---

##第三題
**題目**：給定下列 5x5 的數位影像，灰階介於 0~7 之間，試回答下列問題：
(a) 求**影像梯度的大小**
(b) 求**影像梯度的方向**並用程式驗證
**要求**：使用 Sobel 濾波器

![img](https://i.imgur.com/LAabwyT.jpg)

- gx、gy 有反轉後計算
  ![img](https://i.imgur.com/8yW3MXL.png)

---

##第四題
**題目**：利用**拉普拉斯**來顯示西洋棋盤的邊緣影像

**要求**：

![img](https://i.imgur.com/xVmMDwB.png)

---

##第五題
**簡答題**

1. 使用拉普拉斯運算子與 Sobel 梯度運算子在效果上有何不同?
   > 拉普拉斯會模糊邊緣以外的畫面，而 Sobel 可以強調單軸邊緣
