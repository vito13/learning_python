# 基本窗口

## 加载图片、显示、保存、创建窗口、销毁窗口

```
import cv2
img = cv2.imread('lean.jpg', -1)
cv2.namedWindow('image')
cv2.imshow('image', img)
cv2.waitKey(0)
cv2.imwrite('lean2.jpg', img)
cv2.destroyAllWindows()
```

## shape、size、dtype

- shape：行、列、通道数
- size：行*列*通道数
- dtype：像素点的数据类型

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
print(dst.shape, dst.size, dst.dtype)
```

## 默认色彩顺序

原始图像，默认是 BGR 格式（OpenCV 的默认色彩顺序）。

# 图形处理

## 创建随机灰度图、彩色图

```
m = np.random.randint(10, 99, size=(256, 256), dtype='uint8')
m = np.random.randint(0, 256, size=[256, 256,3], dtype='uint8')
```

## 创建8通道图

```
每个通道保存一个 2 的幂次,实质为8个二进制位
x[:,:,0] = 1
x[:,:,1] = 2
x[:,:,7] = 128
换句话说，x[:,:,i] 对应第 i 位的权值。

x = np.zeros((r, c, 8), dtype='uint8')
for i in range(8):
    x[:,:,i] = 2**i
```

## 读写像素

### 数组方式（逐像素）

```
img = cv2.imread('lean.jpg', -1)
cv2.namedWindow('image')
cv2.imshow('image', img)

for i in range(10, 100):
    for j in range(80, 100):
        img[i,j]=255
cv2.imshow('after', img)
cv2.waitKey(0)
```

### item与itemset（逐像素）

```
m = np.random.randint(10, 99, size=(256, 256), dtype='uint8')
print(m.item(3,2))
m.itemset((3,2), 0)
print(m.item(3,2))
cv2.waitKey(0)
```

```
for i in range(0, 100):
    for j in range(100, 200):
        for k in range(0, 3):
            m.itemset((i,j,k), 128)
```

### ROI（即切片、整片的改）

- m[:,:,0] = 255, B通道，设置为蓝
- m[:,:,1] = 255，G通道，设置为绿
- m[:,:,2] = 255，R通道，设置为红

```
m = np.zeros((300,300,3), dtype="uint8")
# 设置50-100行为绿色
m[50:100,:,1] = 255
# 设置100-200列为红色
m[:,100:200,2] = 255
cv2.imshow("Original", m)
```

```
img = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
# 原图
cv2.imshow('image1', img)
# 局部
cv2.imshow('image2', img[0:150, 0:150])
# 更改原图的局部
img[0:150, 0:150] = np.random.randint(0, 256, size=[150, 150, 3], dtype='uint8')
cv2.imshow('image3', img)
cv2.waitKey(0)
```

### 局部的复制

```
src = np.random.randint(0, 256, size=[256, 256,3], dtype='uint8')
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
dst[0:150, 0:150] = src[0:150, 0:150]
cv2.imshow('image', dst)
cv2.waitKey(0)
```

### 拆分通道（切片方式）、改通道值

取3个通道值、修改B通道

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
b = dst[:,:,0]
g = dst[:,:,1]
r = dst[:,:,2]

cv2.imshow('b', b)
cv2.imshow('g', g)
cv2.imshow('r', r)
dst[:,:,0] = 0
cv2.imshow('img', dst)
```

