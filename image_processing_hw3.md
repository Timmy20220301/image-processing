<p align="right">
  影像處理--第3周作業
</p>

## 第一題

- 題目：設計 Python 程式，使用影像形成模型來取得影像
- 要求：顯示影像

```
import numpy as np
import cv2
from matplotlib import pyplot as plt
from google.colab import drive
from google.colab.patches import cv2_imshow
drive.mount('/content/gdrive')
img = cv2.imread("/content/gdrive/MyDrive/Colab Notebooks/picture/Lenna.jpg",-1)
print(img.shape)
```

```
import numpy as np
from matplotlib import pyplot as plt
nr, nc = 512, 512

x0 = nr//2
y0 = nc//2

illumination = np.zeros([nr, nc], dtype = 'float32')
sigma = 75

for x in range(nr):
  for y in range(nc):
    illumination[x,y] = np.exp( -((x-x0) ** 2 + (y-y0) ** 2) / (2 * sigma * sigma) )
```

```
new_img = img.copy()
for x in range(nr):
  for y in range(nc):
    for k in range(3):
      val = round(illumination[x,y]*img[x,y,k])
      new_img[x,y,k] = np.uint8(val)
images = [img, illumination, new_img]
titles = ['Original', 'Gaussian', 'Image Fromation']
plt.figure(figsize=(15,15))
for i in range(3):
  plt.subplot(1,3,i+1),plt.imshow(images[i])
  plt.title(titles[i])
plt.tight_layout()
plt.show()
```

![img](https://i.imgur.com/wXyl8oJ.png)

---

## 第二題

- 題目： 設計 Python 程式， 選取一張灰階 影像，同時選取不同位元數，顯示結果

```
import numpy as np
import cv2
from matplotlib import pyplot as plt #視覺化資料套件
from google.colab import drive
from google.colab.patches import cv2_imshow
drive.mount('/content/gdrive') #掛載雲端硬碟
img = cv2.imread("/content/gdrive/MyDrive/Colab Notebooks/picture/Lenna.bmp",-1)
print(img.shape)
```

```
def image_quantization(img, bits):
  nr, nc = img.shape[:2] #取出影像的高及寬
  retImg = img.copy() #複製影像
  levels = 2**bits #計算灰階數
  interval = 256/levels #灰階量化質間距
  gray_level_interval = 255/(levels)
  table = np.zeros(256) #建立Look-Up表
  print("原先的Look-Up表內容:{}".format(table))
  for k in range(256):
    for l in range(levels):
      if k >= l * interval and l < (l + 1) * interval:
        table[k] = round(1 * gray_level_interval)
    for x in range(nr):
      for y in range(nc):
        retImg[x,y] = np.uint8(table[img[x,y]])
  return retImg
```

```
img_5bit = image_quantization(img,5)
img_2bit = image_quantization(img,2)
images = [img, img_5bit, img_2bit]
titles = ['Original', 'QZ 5bits', 'QZ 2bits']
plt.figure(figsize=(25,15)) #設定圖片區域大小
for i in range(3):
  #顯示1(row)3(column)的圖片
  plt.subplot(1,3,i+1),plt.imshow(images[i], 'gray')
  plt.title(titles[i], fontsize=20, color='r')
  plt.xticks([]),plt.yticks([])#不顯示(x,y)軸
plt.tight_layout() #自動調整圖片間距
plt.show()
```

![img](https://i.imgur.com/tZQPNCs.png)

---

## 第三題

- 簡答題 : 試解釋 Nyquist-Shammon 取樣定理?試解釋何謂混疊 (Aliasing) 現象

```
1.取樣是將一個訊號（例如時間或空間上連續的函式）轉換為數位序列（時間或空間上離散的函式）的過程；
2.混疊是指取樣訊號被還原成連續訊號時產生彼此交疊而失真的現象。
3.只要離散系統的奈奎斯特頻率高於被採樣訊號的最高頻率或帶寬，就可以避免混疊現象。
```
