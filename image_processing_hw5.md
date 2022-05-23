<p align="right">
  影像處理--第5周作業
</p>

#第一題
**題目**：選取您喜歡的數位影像，試套用一些強度轉換技術，並輸出結果
**要求**：(a) **影像負片** (b) **Gamma 矯正** (c) **Beta 矯正**

![img](https://i.imgur.com/QvQOZDR.jpg)

---

#第二題
**題目**：給定下列 7x7 的數位影像，灰階介於 0~7 之間，試回答下列問題:
![img](https://i.imgur.com/7QClggR.png)
(a) 求**直方圖**，並以圖形表示之
(b) 求**機率密度函數 PDF**，並以圖形表示之
(c) 求**累積密度函數 CDF**，並以圖形表示之
(d) 若使用**直方圖等化技術**，列出灰階 0~7 對應的輸出值

![img](https://i.imgur.com/SQbq37z.jpg)

---

#第三題
**簡答題**

1. 說明影像增強技術的目的。常用的方法有哪些?

> 影像增強是為了要符合特定需求，通常是希望【增強數位影像的品質】
> 有三種方法，1.強度轉換，2.直方圖處理，3.影像濾波。

###

2. 說明直方圖等化技術(Histogram Equalization)的目的。處理的演算法為何?

> 直方圖等化技術是為了使影像中所有的強度的像素個數均相等。

---

```
###第一題程式碼
import numpy as np
import cv2
import scipy.special as special
from matplotlib import pyplot as plt #資料視覺化套件
from google.colab import drive
from google.colab.patches import cv2_imshow
#讀取影像
drive.mount('/content/drive') #掛載雲端硬碟
img = cv2.imread("/content/drive/MyDrive/Colab Notebooks/picture/Baboon.bmp",-1)

#影像負片
def image_negative(f):
  g = 155 - f
  return g

#Gamma 矯正
def gamma_correction(f, gamma=2.0):
  g = f.copy()
  nr,nc = f.shape[:2]
  c = 255/(255.0**gamma)
  table = np.zeros(256)
  for i in range(256):
    table[i] = round(i**gamma*c,0)
  if f.ndim != 3:
    for x in range(nr):
      for y in range(nc):
        g[x,y] = table[f[x,y]]
  else:
    for x in range(nr):
      for y in range(nc):
        for k in range(3):
          g[x,y,k] = table[f[x,y,k]]
  return g

#Beta矯正
def beta_correction(f, a=2.0, b=2.0):
  g = f.copy()
  nr,nc = f.shape[:2]
  x = np.linspace(0, 1, 256) #在0~1之間產生256個點
  #將不完整brta函數輸出值正規化至0~255
  table = np.round(special.betainc(a, b, x)*255, 0)
  if f.ndim != 3:
    for x in range(nr):
      for y in range(nc):
        g[x,y] = table[f[x,y]]
  else:
    for x in range(nr):
      for y in range(nc):
        for k in range(3):
          g[x,y,k] = table[f[x,y,k]]
  return g

newImg1 = image_negative(img)
newImg2 = gamma_correction(img, 2.0)
newImg3 = beta_correction(img, a=2.0, b=2.0)

images = [img, newImg1, newImg2, newImg3]
titles = ['Original', 'Image Negative', 'gamma_correction(r=2.0)', 'Beta Correction(a=b=2.0)']
plt.figure(figsize=(10,10)) #設定圖片區域大小(寬度及高度)

for i in range(4):
  #顯示1*4的圖片
  plt.subplot(2,2,i+1),plt.imshow(images[i]) #2+2=4
  plt.title(titles[i], fontsize=20, color='r') #顯示圖片標題
  #plt.zticks([]),plt.yticks([]) #不顯示(x,y)軸

plt.tight_layout() #自動調整圖片間距
plt.show()
```