### 拆分通道（split）、合并通道

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
b, g, r = cv2.split(dst)
cv2.imshow('bgr', cv2.merge((b, g, r)))
cv2.imshow('rgb', cv2.merge((r, g, g)))
cv2.waitKey(0)
```

## 运算

### 加法+、add（变亮）

- add： 超过255则等于255（图像变亮）
- +： 超过255则取模（变暗）
- 可以数组+数组，也可以数字+数组

```
m1 = np.random.randint(0, 256, size=(3, 3), dtype='uint8')
m2 = np.random.randint(0, 256, size=(3, 3), dtype='uint8')
print(m1+m2)
print(cv2.add(m1, m2))
print(cv2.add(m1, 100))
```

### 加权（alpha混合）

类似alpha混合，分别对2个src进行浮点设置，权重值通常为0，其实三个数都可以随意

```
rc = cv2.imread('rc.jpg', -1)
img = cv2.imread('lean.jpg', -1)
r = cv2.addWeighted(img, 0.1, rc, 0.9, 0)
cv2.imshow('bgr', r)
```

### 按位与（alpha测试）

mask上像素为255即白全1，则src通过，否则非全1则失败

- 一张图与mask

```
img = cv2.imread('lean.jpg', -1)
mask = np.zeros(img.shape, dtype="uint8")
mask[100:200, 100:200] = 255
c = cv2.bitwise_and(img, mask)
cv2.imshow('bgr', c)
cv2.waitKey(0)
```

- 2张图与mask，2张图按位与然后再mask测试

```
img = cv2.imread('lean.jpg', 1)
w,h,c=img.shape
mask = np.zeros((w,h), dtype="uint8")
mask[100:200, 100:200] = 255
img2 = cv2.imread('rc.jpg', 1)
c = cv2.bitwise_and(img, img2, mask=mask)
cv2.imshow('bgr', c)
```

### 按位或、按位非、按位异或

- bitwise_or
- bitwise_not
- bitwise_xor，常用于图片的加密解密，因为异或（XOR）运算是可逆的：如果 A⊕K=B，那么 B⊕K=A。

```
img = cv2.imread('lena.jpg', 0)
cv2.imshow('lena', img)
r, c = img.shape
k = np.random.randint(0, 256, size=(r, c), dtype='uint8')
enc=cv2.bitwise_xor(img, k)
dec=cv2.bitwise_xor(enc, k)
cv2.imshow('2', k)
cv2.imshow('3', enc)
cv2.imshow('4', dec)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

### 位平面

255是8个二进制位，所以可分成8个位平面（二维数组）

```
import cv2
import numpy as np

# 1. 读取灰度图
img = cv2.imread('lena.jpg', 0)
cv2.imshow('lena', img)
r, c = img.shape
# 创建提取矩阵，因为灰度图是8位，所以8张
x = np.zeros((r, c,8), dtype='uint8')
for i in range(8):
    # 设置提取矩阵的值
    x[:,:,i] = 2**i

# 创建位平面8个
result =np.zeros((r,c,8), dtype='uint8')
for i in range(8):
    # 提取位平面，2**i是对应位平面的掩码，与图片按位或，得到位平面
    result[:, :, i] = cv2.bitwise_and(img, 2**i)
    # 阈值处理、将大于0的点改为真、否则为假，真的改为白色，用于显示
    # mask是二维数组，内容是T、F
    mask = result[:, :, i] > 0
    result[mask, i] = 255
    cv2.imshow(f'Bit plane {i}', result[:, :, i])


cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 数字水印

即将第0位平面替换为同尺寸的二值图

```
import cv2
import numpy as np

# 注意2张图要同尺寸
lena = cv2.imread('lena.jpg', 0)
watermark=cv2.imread("watermark.png", 0)
# 将水印图所有非零像素都设为1,即将其二值化（把灰度水印变为黑白掩码）。
w=watermark[:,:]>0
watermark[w]=1

# 创建矩阵，每个像素值都是 254（即二进制 11111110）。
r,c=lena.shape
t254=np.ones((r,c),dtype=np.uint8)*254
# 关键的“清零最低有效位（LSB）”操作。
lenah7=cv2.bitwise_and(lena,t254)
# 水印嵌入到最低位。每个像素的最低位上写入水印位（0 或 1）。
e=cv2.bitwise_or(lenah7,watermark)

# 提取嵌入后的图像 e 的最低有效位，即“取出”隐藏在图像里的水印。
t1=np.ones((r,c),dtype=np.uint8)
wm=cv2.bitwise_and(e,t1)
# 把提取出的水印放大到可视化范围（0 → 黑，255 → 白）。
w=wm[:,:]>0
wm[w]=255

cv2.imshow('lena', lena)
cv2.imshow('watermark', watermark*255)
cv2.imshow('e', e)
cv2.imshow('wm', wm)
cv2.waitKey(0)
```

### 打码与解码

```
import cv2
import numpy as np
#读取原始载体图像
lena=cv2.imread("lena.jpg",0)
#读取原始载体图像的shape值
r,c=lena.shape

# 掩码矩阵，用于指定“要打码的区域”。全部初始化为 0（黑色）；
# 中间 mask区域设为 1，对应 Lena 的脸部。
mask=np.zeros((r,c),dtype=np.uint8)
mask[110:200,125:175]=1
cv2.imshow("lena",lena)
cv2.imshow("mask",mask*255)


#随机矩阵作为密钥
key=np.random.randint(0,256,size=[r,c],dtype=np.uint8)
cv2.imshow("key",key)
#============获取打码脸============
# 整张图像都与密钥异或，得到加密后的图像。
lenaXorKey=cv2.bitwise_xor(lena,key)
cv2.imshow("lenaXorKey",lenaXorKey)
# 提取出“加密图像中属于脸部的部分”（其余区域清零置黑）。
encryptFace=cv2.bitwise_and(lenaXorKey,mask*255)
cv2.imshow("encryptFace",encryptFace)

#清除原始图像中的脸部（即只保留身体、背景部分）。
# 1-mask是对二值内容进行取反，即1变0，0变1
noFace1=cv2.bitwise_and(lena,(1-mask)*255)
cv2.imshow("1-mask",(1-mask)*255)
cv2.imshow("noFace1",noFace1)

#把加密的脸（encryptFace）加回背景部分（noFace1），
# 得到被打码的 Lena 图像（脸部是加密的）。
maskFace=encryptFace+noFace1
cv2.imshow("maskFace",maskFace)
cv2.waitKey()
cv2.destroyAllWindows()

#============将打码脸解码============
cv2.imshow("maskFace",maskFace)
#将脸部打码的lena与密钥key异或，脸部复原了，但其余部分会变为打码
extractOriginal=cv2.bitwise_xor(maskFace,key)
cv2.imshow("extractOriginal",extractOriginal)

#提取出解码后的脸部。（其余区域清零置黑）。
extractFace=cv2.bitwise_and(extractOriginal,mask*255)
cv2.imshow("extractFace",extractFace)

# 提取图像中不包含脸的部分。
noFace2=cv2.bitwise_and(maskFace,(1-mask)*255)
cv2.imshow("noFace2",noFace2)

# 将解码出的脸与背景部分重新合并，得到完全复原的 Lena。
extractLena=noFace2+extractFace
cv2.imshow("extractLena",extractLena)

cv2.waitKey()
cv2.destroyAllWindows()
```

## 色彩空间

### 转换函数 cvtColor

```
import cv2
import numpy as np
img=np.random.randint(0,256,size=[2,4,3],dtype=np.uint8)
rgb=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
bgr=cv2.cvtColor(rgb,cv2.COLOR_RGB2BGR)
print("img=\n",img)
print("rgb=\n",rgb)
print("bgr=\n",bgr)
```

```
import cv2
import numpy as np
lena=cv2.imread("lena.jpg")
rgb = cv2.cvtColor(lena, cv2.COLOR_BGR2RGB)
cv2.imshow("lena",lena)
cv2.imshow("rgb",rgb)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 颜色识别与分离 inRange

- 把图像从 BGR 空间转换到 HSV 空间，再通过设定颜色范围提取蓝、绿、红等区
- inRange用于检测点值是否再指定范围内，并返回二维结果作为mask
- 再使用bitwise_and对mask提取区域

```
import cv2
import numpy as np
opencv=cv2.imread("opencv.jpg")
hsv = cv2.cvtColor(opencv, cv2.COLOR_BGR2HSV)
cv2.imshow('opencv',opencv)
#=============指定蓝色值的范围=============
minBlue = np.array([110,50,50])
maxBlue = np.array([130,255,255])
#生成一个二值掩码mask,落在蓝色范围内的像素值为 255,其他为 0。
mask = cv2.inRange(hsv, minBlue, maxBlue)
#对原图做“按位与”，只保留蓝色区域（其余变黑）。
blue = cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('blue',blue)
#=============指定绿色值的范围=============
minGreen = np.array([50,50,50])
maxGreen = np.array([70,255,255])
#确定绿色区域
mask = cv2.inRange(hsv, minGreen, maxGreen)
#通过掩码控制的按位与，锁定绿色区域
green = cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('green',green)
#=============指定红色值的范围=============
minRed = np.array([0,50,50])
maxRed = np.array([30,255,255])
#确定红色区域
mask = cv2.inRange(hsv, minRed, maxRed)
#通过掩码控制的按位与，锁定红色区域
red= cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('red',red)
cv2.waitKey()
cv2.destroyAllWindows()
```