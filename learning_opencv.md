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

## 坐标系

OpenCV 的坐标系以左上为原点，x 向右增大，y 向下增大

## 边缘、轮廓

- 边缘：不连续的，可能是一段一段的
- 轮廓：连续的，可以用于后续计算的

## 默认色彩顺序

原始图像，默认是 BGR 格式（OpenCV 的默认色彩顺序）。

## 自动灰度导入，后期转换成灰度

- imread的末尾参数使用0，即使彩色也按照灰度图导入
- gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)

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

## 通道

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

```
import cv2
img=cv2.imread("barbara.bmp")
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv)
v[:,:]=255
newHSV=cv2.merge([h,s,v])
art = cv2.cvtColor(newHSV, cv2.COLOR_HSV2BGR)
cv2.imshow("img",img)
cv2.imshow("art",art)
cv2.waitKey()
cv2.destroyAllWindows()
```

### alpha通道

运行时看不出来，保存后看文件才会有效果。。。

```
import cv2
img=cv2.imread("lenacolor.png")
bgra = cv2.cvtColor(img, cv2.COLOR_BGR2BGRA)
b,g,r,a=cv2.split(bgra)
a[:,:]=125
bgra125=cv2.merge([b,g,r,a])
a[:,:]=0
bgra0=cv2.merge([b,g,r,a])
cv2.imshow("img",img)
cv2.imshow("bgra",bgra)
cv2.imshow("bgra125",bgra125)
cv2.imshow("bgra0",bgra0)
cv2.waitKey()
cv2.destroyAllWindows()
cv2.imwrite("bgra.png", bgra)
cv2.imwrite("bgra125.png", bgra125)
cv2.imwrite("bgra0.png", bgra0)
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

### 按位与（掩码、alpha测试）

src在mask相同位置上为白色（像素为255、即1）则通过，否则不通过

- 构造掩码图

```
import cv2
import numpy as np
mask=np.zeros([600,600],np.uint8)
mask[200:400,200:400]=255
cv2.imshow('mask',mask)
cv2.waitKey()
cv2.destroyAllWindows()
```

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

### 阈值筛选 inRange

#### 颜色识别与分离

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

### 标记肤色

- 可以使用“&”组合2个二值mask

```
import cv2
img=cv2.imread("lesson2.jpg")

# 分别得到三个单通道图像：
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv)

# 保留 色相值在 [5,170] 之间的区域。
# 过滤掉极端的红、紫之类的部分。
minHue=5
maxHue=170
hueMask=cv2.inRange(h, minHue, maxHue)

# 保留饱和度在 [25,166] 之间的区域；
# 饱和度太低的区域（灰度、阴影）或太高的区域（过曝）都会被过滤。
minSat=25
maxSat=166
satMask = cv2.inRange(s, minSat, maxSat)

# 用 按位与运算 (&) 得到综合掩膜；
# 只有同时满足色相范围 和 饱和度范围的像素才会保留；
# 结果是一个二值图像（mask）。
mask = hueMask & satMask
roi = cv2.bitwise_and(img,img, mask= mask)
cv2.imshow("img",img)
cv2.imshow("ROI",roi)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 几何变换

## 缩放 resize

- 通过绝对宽高设置

```
import cv2
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
size=(int(cols*0.9),int(rows*0.5))
rst=cv2.resize(img,size)
print("img.shape=",img.shape)
print("rst.shape=",rst.shape)
cv2.imshow("img",img)
cv2.imshow("rst",rst)
cv2.waitKey(0)
```

- 通过比例设置

```
import cv2
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
rst=cv2.resize(img,None,fx=2,fy=0.5)
print("img.shape=",img.shape)
print("rst.shape=",rst.shape)
cv2.imshow("img",img)
cv2.imshow("rst",rst)
cv2.waitKey(0)
```

## 翻转 flip

- 0：上下
- 1：左右
- -1: 上下+左右

```
img=cv2.imread("lena.bmp")
x=cv2.flip(img,0)
y=cv2.flip(img,1)
xy=cv2.flip(img,-1)
cv2.imshow("img",img)
cv2.imshow("x",x)
cv2.imshow("y",y)
cv2.imshow("xy",xy)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 仿射 warpAffine

仿射变换（Affine Transformation），也就是在不破坏平行线关系的前提下，对图像进行平移、旋转、缩放、错切等组合变换。

### 平移

通过float32创建矩阵，指定xy位移

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
height,width=img.shape[:2]
x=50
y=100
M = np.float32([[1, 0, x], [0, 1, y]])
move=cv2.warpAffine(img,M,(width,height))
cv2.imshow("original",img)
cv2.imshow("move",move)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 旋转

使用getRotationMatrix2D创建矩阵，指定旋转中心、角度与缩放

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
height,width=img.shape[:2]
M=cv2.getRotationMatrix2D((width/2,height/2),45,0.6)
rotate=cv2.warpAffine(img,M,(width,height))
cv2.imshow("original",img)
cv2.imshow("rotation",rotate)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 错切

从3个点变道3个点，但要保持对边的平行性

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
rows,cols,ch=img.shape

# 这是原图像上的三个点：
# 左上角 → (0, 0)
# 右上角 → (cols-1, 0)
# 左下角 → (0, rows-1)
# 在图像中选三个不共线的点，用于定义原始三角形区域。
p1=np.float32([[0,0],[cols-1,0],[0,rows-1]])

# 变换后三角形顶点要映射到的新位置。
# 第1个点：移到了稍微下方；
# 第2个点：往左下方倾斜；
# 第3个点：往右上方偏移。
# 通过改变这三个目标点的位置，可以控制图像的旋转、拉伸或倾斜。
p2=np.float32([[0,rows*0.33],[cols*0.85,rows*0.25],[cols*0.15,rows*0.7]])

# 计算仿射变换矩阵
M=cv2.getAffineTransform(p1,p2)

dst=cv2.warpAffine(img,M,(cols,rows))
cv2.imshow("origianl",img)
cv2.imshow("result",dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 透视 warpPerspective

从4个点变到另外4个点，包含仿射的效果

```

import cv2
import numpy as np
img=cv2.imread('demo.bmp')
rows,cols=img.shape[:2]
print(rows,cols)
# src：定义平行四边形的四个点
pts1 = np.float32([[150,50],[400,50],[60,450],[310,450]])
# dst：定义一个矩形
pts2 = np.float32([[50+100,50],[rows-50-100,50],[50,cols-50],[rows-50,cols-50]])
# 计算3×3 透视变换矩阵，进行透视变换
M=cv2.getPerspectiveTransform(pts1,pts2)
dst=cv2.warpPerspective(img,M,(cols,rows))

cv2.imshow("img",img)
cv2.imshow("dst",dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 重映射 remap

- 最强的的存在，可以实现上面的所有变换，相当于告诉 OpenCV：“输出图像上第 (i, j) 个像素，要从原图的 (mapx[i,j], mapy[i,j]) 位置取颜色，然后 OpenCV 根据这两个映射表自动完成插值采样和生成新图
- mapx[i,j], mapy[i,j]分别保存每个点各自的x、 y新位置

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
mapx = np.zeros(img.shape[:2],np.float32)
mapy = np.zeros(img.shape[:2],np.float32)
for i in range(rows):
    for j in range(cols):
# 复制
#        mapx.itemset((i, j), j)
#        mapy.itemset((i, j), i)
# 上下翻转
#        mapx.itemset((i,j),j)
#        mapy.itemset((i,j),rows-1-i)
# 左右翻转
#        mapx.itemset((i, j), cols - 1 - j)
#        mapy.itemset((i, j), i)
# 上下左右都翻转
#        mapx.itemset((i, j), cols - 1 - j)
#        mapy.itemset((i, j), rows - 1 - i)
# 行列互换（旋转90度的效果）
#        mapx.itemset((i, j), i)
#        mapy.itemset((i, j), j)
# 缩放
        if 0.25 * cols < i < 0.75 * cols and 0.25 * rows < j < 0.75 * rows:
            mapx.itemset((i, j), 2 * (j - cols * 0.25) + 0.5)
            mapy.itemset((i, j), 2 * (i - rows * 0.25) + 0.5)
        else:
            mapx.itemset((i, j), 0)
            mapy.itemset((i, j), 0)
rst=cv2.remap(img,mapx,mapy,cv2.INTER_LINEAR)
cv2.imshow("original",img)
cv2.imshow("result",rst)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 阈值处理（二值化）

一般要求输入 灰度图像（单通道），而不是彩色图。若直接传入彩色图像，它会对每个通道分别进行阈值处理。

## 全局固定阈值 threshold

所有像素都使用同一个阈值进行二值化。适合光照均匀的图像，若图像光照不均，这种方式常常效果不理想。

- cv2.THRESH_BINARY	像素 >127 → 255；否则 → 0	二值化图，大于阈值→白，否则→黑
- cv2.THRESH_BINARY_INV	像素 >127 → 0；否则 → 255	反转二值图
- cv2.THRESH_TRUNC	像素 >127 → 127；否则保持原值	截断亮度
- cv2.THRESH_TOZERO	像素 >127 → 保持原值；否则 → 0	保留亮的部分
- cv2.THRESH_TOZERO_INV	像素 >127 → 0；否则保持原值	保留暗的部分

```
import cv2
import numpy as np
img=cv2.imread("lena.bmp")
# t：实际使用的阈值（这里等于 127）
t,THRESH_BINARY=cv2.threshold(img,127,255,cv2.THRESH_BINARY)
t,THRESH_BINARY_INV=cv2.threshold(img,127,255,cv2.THRESH_BINARY_INV)
t,THRESH_TRUNC=cv2.threshold(img,127,255,cv2.THRESH_TRUNC)
t,THRESH_TOZERO_INV=cv2.threshold(img,127,255,cv2.THRESH_TOZERO_INV)
t,THRESH_TOZERO=cv2.threshold(img,127,255,cv2.THRESH_TOZERO)
cv2.imshow("img",img)
cv2.imshow("THRESH_BINARY",THRESH_BINARY)
cv2.imshow("THRESH_BINARY_INV",THRESH_BINARY_INV)
cv2.imshow("THRESH_TRUNC",THRESH_TRUNC)
cv2.imshow("THRESH_TOZERO_INV",THRESH_TOZERO_INV)
cv2.imshow("THRESH_TOZERO",THRESH_TOZERO)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自动阈值 Otsu

- Otsu 自动找到“最合适的分界线”，不需要手动设定阈值。(计算图像灰度直方图；尝试不同阈值；找到使类间方差（前景与背景分布差异）最大的那个阈值；自动使用该阈值进行二值化。)

```
import cv2
import numpy as np
img=cv2.imread("tiffany.bmp",0)
t1,thd=cv2.threshold(img,127,255,cv2.THRESH_BINARY)

使用THRESH_OTSU时候第二个参数写成0
t2,otsu=cv2.threshold(img,0,255,cv2.THRESH_BINARY+cv2.THRESH_OTSU)
cv2.imshow("img",img)
cv2.imshow("thd",thd)
cv2.imshow("otus",otsu)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自适应阈值 adaptiveThreshold

- ADAPTIVE_THRESH_MEAN_C 均值自适应，适合光照不均的图像，自动适应亮度变化，计算稍慢
- ADAPTIVE_THRESH_GAUSSIAN_C 高斯自适应，适合含噪图像，平滑效果好，参数需调试

```
img=cv2.imread("computer.jpg",0)
t1,thd=cv2.threshold(img,127,255,cv2.THRESH_BINARY)

末尾2个参数的作用：
邻域块大小（blockSize）：每个像素以其周围 3×3 区域计算局部阈值。应为奇数且大于1。如3、5、7
C常数：从计算出的局部平均（或高斯加权平均）中减去该常数，微调阈值。

athdMEAN=cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY,3,5)
athdGAUS=cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_GAUSSIAN_C,cv2.THRESH_BINARY,3,5)
cv2.imshow("img",img)
cv2.imshow("thd",thd)
cv2.imshow("athdMEAN",athdMEAN)
cv2.imshow("athdGAUS",athdGAUS)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 滤波

## 基本概念与卷积核（Convolution Kernel）

- 是图像处理中最常见的操作之一，用于去噪声、平滑图像或增强边缘。用像素邻域的加权结果替代当前像素值。

- 卷积核是一块带有权值的小矩阵，通过在图像上滑动并与像素区域做加权计算，控制图像的模糊、锐化、边缘检测等效果。本质上就是图像处理的运算规则模板。

- 卷积越大、时间越久、更平滑、但越失真

## 种类对比

| 滤波类型                           | OpenCV函数                                              | 原理                  | 主要参数                            | 优点            | 缺点          | 典型用途           |
| ------------------------------ | ----------------------------------------------------- | ------------------- | ------------------------------- | ------------- | ----------- | -------------- |
| **1️⃣ 均值滤波（Mean Filter）**      | `cv2.blur(src, ksize)`                                | 用邻域像素的平均值替代中心像素     | `ksize=(m,n)` 滤波核大小             | 简单快速，能去除随机噪声  | 模糊边缘，细节丢失   | 图像平滑、去随机噪声     |
| **2️⃣ 方框滤波（Box Filter）**       | `cv2.boxFilter(src, ddepth, ksize, normalize)`        | 类似均值滤波，可控制是否归一化     | `normalize=True/False`          | 控制灵活，可实现加权或求和 | 不归一化会导致亮度偏移 | 特殊加权或亮度操作      |
| **3️⃣ 高斯滤波（Gaussian Filter）**  | `cv2.GaussianBlur(src, ksize, sigmaX)`                | 按高斯分布加权平均，中心权重大     | `ksize`, `sigmaX`, `sigmaY`     | 平滑自然，边缘保留较好   | 计算略慢        | 去高斯噪声、边缘检测前预处理 |
| **4️⃣ 中值滤波（Median Filter）**    | `cv2.medianBlur(src, ksize)`                          | 用邻域像素的中间值替代中心像素     | `ksize`（奇数）                     | 去椒盐噪声能力强，保边缘好 | 对高斯噪声效果一般   | 去椒盐噪声          |
| **5️⃣ 双边滤波（Bilateral Filter）** | `cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace)` | 综合考虑空间距离与颜色相似度的加权平均 | `d`, `sigmaColor`, `sigmaSpace` | 平滑同时保留边缘，效果自然 | 计算量大，速度慢    | 人像磨皮、摄影后期平滑    |
| **6️⃣ 自定义卷积滤波（filter2D）**      | `cv2.filter2D(src, ddepth, kernel)`                   | 通用卷积操作，可自定义任意核      | `kernel`（矩阵）                    | 灵活强大，可实现任意滤波  | 需手动设计卷积核    | 锐化、模糊、边缘检测等    |

## 图像效果直观总结

| 滤波类型       | 视觉效果             |
| ---------- | ---------------- |
| 均值滤波       | 整体模糊，边缘变钝        |
| 方框滤波（不归一化） | 图像亮度变高           |
| 高斯滤波       | 平滑自然，边缘略保留       |
| 中值滤波       | 去除黑白点噪声效果最佳      |
| 双边滤波       | 平滑又保留边缘（最自然）     |
| filter2D   | 效果取决于卷积核，可实现多种滤波 |

## 如何选择滤波方法

| 场景            | 推荐滤波方法                |
| ------------- | --------------------- |
| 图像噪声较多，无需保留边缘 | **均值滤波 / 高斯滤波**       |
| 图像有“椒盐噪声”     | **中值滤波**              |
| 想平滑但保留边缘（如人脸） | **双边滤波**              |
| 想实验自定义效果      | **filter2D**          |
| 想控制亮度         | **方框滤波（normalize=0）** |

## 总结一句话

🟦 均值滤波：平均去噪，模糊边缘

🟩 方框滤波：可控制是否归一化

🟧 高斯滤波：平滑柔和，边缘较清晰

🟥 中值滤波：去椒盐噪声的首选

🟪 双边滤波：平滑 + 保边缘 = 最自然

⚙️ filter2D：万能卷积器，任意自定义滤波核

## 均值滤波（Mean Filtering）

- 是线性平滑滤波，用于去除图像中的随机噪声。用矩阵在图像上滑动，将矩阵覆盖的所有像素的平均值作为中心像素的新值。

- 权值全部相等(矩阵元素都相同)

```
o=cv2.imread("lenaNoise.png")
r5=cv2.blur(o,(5,5))
r30=cv2.blur(o,(30,30))
cv2.imshow("original",o)
cv2.imshow("result5",r5)
cv2.imshow("result30",r30)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 方框滤波（box Filter）

- 如果参数 normalize（归一化）=True（默认）结果是求平均值（即均值滤波）。
- 否则是求加总值，不除以像素个数。所以亮度会显著增（最大255全白）

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
# r=cv2.boxFilter(o,-1,(5,5))
# r=cv2.boxFilter(o,-1,(5,5),normalize=0)
r=cv2.boxFilter(o,-1,(2,2),normalize=0) 
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 高斯滤波（Gaussian Blur，高斯平滑）

- 高斯滤波是一种加权的平滑滤波，利用“高斯分布”控制权重，是让离中心越近的像素权重越大，离得越远权重越小。 平滑噪声更有效，又能较好地保留图像边缘信息，图像预处理、边缘检测前降噪
- 参数σX：X方向标准差控制模糊程度
- 参数σY：Y方向标准差，一般设为 0，表示与 X 相同

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.GaussianBlur(o,(5,5),0,0)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 中值滤波（Median Filtering）

- 与均值滤波不同，它不会计算平均值，而是取“排序后居中的那个值”。来代替中心像素的值。
- 能有效去除椒盐噪声（即随机出现的黑白点噪声）、对边缘结构的破坏小，平滑效果自然

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.medianBlur(o,3)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 双边滤波（Bilateral Filter）

- 既能平滑图像、又能保留边缘的“高级滤波算法”。人像磨皮（光滑皮肤但保留眼鼻等边缘）
- 只有“距离近”且“颜色相似”的像素才参与平均，边缘两侧颜色差很大的像素不会互相混合，因此边缘可以被保留下来。
- 参数d：像素的邻域范围；
- 参数sigmaColor：控制“颜色差异”敏感度，颜色差异更容易被忽略（模糊更强）
- 参数sigmaSpace：控制“空间距离”敏感度，更远的像素也参与平均（模糊更广）

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.bilateralFilter(o,25,100,100)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 卷积滤波（filter2D）

自定义矩阵进行滤波操作

```
import cv2
import numpy as np
o=cv2.imread("lena.bmp")
kernel = np.ones((9,9),np.float32)/81
r = cv2.filter2D(o,-1,kernel)
cv2.imshow("original",o)
cv2.imshow("filter2D",r)
cv2.waitKey()
cv2.destroyAllWindows(
```

# 形态学操作（Morphological Operation）

## 概念、作用

- 使用kernel（即卷积核、可理解为自定义的刷子）对二值图像、灰度图进行遍历，分析像素局部邻域，从而达到去噪、提取边缘、连接或分离目标、纹理增强、目标检测、工业/医学图像处理。

- Kernel有形状（矩形、十字、椭圆）、大小、执行次数的属性，决定了操作的方向性和强度。

## 总结对比

| 操作                   | 原理          | 效果            | 应用              |
| -------------------- | ----------- | ------------- | --------------- |
| **腐蚀 (Erosion)**     | 白色区域收缩，前景缩小 | 去掉小白噪点，分离物体   | 噪声去除、物体分离       |
| **膨胀 (Dilation)**    | 白色区域扩张，前景增大 | 填补小黑洞，连接白色物体  | 填洞、连接目标         |
| **开运算 (Opening)**    | 先腐蚀再膨胀      | 去除小白噪声，平滑边缘   | 去噪、分离小物体        |
| **闭运算 (Closing)**    | 先膨胀再腐蚀      | 填补小黑洞，平滑边界    | 填洞、连接断裂目标       |
| **形态学梯度 (Gradient)** | 膨胀减去腐蚀      | 提取物体边缘，显示轮廓线  | 边缘检测、轮廓分析       |
| **顶帽变换 (Top-hat)**   | 原图减去开运算     | 提取小亮点，增强局部亮特征 | 亮点检测、高光增强、纹理分析  |
| **黑帽变换 (Black-hat)** | 闭运算减去原图     | 提取小暗点，强化局部阴影  | 暗特征检测、纹理增强、缺陷检测 |



## 腐蚀（Erosion）

- 目标“让白色（前景）区域变小，黑色（背景）区域扩大。”
- 首先定义kernel（是矩阵）用于设置腐蚀的“力度”和“形状（对边缘形态影响不同）”，然后执行erode函数进行腐蚀，iterations腐蚀的重复次数

```
import cv2
import numpy as np
o=cv2.imread("erode.bmp",cv2.IMREAD_UNCHANGED)
kernel = np.ones((9,9),np.uint8)
erosion = cv2.erode(o,kernel,iterations =5)
cv2.imshow("orriginal",o)
cv2.imshow("erosion",erosion)
cv2.waitKey()
cv2.destroyAllWindows()
```


## 膨胀（Dilation）

会让白色前景扩大，用于填补空隙、连接断裂、强化形状，与腐蚀正好相反

```
o=cv2.imread("dilation.bmp",cv2.IMREAD_UNCHANGED)
kernel = np.ones((5,5),np.uint8)
dilation = cv2.dilate(o,kernel,iterations = 9)
cv2.imshow("original",o)
cv2.imshow("dilation", dilation)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 开运算（Opening）

开运算是先腐蚀再膨胀，主要用于去除小白噪声、平滑物体边缘，而不会明显改变主体形状。

```
img1=cv2.imread("opening.bmp")
img2=cv2.imread("opening2.bmp")
k=np.ones((10,10),np.uint8)
r1=cv2.morphologyEx(img1,cv2.MORPH_OPEN,k)
r2=cv2.morphologyEx(img2,cv2.MORPH_OPEN,k)
cv2.imshow("img1",img1)
cv2.imshow("result1",r1)
cv2.imshow("img2",img2)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 闭运算（Closing）

闭运算是先膨胀再腐蚀，主要用于填补小黑洞、连接相邻白区域、平滑边界

```
img1=cv2.imread("closing.bmp")
img2=cv2.imread("closing2.bmp")
k=np.ones((10,10),np.uint8)
r1=cv2.morphologyEx(img1,cv2.MORPH_CLOSE,k,iterations=3)
r2=cv2.morphologyEx(img2,cv2.MORPH_CLOSE,k,iterations=3)
cv2.imshow("img1",img1)
cv2.imshow("result1",r1)
cv2.imshow("img2",img2)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 形态学梯度（Morphological Gradient）

即膨胀减去腐蚀，它的结果是物体的边缘轮廓，常用于边缘检测与目标分割。

```
o=cv2.imread("gradient.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r=cv2.morphologyEx(o,cv2.MORPH_GRADIENT,k)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 顶帽（Top-hat）

原图减去开运算结果，用于提取小而亮的区域（噪声）、增强局部亮细节。

```
o1=cv2.imread("tophat.bmp",cv2.IMREAD_UNCHANGED)
o2=cv2.imread("lena.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r1=cv2.morphologyEx(o1,cv2.MORPH_TOPHAT,k)
r2=cv2.morphologyEx(o2,cv2.MORPH_TOPHAT,k)
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 黑帽（Black-hat）

是闭运算减去原图，用于提取小暗区域、增强局部阴影细节。

```
o1=cv2.imread("blackhat.bmp",cv2.IMREAD_UNCHANGED)
o2=cv2.imread("lena.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r1=cv2.morphologyEx(o1,cv2.MORPH_BLACKHAT,k)
r2=cv2.morphologyEx(o2,cv2.MORPH_BLACKHAT,k)
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自定义核函数

可使用3种形状进行自定义那个核刷子的形状，用于影响刷出来的外观

```
o=cv2.imread("kernel.bmp",cv2.IMREAD_UNCHANGED)
kernel1 = cv2.getStructuringElement(cv2.MORPH_RECT, (59,59))
kernel2 = cv2.getStructuringElement(cv2.MORPH_CROSS,  (59,59))
kernel3 = cv2.getStructuringElement(cv2.MORPH_ELLIPSE,  (59,59))
dst1 = cv2.dilate(o,kernel1)
dst2 = cv2.dilate(o,kernel2)
dst3 = cv2.dilate(o,kernel3)
cv2.imshow("orriginal",o)
cv2.imshow("dst1",dst1)
cv2.imshow("dst2",dst2)
cv2.imshow("dst3",dst3)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 图像梯度计算

## 概念作用

- 求每个像素的灰度变化幅度和方向（如果某个区域灰度变化大即梯度大越亮）
- 是提取边缘和局部结构的重要工具。

## 对比总结

| 算子            | 阶数 | 方向      | 核大小         | 特点               | 优点          | 缺点                  | 典型用途           |
| ------------- | -- | ------- | ----------- | ---------------- | ----------- | ------------------- | -------------- |
| **Sobel**     | 一阶 | X/Y 可分开 | 可调 (3,5,7…) | 计算一阶梯度，强调水平/竖直边缘 | 简单，通用       | 对弱边缘和细节敏感度一般        | 边缘检测、特征提取、图像分割 |
| **Scharr**    | 一阶 | X/Y 可分开 | 固定 3x3，优化权重 | Sobel 升级版，更锐利    | 对细节和弱边缘敏感   | 只能单方向，不支持 dx=1,dy=1 | 边缘检测、细节增强      |
| **Laplacian** | 二阶 | 全方向     | 3x3 或 5x5   | 计算二阶导数，全方向边缘一次提取 | 能一次提取所有方向边缘 | 对噪声敏感               | 边缘检测、图像锐化      |

- Sobel：适合一般边缘检测，可调核大小，简单易用。
- Scharr：对细节边缘更敏感，适合高精度边缘检测。
- Sobel与Scharr可以X/Y 梯度先分别求，再加权合成 → 获得完整边缘图
- Laplacian：一次提取全方向边缘，但噪声敏感，常结合平滑（如高斯模糊）使用。可单独用于全方向边缘检测或锐化

## Sobel

- Sobel 算子 = 边缘检测基础工具
- dx/dy 决定梯度方向 → 决定边缘方向
- addWeighted 合并 → 得到全局边缘
- CV_64F + convertScaleAbs → 保证梯度计算准确且可显示
- ksize=3，下面案例未使用，用于设置核大小3x3

```
# 得到竖线边缘信息，x=1,y=0,求x方向导数
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelx = cv2.Sobel(o,cv2.CV_64F,1,0)
sobelx = cv2.convertScaleAbs(sobelx)   # 转回uint8
cv2.imshow("original",o)
cv2.imshow("x",sobelx)
cv2.waitKey()
cv2.destroyAllWindows()

# 得到横线边缘信息,dx=0, dy=1,求 y 方向导数
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobely = cv2.Sobel(o,cv2.CV_64F,0,1)
sobely = cv2.convertScaleAbs(sobely)
cv2.imshow("original",o)
cv2.imshow("y",sobely)
cv2.waitKey()
cv2.destroyAllWindows()


# 得到交叉点信息, x=1,y=1,同时对x和y求导（二阶混合导数，不是简单的 x+y，非下面案例的加权效果）
# 仅角点或斜交区域亮，点状、不连续，线条不明显
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelxy=cv2.Sobel(o,cv2.CV_64F,1,1)
sobelxy=cv2.convertScaleAbs(sobelxy)
cv2.imshow("original",o)
cv2.imshow("xy",sobelxy)
cv2.waitKey()
cv2.destroyAllWindows()

# X+Y分别计算再addWeighted，水平和竖直边缘都保留，连续完整的边缘线
# 0.5权重保证 x、y 贡献相等,得到综合边缘图
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelx = cv2.Sobel(o,cv2.CV_64F,1,0)
sobely = cv2.Sobel(o,cv2.CV_64F,0,1)
sobelx = cv2.convertScaleAbs(sobelx)   # 转回uint8
sobely = cv2.convertScaleAbs(sobely)
sobelxy =  cv2.addWeighted(sobelx,0.5,sobely,0.5,0)
cv2.imshow("original",o)
cv2.imshow("xy",sobelxy)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Scharr

- Scharr 是 Sobel 的升级版，更精确地计算图像梯度，尤其在边缘较明显或细节复杂时比 Sobel 更敏感


```
import cv2
import numpy as np

# X 方向梯度,得到竖线
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrx = cv2.Scharr(o,cv2.CV_64F,1,0)
scharrx = cv2.convertScaleAbs(scharrx)   # 转回uint8
cv2.imshow("original",o)
cv2.imshow("x",scharrx)
cv2.waitKey()
cv2.destroyAllWindows()

# Y 方向梯度,得到横线
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharry = cv2.Scharr(o,cv2.CV_64F,0,1)
scharry = cv2.convertScaleAbs(scharry)
cv2.imshow("original",o)
cv2.imshow("y",scharry)
cv2.waitKey()
cv2.destroyAllWindows()

# X、Y 加权融合，得到综合边缘图
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrx = cv2.Scharr(o,cv2.CV_64F,1,0)
scharry = cv2.Scharr(o,cv2.CV_64F,0,1)
scharrx = cv2.convertScaleAbs(scharrx)   # 转回uint8
scharry = cv2.convertScaleAbs(scharry)
scharrxy =  cv2.addWeighted(scharrx,0.5,scharry,0.5,0)
cv2.imshow("original",o)
cv2.imshow("xy",scharrxy)
cv2.waitKey()
cv2.destroyAllWindows()

# Scharr 不允许 dx=1,dy=1，因为它是专门优化单方向一阶导数的算子。想要综合边缘，必须 X/Y 分开计算再合并。此处会运行出错
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrxy11=cv2.Scharr(o,cv2.CV_64F,1,1)
cv2.imshow("original",o)
cv2.imshow("xy11",scharrxy11)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Laplacian

Laplacian 是二阶导数算子，直接检测全方向边缘，常用于边缘检测和图像锐化，但噪声敏感，需要结合平滑处理。

```
o = cv2.imread('Laplacian.bmp',cv2.IMREAD_GRAYSCALE)
Laplacian = cv2.Laplacian(o,cv2.CV_64F)
Laplacian = cv2.convertScaleAbs(Laplacian)
cv2.imshow("original",o)
cv2.imshow("Laplacian",Laplacian)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 车道线检测（Canny + 霍夫变换）

## Canny 边缘检测

是一个经典多阶段边缘检测算法，通过高斯滤波去噪平滑、用 Sobel 或 Scharr计算梯度、非极大值抑制和双阈值连接，能在噪声环境中提取精确、连续的全方向边缘（轮廓、形状、纹理）。

- 双阈值 + 边缘连接 的机制：
- threshold1（低阈值）：弱边缘阈值，梯度值低于这个值的像素被认为不是边缘，直接丢弃
- threshold2（高阈值）：强边缘阈值，梯度值高于这个值的像素被认为一定是边缘
- 梯度值在低阈值和高阈值之间：被认为是“弱边缘”，仅保留与强边缘相连部分
- threshold1 决定弱边缘起点，threshold2 决定强边缘，双阈值 + 边缘连接让 Canny 得到干净、连续的边缘。


```
edges = cv2.Canny(gray, 50, 150, apertureSize=3)
50 = 最小阈值
150 = 最大阈值
apertureSize=3 → Sobel 卷积核大小
输出 edges → 二值边缘图
```

```
o=cv2.imread("lena.bmp",cv2.IMREAD_GRAYSCALE)
r1=cv2.Canny(o,128,200)
r2=cv2.Canny(o,32,128)
cv2.imshow("original",o)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 霍夫变换

HoughLinesP 更适合实际应用，因为它直接返回线段端点，不需要延长到无限大，绘制更直观。

| 特性   | HoughLines            | HoughLinesP                         |
| ---- | --------------------- | ----------------------------------- |
| 返回值  | `(rho, theta)` → 无限直线 | `(x1, y1, x2, y2)` → 线段端点           |
| 适用场景 | 需要全图延长直线              | 需要实际线段（如车道、物体边框）                    |
| 处理方式 | 需要计算端点再绘制             | 直接绘制即可                              |
| 控制参数 | 阈值                    | 阈值 + `minLineLength` + `maxLineGap` |


### 直线变换 HoughLines

- 首先使用Canny检测图像中连续、清晰的边缘
- 霍夫直线变换检测直线（将边缘点映射到极坐标空间检测直线，HoughLines检测的是无限延长直线，HoughLinesP返回线段而不是无限延长直线，更实际）

    lines = cv2.HoughLines(edges, 1, np.pi/180, 140)，参数解释：  
    1 → 距离精度 1 像素  
    np.pi/180 → 角度精度 1 度
    140 → 阈值，累加器票数大于 140 才认为是一条直线  
    返回 lines → 每条线的 (rho, theta)  
    rho → 到原点距离  
    theta → 与 x 轴夹角  

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('computer.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(gray,50,150,apertureSize = 3)

# 转 RGB 用于绘制颜色线
orgb=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
oShow=orgb.copy()

lines = cv2.HoughLines(edges,1,np.pi/180,140)

# x0, y0 → 直线在极坐标下的基准点
# (x1,y1),(x2,y2) → 直线两端点，延长很长（1000 像素）确保覆盖整图
# (0,0,255) → 红色直线
# 2 → 线宽
for line in lines:
    rho,theta = line[0]
    a = np.cos(theta)
    b = np.sin(theta)
    x0 = a*rho
    y0 = b*rho
    x1 = int(x0 + 1000*(-b))
    y1 = int(y0 + 1000*(a))
    x2 = int(x0 - 1000*(-b))
    y2 = int(y0 - 1000*(a))
    cv2.line(orgb,(x1,y1),(x2,y2),(0,0,255),2)
plt.subplot(121)
plt.imshow(oShow)
plt.axis('off')
plt.subplot(122)
plt.imshow(orgb)
plt.axis('off')
plt.show()
```

### 概率直线变换 HoughLinesP

- 不同于 HoughLines 返回无限长直线，HoughLinesP 直接返回线段端点 (x1, y1, x2, y2)。所以绘制代码是不同的，不需要再计算极坐标

    lines = cv2.HoughLinesP(edges, 1, np.pi/180, 160, minLineLength=100, maxLineGap=10)

| 参数                  | 含义                         |
| ------------------- | -------------------------- |
| `edges`             | 边缘图像                       |
| `1`                 | 距离分辨率 = 1 像素               |
| `np.pi/180`         | 角度分辨率 = 1 度                |
| `160`               | 阈值，累加器票数 ≥ 160 才认为是直线      |
| `minLineLength=100` | 最短线段长度，短于它会被忽略             |
| `maxLineGap=10`     | 同一条直线上点之间最大间隙，小于它会被连接成一条线段 |

### 霍夫圆环

霍夫圆变换 (Hough Circle Transform) 来检测图像中的圆形

- circles = cv2.HoughCircles(img, cv2.HOUGH_GRADIENT, 1, 300,
                           param1=50, param2=30, minRadius=100, maxRadius=200)

| 参数                   | 含义                |
| -------------------- | ----------------- |
| `img`                | 输入灰度图             |
| `cv2.HOUGH_GRADIENT` | 霍夫梯度法检测圆          |
| `1`                  | 累加器分辨率 = 输入图像分辨率  |
| `300`                | 圆心最小距离（避免重复检测）    |
| `param1=50`          | Canny 高阈值（边缘检测使用） |
| `param2=30`          | 累加器阈值（圆检测灵敏度）     |
| `minRadius=100`      | 最小圆半径             |
| `maxRadius=200`      | 最大圆半径             |

- 输出 circles → 圆的参数 (x_center, y_center, radius)，先通过 np.uint16(np.around(circles)) 转为整数绘制

| 步骤    | 作用                                                        |
| ----- | --------------------------------------------------------- |
| 中值滤波  | 去噪声，提高圆检测准确率                                              |
| 霍夫圆变换 | 检测图像中的圆形，返回圆心和半径                                          |
| 绘制圆   | 可视化检测结果（圆和圆心）                                             |
| 参数调节  | `param1/param2` 控制边缘检测与灵敏度，`minRadius/maxRadius` 控制检测半径范围 |


```
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('chess.jpg',0)
imgo=cv2.imread('chess.jpg',-1)
o=cv2.cvtColor(imgo,cv2.COLOR_BGR2RGB)
oshow=o.copy()
img = cv2.medianBlur(img,5)
circles = cv2.HoughCircles(img,cv2.HOUGH_GRADIENT,1,300,param1=50,param2=30,minRadius=100,maxRadius=200)
circles = np.uint16(np.around(circles))
for i in circles[0,:]:
  cv2.circle(o,(i[0],i[1]),i[2],(255,0,0),12)
  cv2.circle(o,(i[0],i[1]),2,(255,0,0),12)
plt.subplot(121)
plt.imshow(oshow)
plt.axis('off')
plt.subplot(122)
plt.imshow(o)
plt.axis('off')
plt.show()
```

# 轮廓

## 查找（findContours）、绘制（drawContours）

- 彩色转灰度再转二值图后才可查找轮廓
- findContours可以设置检测参数，如RETR_EXTERNAL仅外轮廓（RETR_LIST是所有轮廓），CHAIN_APPROX_SIMPLE是只保留拐点，减少数据量，返回轮廓列表和层级信息
- drawContours是绘制轮廓，可设置颜色，线宽（为-1则绘制为实心的）等，返回绘制后的结果图

```
o = cv2.imread('contours.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_EXTERNAL,
                                             cv2.CHAIN_APPROX_SIMPLE)

# 一次全绘制到一个窗口
o=cv2.drawContours(o,contours,-1,(0,0,255),5)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()

# 分着每个绘制到不同窗口
n=len(contours)
contoursImg=[]
for i in range(n):
    temp=np.zeros(o.shape,np.uint8)
    contoursImg.append(temp)
    contoursImg[i]=cv2.drawContours(
            contoursImg[i],contours,i,(255,255,255),5)
    cv2.imshow("contours[" + str(i)+"]",contoursImg[i])
cv2.waitKey()
cv2.destroyAllWindows()
```


## 抠图案例

- 这段代码用 findContours() 找出物体边界，
- 再用 drawContours() 生成掩膜，
- 最后用 bitwise_and() 从原图中“抠出”目标区域。

```
o = cv2.imread('loc3.jpg')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
mask=np.zeros(o.shape,np.uint8)
mask=cv2.drawContours(mask,contours,-1,(255,255,255),-1)
cv2.imshow("mask" ,mask)
loc=cv2.bitwise_and(o,mask)
cv2.imshow("location" ,loc)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 普通矩 cv2.moments

- 是图像像素灰度值的加权统计量，一种用来描述图像形状、方向、质心、倾斜程度等特征的数学方式，简单理解为图像的几何特征
- 从二值图像中提取出各个轮廓，然后可以得到它们的矩（moments），使用cv2.moments函数返回的是字典
- 轮廓区域面积是字典的m00元素
- 字典的“nuXX”开头的元素是归一化中心矩（Normalized Central Moments），它们与图像的平移、缩放无关，即使图像大小或位置改变，nu值也几乎相同。

```
o = cv2.imread('moments.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
n=len(contours)
contoursImg=[]
for i in range(n):
    temp=np.zeros(image.shape,np.uint8)
    contoursImg.append(temp)
    contoursImg[i]=cv2.drawContours(contoursImg[i],contours,i,255,3)
    cv2.imshow("contours[" + str(i)+"]",contoursImg[i])
print("观察各个轮廓的矩（moments）:")
for i in range(n):
    print("轮廓"+str(i)+"的矩:\n",cv2.moments(contours[i]))
print("观察各个轮廓的面积:")
for i in range(n):
    print("轮廓"+str(i)+"的面积:%d" %cv2.moments(contours[i])['m00'])
cv2.waitKey()
cv2.destroyAllWindows()
```

## Hu不变矩 cv2.HuMoments

- Hu Moments（胡不变矩） 是 7 个数学特征值。把同一个图形放大、旋转、挪动位置，Hu 值几乎不变；因此它常用于“形状匹配”和“物体识别”。

| Hu[i]       | 描述         | 不变性        |
| ----------- | ---------- | ---------- |
| Hu[0]       | 形状的总体方差    | 平移、旋转、缩放不变 |
| Hu[1]       | 图像的对称性     | 同上         |
| Hu[2]~Hu[6] | 更复杂的高阶形状特征 | 同上         |

- 不变矩的Hu[0] 应该等于普通矩的 nu20 + nu02，下面代码进行了验证

```
o1 = cv2.imread('cs1.bmp')
gray = cv2.cvtColor(o1,cv2.COLOR_BGR2GRAY)
HuM1=cv2.HuMoments(cv2.moments(gray)).flatten()
print("cv2.moments(gray)=\n",cv2.moments(gray))
print("\nHuM1=\n",HuM1)
print("\ncv2.moments(gray)['nu20']+cv2.moments(gray)['nu02']=%f+%f=%f\n"
      %(cv2.moments(gray)['nu20'],cv2.moments(gray)['nu02'],
        cv2.moments(gray)['nu20']+cv2.moments(gray)['nu02']))
print("HuM1[0]=",HuM1[0])
print("\nHu[0]-(nu02+nu20)=",
      HuM1[0]-(cv2.moments(gray)['nu20']+cv2.moments(gray)['nu02']))
```

## 形状匹配案例（使用Hu不变矩）

```

import cv2
import numpy as np

o1 = cv2.imread('cs1.bmp')
gray1 = cv2.cvtColor(o1,cv2.COLOR_BGR2GRAY)
HuM1=cv2.HuMoments(cv2.moments(gray1)).flatten()
#----------------计算图像2的Hu矩-------------------
o2 = cv2.imread('cs3.bmp')
gray2 = cv2.cvtColor(o2,cv2.COLOR_BGR2GRAY)
HuM2=cv2.HuMoments(cv2.moments(gray2)).flatten()
#----------------计算图像3的Hu矩-------------------
o3 = cv2.imread('lena.bmp')
gray3 = cv2.cvtColor(o3,cv2.COLOR_BGR2GRAY)
HuM3=cv2.HuMoments(cv2.moments(gray3)).flatten()
#---------打印图像1、图像2、图像3的特征值------------
print("o1.shape=",o1.shape)
print("o2.shape=",o2.shape)
print("o3.shape=",o3.shape)
print("cv2.moments(gray1)=\n",cv2.moments(gray1))
print("cv2.moments(gray2)=\n",cv2.moments(gray2))
print("cv2.moments(gray3)=\n",cv2.moments(gray3))
print("\nHuM1=\n",HuM1)
print("\nHuM2=\n",HuM2)
print("\nHuM3=\n",HuM3)
#---------计算图像1与图像2、图像3的Hu矩之差----------------
def compareHu(H1, H2):
    diff = np.sum(np.abs(H1 - H2))
    if diff < 1e-5: # 1×10−5=0.00001
        return "形状几乎完全相同"
    elif diff < 1e-3: # 1e-3 = 0.001
        return "形状相似"
    else:
        return "形状明显不同"

print("图1 vs 图2：", compareHu(HuM1, HuM2))
print("图1 vs 图3：", compareHu(HuM1, HuM3))
#---------显示图像----------------
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("original3",o3)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 形状匹配 cv2.matchShapes

- cv2.matchShapes 是直接对比形状相似度，封装了 Hu矩计算和差值，数值越小形状越相似
- 可以快速判断“同形状”、“相似形状”和“不同形状”，非常适合图像库匹配、模板识别、目标检测等场景
- 参数的1表示方法1，基于 Hu 矩差异和对数，0.0 是额外参数，一般不变

```
o1 = cv2.imread('cs1.bmp')
o2 = cv2.imread('cs2.bmp')
o3 = cv2.imread('cc.bmp')
#----------打印3幅原始图像的shape属性值-------------
print("o1.shape=",o1.shape)
print("o2.shape=",o2.shape)
print("o3.shape=",o3.shape)
#--------------色彩空间转换--------------------
gray1 = cv2.cvtColor(o1,cv2.COLOR_BGR2GRAY)
gray2 = cv2.cvtColor(o2,cv2.COLOR_BGR2GRAY)
gray3 = cv2.cvtColor(o3,cv2.COLOR_BGR2GRAY)
#-------------进行Hu矩匹配--------------------
ret0 = cv2.matchShapes(gray1,gray1,1,0.0) # 自己 vs 自己 → 接近 0
ret1 = cv2.matchShapes(gray1,gray2,1,0.0) # 类似图像 → 较小
ret2 = cv2.matchShapes(gray1,gray3,1,0.0) # 完全不同 → 数值明显大
#--------------打印差值--------------------
print("相同图像的matchShape=",ret0)
print("相似图像的matchShape=",ret1)
print("不相似图像的matchShape=",ret2)
#--------------显示3幅原始图像--------------------
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("original3",o3)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 取轮廓内像素点集

- 可以使用np、cv各自提供的两种方式，表格对应下面代码里说明
- nonzero方法返回两个数组 (行索引数组, 列索引数组)，transpose() 将其组合成 [y, x] 的二维坐标列表
- 空心轮廓只包含边界线像素（形状分析、边界提取）。实心轮廓包含轮廓内部所有像素（区域统计、掩膜操作）。
- np.nonzero() 返回 (y,x)，需 transpose 调整。cv2.findNonZero() 返回 (x,y)，直接适合 OpenCV 使用。

| 操作对象       | 方法/函数                                | 空心/实心 | 返回值形式        | 坐标顺序    | 备注/用途                |
| ---------- | ------------------------------------ | ----- | ------------ | ------- | -------------------- |
| 随机矩阵 a     | `np.nonzero(a)` + `np.transpose`     | —     | `N×2` 坐标数组   | `(y,x)` | 查找非零元素位置             |
| 随机矩阵 a     | `cv2.findNonZero(a)`                 | —     | `N×1×2` 坐标数组 | `(x,y)` | 查找非零元素位置，OpenCV风格    |
| 图像轮廓 mask1 | `np.nonzero(mask1)` + `np.transpose` | 空心    | `N×2` 坐标数组   | `(y,x)` | 查找轮廓边界像素位置           |
| 图像轮廓 mask2 | `np.nonzero(mask2)` + `np.transpose` | 实心    | `N×2` 坐标数组   | `(y,x)` | 查找轮廓内部+边界像素          |
| 图像轮廓 mask1 | `cv2.findNonZero(mask1)`             | 空心    | `N×1×2` 坐标数组 | `(x,y)` | 查找轮廓边界像素位置，OpenCV风格  |
| 图像轮廓 mask2 | `cv2.findNonZero(mask2)`             | 实心    | `N×1×2` 坐标数组 | `(x,y)` | 查找轮廓内部+边界像素，OpenCV风格 |

```

#------------生成一个都是0值的a-------------------
a=np.zeros((5,5),dtype=np.uint8)
#-------随机将其中10个位置上的数值设置为1------------
#---times控制次数
#---i,j是随机生成的行、列位置
#---a[i,j]=1,将随机挑选出来的位置上的值设置为1
for times in range(10):
    i=np.random.randint(0,5)
    j=np.random.randint(0,5)
    a[i,j]=1
#-------打印a，观察a内值的情况-----------
print("a=\n",a)
#------查找a内非零值的位置信息------------
loc=np.transpose(np.nonzero(a))
#-----将a内非零值的位置信息输出------------
print("a内非零值位置:\n",loc)




#-----------------读取原始图像----------------------
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
#-----------------获取轮廓------------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cnt=contours[0]
#-----------------绘制空心轮廓------------------------
mask1 = np.zeros(gray.shape,np.uint8)
cv2.drawContours(mask1,[cnt],0,255,2)
pixelpoints1 = np.transpose(np.nonzero(mask1))
print("pixelpoints1.shape=",pixelpoints1.shape)
print("pixelpoints1=\n",pixelpoints1)
cv2.imshow("mask1",mask1)
#-----------------绘制实心轮廓---------------------
mask2 = np.zeros(gray.shape,np.uint8)
cv2.drawContours(mask2,[cnt],0,255,-1)
pixelpoints2 = np.transpose(np.nonzero(mask2))
print("pixelpoints2.shape=",pixelpoints2.shape)
print("pixelpoints2=\n",pixelpoints2)
cv2.imshow("mask2",mask2)
#-----------------释放窗口------------------------
cv2.waitKey()
cv2.destroyAllWindows()


#------------生成一个都是0值的a-------------------
a=np.zeros((5,5),dtype=np.uint8)
#-------随机将其中10个位置上的数值设置为1------------
#---times控制次数
#---i,j是随机生成的行、列位置
#---a[i,j]=1,将随机挑选出来的位置上的值设置为1
for times in range(10):
    i=np.random.randint(0,5)
    j=np.random.randint(0,5)
    a[i,j]=1
#-------打印a，观察a内值的情况-----------
print("a=\n",a)
#------查找a内非零值的位置信息------------
loc = cv2.findNonZero(a)
#-----将a内非零值的位置信息输出------------
print("a内非零值位置:\n",loc)


#-----------------读取原始图像----------------------
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
#-----------------获取轮廓------------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cnt=contours[0]
#-----------------绘制空心轮廓------------------------
mask1 = np.zeros(gray.shape,np.uint8)
cv2.drawContours(mask1,[cnt],0,255,2)
pixelpoints1 = cv2.findNonZero(mask1)
print("pixelpoints1.shape=",pixelpoints1.shape)
print("pixelpoints1=\n",pixelpoints1)
cv2.imshow("mask1",mask1)
#-----------------绘制实心轮廓---------------------
mask2 = np.zeros(gray.shape,np.uint8)
cv2.drawContours(mask2,[cnt],0,255,-1)
pixelpoints2 = cv2.findNonZero(mask2)
print("pixelpoints2.shape=",pixelpoints2.shape)
print("pixelpoints2=\n",pixelpoints2)
cv2.imshow("mask2",mask2)
#-----------------释放窗口------------------------
cv2.waitKey()
cv2.destroyAllWindows()
```

# 外包

## 外包矩形 cv2.boundingRect

- 使用boundingRect获取矩形，rectangle进行获取与绘制

```
o = cv2.imread('cc.bmp')
#---------------提取图像轮廓------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
#---------------构造矩形边界------------------
x,y,w,h = cv2.boundingRect(contours[0])
cv2.rectangle(o,(x,y),(x+w,y+h),(255,255,255),2)
#---------------显示矩形边界------------------
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 外包最小矩形 cv2.minAreaRect

- 不规则图形的外包矩形可以是有角度的，所以比正常的矩形要更小
- 返回点集，所以要再次构造进行绘制

```
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
rect = cv2.minAreaRect(contours[0])
print("返回值rect:\n",rect)
points = cv2.boxPoints(rect) # 将 (center, size, angle) 转为四个角点坐标
print("\n转换后的points：\n",points)
points = np.int0(points)  #取整
image=cv2.drawContours(o,[points],0,(255,255,255),2)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 外包圆形 cv2.minEnclosingCircle

- cv2.minEnclosingCircle 返回 圆心 (x, y) 和半径 radius
- cv2.circle绘制

```
o = cv2.imread('cc.bmp')  
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)  
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)  
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)  
(x,y),radius = cv2.minEnclosingCircle(contours[0])
center = (int(x),int(y))
radius = int(radius)
cv2.circle(o,center,radius,(255,255,255),2)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 外包三角形 cv2.minEnclosingTriangle

三角形可以捕捉轮廓的主方向和尖角，用于对物体方向、尖角特征提取

- cv2.minEnclosingTriangle 返回：area → 三角形面积，trgl → 三个顶点坐标（浮点数）
- 使用cv2.line绘制三条线

```
o = cv2.imread('cc.bmp')  
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)  
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)  
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)  
area,trgl = cv2.minEnclosingTriangle(contours[0])
print("area=",area)
print("trgl:",trgl)
for i in range(0, 3):
    cv2.line(o, tuple(trgl[i][0]), 
             tuple(trgl[(i + 1) % 3][0]), (255,255,255), 2) 
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 外包椭圆 cv2.fitEllipse

- cv2.fitEllipse 返回一个元组：
- (center_x, center_y)：椭圆中心
- (major_axis, minor_axis)：长轴和短轴长度
- angle：长轴与水平线的夹角
- cv2.ellipse绘制

```
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
ellipse = cv2.fitEllipse(contours[0])
retval=cv2.fitEllipse(contours[0])
print("单个返回值形式：")
print("retval=\n",retval)
(x,y),(MA,ma),angle = cv2.fitEllipse(contours[0])
print("三个返回值形式：")
print("(x,y)=(",x,y,")")
print("(MA,ma)=(",MA,ma,")")
print("angle=",angle)
cv2.ellipse(o,ellipse,(0,0,255),2)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

```
o = cv2.imread('cc.bmp')
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cv2.imshow("original",o)
ellipse = cv2.fitEllipse(contours[0])
print("ellipse=",ellipse)
cv2.ellipse(o,ellipse,(0,255,0),3)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 拟合直线 cv2.fitLine

用一条直线近似轮廓的整体方向，可以快速描述轮廓的倾斜方向，对长条或线状物体效果好，多用于方向估计、轮廓主轴分析、形状特征提取

- cv2.fitLine 返回四个参数：(vx, vy) → 方向向量，(x, y) → 直线通过的点（质心附近）
- cv2.line绘制

```
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
rows,cols = image.shape[:2]
[vx,vy,x,y] = cv2.fitLine(contours[0], cv2.DIST_L2,0,0.01,0.01)
# 根据方向向量计算直线在图像左边界和右边界的 y 坐标
# 确保绘制整条直线覆盖整个图像宽度
lefty = int((-x*vy/vx) + y)
righty = int(((cols-x)*vy/vx)+y)
cv2.line(o,(cols-1,righty),(0,lefty),(0,255,0),2)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 轮廓多边形逼近 cv2.approxPolyDP

轮廓逼近是对轮廓进行多边形近似的算法，
- cv2.approxPolyDP的参数epsilon值越小得到的多边形点越多，通常使用周长的比例，True表示闭合轮廓，返回顶点集合

```
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
#----------------获取轮廓-------------------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
#----------------epsilon=0.1*周长-------------------------------
adp = o.copy()
epsilon = 0.1*cv2.arcLength(contours[0],True)
approx = cv2.approxPolyDP(contours[0],epsilon,True)
adp=cv2.drawContours(adp,[approx],0,(0,0,255),2)
cv2.imshow("result0.1",adp)
#----------------epsilon=0.09*周长-------------------------------
adp = o.copy()
epsilon = 0.09*cv2.arcLength(contours[0],True)
approx = cv2.approxPolyDP(contours[0],epsilon,True)
adp=cv2.drawContours(adp,[approx],0,(0,0,255),2)
cv2.imshow("result0.09",adp)
#----------------epsilon=0.055*周长-------------------------------
adp = o.copy()
epsilon = 0.055*cv2.arcLength(contours[0],True)
approx = cv2.approxPolyDP(contours[0],epsilon,True)
adp=cv2.drawContours(adp,[approx],0,(0,0,255),2)
cv2.imshow("result0.055",adp)
#----------------epsilon=0.05*周长-------------------------------
adp = o.copy()
epsilon = 0.05*cv2.arcLength(contours[0],True)
approx = cv2.approxPolyDP(contours[0],epsilon,True)
adp=cv2.drawContours(adp,[approx],0,(0,0,255),2)
cv2.imshow("result0.05",adp)
#----------------epsilon=0.02*周长-------------------------------
adp = o.copy()
epsilon = 0.02*cv2.arcLength(contours[0],True)
approx = cv2.approxPolyDP(contours[0],epsilon,True)
adp=cv2.drawContours(adp,[approx],0,(0,0,255),2)
cv2.imshow("result0.02",adp)
#----------------等待释放窗口-------------------------------
cv2.waitKey()
cv2.destroyAllWindows()
```

# 凸包（Convex Hull）与凸缺陷（Convexity Defects）

## 概念

- 凸包是物体的“外包轮廓”，也就是包住物体所有点的最小凸多边形
- 如一只手，凸包包住了所有手指外沿，手指之间的空隙（“V”形）区域，就是凸缺陷。
- 用于手势识别（比如计算手指数量），统计凹陷点（凸缺陷数量）即可推测有几根手指。形状分析（判断凹凸程度、凹陷深度），用 d 的值判断凹陷“深度”。轮廓平滑/形状简化，可根据缺陷修正非凸轮廓。

## 凸包函数 cv2.convexHull

- contours[0]参数是来自使用findContours获取轮廓的结果点集
- 使用bool参数控制返回图标的点坐标、或是点索引
- 第二个案例是polylines绘制凸包

```
o = cv2.imread('contours.bmp')
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_TREE,
                                             cv2.CHAIN_APPROX_SIMPLE)
hull = cv2.convexHull(contours[0])   #返回坐标值
print("returnPoints为默认值True时返回值hull的值：\n",hull)
hull2 = cv2.convexHull(contours[0], returnPoints=False) #返回索引值
print("returnPoints为False时返回值hull的值：\n",hull2)
```

```
o = cv2.imread('hand.bmp')
cv2.imshow("original",o)
# --------------提取轮廓------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
# --------------寻找凸包，得到凸包的角点------------------
hull = cv2.convexHull(contours[0])
# --------------绘制凸包------------------
cv2.polylines(o, [hull], True, (0, 255, 0), 2)
# --------------显示凸包------------------
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 判断凸多边形 cv2.isContourConvex

```
hull = cv2.convexHull(contours[0])
cv2.polylines(image1, [hull], True, (0, 255, 0), 2)
print("使用函数cv2.convexHull()构造的多边形是否是凸包：",
      cv2.isContourConvex(hull))
```

## 凸缺陷函数 cv2.convexityDefects

- 调用convexHull时要使用false，cv2.convexityDefects要用索引做参数
- 返回一个四元组 [s, e, f, d]

| 参数  | 含义                      |
| --- | ----------------------- |
| `s` | 凸缺陷起点索引（轮廓上的点）          |
| `e` | 凸缺陷终点索引                 |
| `f` | 凹陷处（最远点）索引              |
| `d` | 起点终点到凹陷点的**距离（深度）×256** |


```
img = cv2.imread('hand.bmp')
cv2.imshow('original',img)
#----------------构造轮廓--------------------------
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray, 127, 255,0)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_TREE,
                                             cv2.CHAIN_APPROX_SIMPLE)
#----------------凸包--------------------------
cnt = contours[0]
hull = cv2.convexHull(cnt,returnPoints = False)
defects = cv2.convexityDefects(cnt,hull)
print("defects=\n",defects)
#----------------构造凸缺陷--------------------------
for i in range(defects.shape[0]):
    s,e,f,d = defects[i,0]
    start = tuple(cnt[s][0])
    end = tuple(cnt[e][0])
    far = tuple(cnt[f][0])
    cv2.line(img,start,end,[0,0,255],2)  # 红线连接凸包边缘；
    cv2.circle(img,far,5,[255,0,0],-1) # 蓝点标出“手指间”的凹陷点（凸缺陷）。
#----------------显示结果、释放图像--------------------------
cv2.imshow('result',img)
cv2.waitKey(0)
cv2.destroyAllWindows()
```

## 点到轮廓的距离 cv2.pointPolygonTest

- 参数contour：轮廓（可以是 cv2.convexHull() 的结果）
- (x, y)：要测试的点坐标
- measureDist：False → 只返回点在内部、外部、边界（+1 / -1 / 0），True → 返回实际“有符号距离”
- 返回值：

| 点位置 | 返回值 | 含义               |
| :-- | :-- | :--------------- |
| 内部  | 正数  | 距离轮廓的最近边界线的距离    |
| 边界上 | 0   | 在边缘上             |
| 外部  | 负数  | 到轮廓的最近边界线的距离（取负） |

```
o = cv2.imread('cs.bmp')
cv2.imshow("original",o)
#----------------获取凸包------------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
hull = cv2.convexHull(contours[0])
# 把二值图转换为彩色以便绘制多色信息
image = cv2.cvtColor(image, cv2.COLOR_GRAY2BGR)
cv2.polylines(image, [hull], True, (0, 255, 0), 2)
#----------------内部点A的距离-------------------------
distA = cv2.pointPolygonTest(hull, (300, 150), True)
font=cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(image,'A',(300,150), font, 1,(0,255,0),3)
print("distA=",distA)
#----------------外部点B的距离-------------------------
distB = cv2.pointPolygonTest(hull, (300, 250), True)
font=cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(image,'B',(300,250), font, 1,(0,255,0),3)
print("distB=",distB)
#------------正好处于边缘上的点C的距离-----------------
distC = cv2.pointPolygonTest(hull, (423, 112), True)
font=cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(image,'C',(423,112), font, 1,(0,255,0),3)
print("distC=",distC)
#print(hull)   #测试边缘到底在哪里，然后再使用确定位置的
#----------------显示-------------------------
cv2.imshow("result",image)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 轮廓形状匹配（Shape Context Distance Extractor）

## 比较特性

| 特性        | Shape Context | Hausdorff |
| --------- | ------------- | --------- |
| 核心原理      | 匹配点分布统计       | 最大最小距离    |
| 对噪声的敏感度   | 较低            | 较高        |
| 对旋转/缩放鲁棒性 | 一般            | 一般        |
| 计算速度      | 较慢            | 较快        |
| 适用场景      | 复杂形状分类        | 快速相似检测    |

## 形状上下文距离算子 cv2.createShapeContextDistanceExtractor

- 创建出的是一个形状上下文（Shape Context）算法的对象，用与分析两个轮廓的整体形状分布，通过匹配点的相对位置来衡量形状的相似度。
- 使用此对象的computeDistance()计算形状相似度
- 算法输出的距离值没有固定单位；0 表示完全相同；<0.2 表示非常相似（可能是同一物体的不同角度或比例）；0.5 表示形状差异较大；1 表示明显不同。

```
o1 = cv2.imread('cs.bmp')
cv2.imshow("original1",o1)
gray1 = cv2.cvtColor(o1,cv2.COLOR_BGR2GRAY)
ret, binary1 = cv2.threshold(gray1,127,255,cv2.THRESH_BINARY)
image,contours1, hierarchy = cv2.findContours(binary1,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
cnt1 = contours1[0]
#-----------原始图像o2边缘--------------------
o2 = cv2.imread('cs3.bmp')
cv2.imshow("original2",o2)
gray2 = cv2.cvtColor(o2,cv2.COLOR_BGR2GRAY)
ret, binary2 = cv2.threshold(gray2,127,255,cv2.THRESH_BINARY)
image,contours2, hierarchy = cv2.findContours(binary2,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
cnt2 = contours2[0]
#-----------原始图像o3边缘--------------------
o3 = cv2.imread('hand.bmp')
cv2.imshow("original3",o3)
gray3 = cv2.cvtColor(o3,cv2.COLOR_BGR2GRAY)
ret, binary3 = cv2.threshold(gray3,127,255,cv2.THRESH_BINARY)
image,contours3, hierarchy = cv2.findContours(binary3,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
cnt3 = contours3[0]
#-----------构造距离提取算子--------------------
sd = cv2.createShapeContextDistanceExtractor()
#-----------计算距离--------------------
d1 = sd.computeDistance(cnt1,cnt1)
print("自身距离d1=", d1)
d2 = sd.computeDistance(cnt1,cnt2)
print("旋转缩放后距离d2=", d2)
d3 = sd.computeDistance(cnt1,cnt3)
print("不相似对象距离d3=", d3)
#-----------显示距离--------------------
cv2.waitKey()
cv2.destroyAllWindows()
```

## Hausdorff距离算子 cv2.createHausdorffDistanceExtractor

- 使用cv2.createHausdorffDistanceExtractor创建算子，使用hd.computeDistance计算两个点集（或轮廓）之间的最大“最短距离”。

| 距离范围    | 形状关系        |
| ------- | ----------- |
| 0 ~ 1   | 完全相同        |
| 1 ~ 10  | 高度相似（旋转/缩放） |
| 10 ~ 50 | 有明显差异       |
| >50     | 完全不同        |


| 变量   | 对比对象         | 含义   | 期望结果         |
| ---- | ------------ | ---- | ------------ |
| `d1` | 自身 vs 自身     | 完全相同 | 应接近 0        |
| `d2` | 原图 vs 旋转/缩放后 | 相似   | 值较小（例如 2~10） |
| `d3` | 原图 vs 不同形状   | 不相似  | 值较大（几十甚至上百）  |


```
o1 = cv2.imread('cs.bmp')
o2 = cv2.imread('cs3.bmp')
o3 = cv2.imread('hand.bmp')
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("original3",o3)
#-----------色彩转换--------------------
gray1 = cv2.cvtColor(o1,cv2.COLOR_BGR2GRAY)
gray2 = cv2.cvtColor(o2,cv2.COLOR_BGR2GRAY)
gray3 = cv2.cvtColor(o3,cv2.COLOR_BGR2GRAY)
#-----------阈值处理--------------------
ret, binary1 = cv2.threshold(gray1,127,255,cv2.THRESH_BINARY)
ret, binary2 = cv2.threshold(gray2,127,255,cv2.THRESH_BINARY)
ret, binary3 = cv2.threshold(gray3,127,255,cv2.THRESH_BINARY)
#-----------提取轮廓--------------------
image,contours1, hierarchy = cv2.findContours(binary1,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
image,contours2, hierarchy = cv2.findContours(binary2,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
image,contours3, hierarchy = cv2.findContours(binary3,
                                              cv2.RETR_LIST,
                                              cv2.CHAIN_APPROX_SIMPLE)
cnt1 = contours1[0]
cnt2 = contours2[0]
cnt3 = contours3[0]
#-----------构造距离提取算子--------------------
hd = cv2.createHausdorffDistanceExtractor()
#-----------计算距离--------------------
d1 = hd.computeDistance(cnt1,cnt1)
print("自身Hausdorff距离d1=", d1)
d2 = hd.computeDistance(cnt1,cnt2)
print("旋转缩放后Hausdorff距离d2=", d2)
d3 = hd.computeDistance(cnt1,cnt3)
print("不相似对象Hausdorff距离d3=", d3)
#-----------显示距离--------------------
cv2.waitKey()
cv2.destroyAllWindows()
```

# 形状特征综合分析

## 算面积 contourArea

- 使用cv2.contourArea函数计算轮廓面积，比使用矩（cv2.moments）的方式快一点

```
o = cv2.imread('contours.bmp')
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cv2.imshow("original",o)
n=len(contours)
contoursImg=[]
for i in range(n):
    print("contours["+str(i)+"]面积=",cv2.contourArea(contours[i]))
    temp=np.zeros(o.shape,np.uint8)
    contoursImg.append(temp)
    contoursImg[i]=cv2.drawContours(contoursImg[i],
                                   contours,
                                   i,
                                   (255,255,255),
                                   3)
    cv2.imshow("contours[" + str(i)+"]",contoursImg[i])
cv2.waitKey()
cv2.destroyAllWindows()
```

## 占空比（extent）

- 可理解为：轮廓面积 / 外接矩形面积
- 它描述了图形在包围矩形中“填满”的程度。例如：圆形的占空比 ≈ 0.785（π/4），正方形的占空比 = 1.0，细长条或星形的占空比 < 0.5

## 算周长 arcLength

- arcLength：参数 True 表示轮廓是封闭的；如果是曲线（非封闭），则用 False。

```
#--------------读取及显示原始图像--------------------
o = cv2.imread('contours0.bmp')
cv2.imshow("original",o)
#--------------获取轮廓--------------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
#--------------计算各个轮廓的长度和、平均长度--------------------
n=len(contours)   #获取轮廓个数
cntLen=[]           #存储各个轮廓的长度
for i in range(n):
    cntLen.append(cv2.arcLength(contours[i],True))
    print("第"+str(i)+"个轮廓的长度:%d"%cntLen[i])
cntLenSum=np.sum(cntLen)  #各个轮廓长度和
cntLenAvr=cntLenSum/n    #各个轮廓长度平均值
print("各个轮廓的总长度为：%d"%cntLenSum)
print("各个轮廓的平均长度为：%d"%cntLenAvr)
#--------------显示超过平均值的轮廓--------------------
contoursImg=[]
for i in range(n):
    temp=np.zeros(o.shape,np.uint8)
    contoursImg.append(temp)
    contoursImg[i]=cv2.drawContours(contoursImg[i],
               contours,i,(255,255,255),3)
    if cv2.arcLength(contours[i],True)>cntLenAvr:
        cv2.imshow("contours[" + str(i)+"]",contoursImg[i])
cv2.waitKey()
cv2.destroyAllWindows()
```

## 凸度（solidity）

- 可以用来衡量一个图形轮廓是否有凹陷或复杂边缘
- 凸度 = 轮廓面积 / 凸包面积，结果越接近 1，形状越凸；越小，凹陷越明显。如手指间空隙会让 solidity 明显小于 1（比如 0.7~0.8）
- 实际用途：手形、叶子、物体检测 → 判断凹凸

```
o = cv2.imread('hand.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,cv2.RETR_LIST,cv2.CHAIN_APPROX_SIMPLE)
cv2.drawContours(o,contours[0],-1,(0,0,255),3)
cntArea=cv2.contourArea(contours[0])
hull = cv2.convexHull(contours[0])
hullArea = cv2.contourArea(hull)
cv2.polylines(o, [hull], True, (0, 255, 0), 2)
solidity=float(cntArea)/hullArea
print(solidity)
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 等效直径（equivalent diameter）

- 把任意形状的面积用一个“圆的直径”来表示，方便比较不同物体的大小
- 公式：np.sqrt(4*Area/np.pi)
- 用于尺寸比较：把任意形状的面积统一转换成一个圆的直径，便于比较大小。形状分析：与圆形度、凸度结合，可了解物体的形状特征。形态学测量：适合植物叶子、细胞、零件等分析

```
o = cv2.imread('cc.bmp')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cv2.drawContours(o,contours[0],-1,(0,0,255),3)
cntArea=cv2.contourArea(contours[0])
equiDiameter = np.sqrt(4*cntArea/np.pi)
print(equiDiameter)
cv2.circle(o,(100,100),int(equiDiameter/2),(0,0,255),3) #展示等直径大小的圆
cv2.imshow("result",o)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 区域内灰度最值 cv2.minMaxLoc

使用cv2.minMaxLoc(gray, mask=mask)在掩膜区域内找出最亮点和最暗点（maxVal / minVal）及其位置

| 场景           | 说明                                 |
| ------------ | ---------------------------------- |
| **医学影像分析**   | 提取肿瘤、器官等特定区域，分析亮度差异或密度分布（如CT、MRI）。 |
| **工业检测**     | 检测零件缺陷或特定区域的磨损、划痕、颜色异常。            |
| **目标跟踪/识别**  | 只关注图像中的目标区域，对目标进行特征提取和匹配。          |
| **图像分割后的分析** | 分割出对象轮廓后，统计该对象内部的灰度、颜色或纹理特征。       |
| **形态学测量**    | 结合轮廓或掩膜，测量面积、直径、亮度范围等指标。           |

```
o = cv2.imread('ct.png')
cv2.imshow("original",o)
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cnt=contours[2]   #coutours[0]、coutours[1]是左侧字母R
#--------使用掩膜获取感兴趣区域的最值-----------------
#需要注意minMaxLoc处理的对象为灰度图像，本例中处理对象为灰度图像gray
#如果希望获取彩色图像的，需要提取各个通道，将每个通道独立计算最值
mask = np.zeros(gray.shape,np.uint8)
mask=cv2.drawContours(mask,[cnt],-1,255,-1)
minVal, maxVal, minLoc, maxLoc = cv2.minMaxLoc(gray,mask = mask)
print("minVal=",minVal)
print("maxVal=",maxVal)
print("minLoc=",minLoc)
print("maxLoc=",maxLoc)
#--------使用掩膜获取感兴趣区域并显示-----------------
masko = np.zeros(o.shape,np.uint8)
masko=cv2.drawContours(masko,[cnt],-1,(255,255,255),-1)
loc=cv2.bitwise_and(o,masko)
cv2.imshow("mask",loc)
#显示灰度结果
#loc=cv2.bitwise_and(gray,mask)
#cv2.imshow("mask",loc)
#--------释放窗口-----------------
cv2.waitKey()
cv2.destroyAllWindows()
```

## 区域内灰度平均值 cv2.mean

- cv2.mean() 计算彩色图像在掩膜区域的 BGR通道平均值。结果是包含B、G、R、A四个值，alpha 一般为 0。

```
o = cv2.imread('ct.png')
cv2.imshow("original",o)
#--------获取轮廓-----------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,
                                             cv2.RETR_LIST,
                                             cv2.CHAIN_APPROX_SIMPLE)
cnt=contours[2]
#--------使用掩膜获取感兴趣区域的均值-----------------
mask = np.zeros(gray.shape,np.uint8)#构造mean所使用的掩膜，必须是单通道的
cv2.drawContours(mask,[cnt],0,(255,255,255),-1)
meanVal = cv2.mean(o,mask = mask)  #mask是区域，所以必须是单通道的
print("meanVal=\n",meanVal)
#--------使用掩膜获取感兴趣区域并显示-----------------
masko = np.zeros(o.shape,np.uint8)
cv2.drawContours(masko,[cnt],-1,(255,255,255),-1)
loc=cv2.bitwise_and(o,masko) # 原图中感兴趣区域提取出来，其他部分置黑，o是彩色图、masko是二值图
cv2.imshow("mask",loc)
#--------释放窗口-----------------
cv2.waitKey()
cv2.destroyAllWindows()
```

## 极值点（最左、最右、最上、最下的点）

典型应用

- 形状分析：获取对象的边界极限，计算尺寸、比例。
- 目标定位：快速得到轮廓的范围，用于裁剪、跟踪。
- 姿态估计：手或物体关键点提取。
- 碰撞检测：游戏或机器人，判断对象边界位置。

```
o = cv2.imread('cs.bmp')
#--------获取并绘制轮廓-----------------
gray = cv2.cvtColor(o,cv2.COLOR_BGR2GRAY)
ret, binary = cv2.threshold(gray,127,255,cv2.THRESH_BINARY)
image,contours, hierarchy = cv2.findContours(binary,cv2.RETR_LIST,cv2.CHAIN_APPROX_SIMPLE)
mask = np.zeros(gray.shape,np.uint8)
cnt=contours[0]
cv2.drawContours(mask,[cnt],0,255,-1)
#--------计算极值-----------------
leftmost = tuple(cnt[cnt[:,:,0].argmin()][0])
rightmost = tuple(cnt[cnt[:,:,0].argmax()][0])
topmost = tuple(cnt[cnt[:,:,1].argmin()][0])
bottommost = tuple(cnt[cnt[:,:,1].argmax()][0])
#--------计算极值-----------------
print("leftmost=",leftmost)
print("rightmost=",rightmost)
print("topmost=",topmost)
print("bottommost=",bottommost)
#--------绘制说明文字-----------------
font=cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(o,'A',leftmost, font, 1,(0,0,255),2)
cv2.putText(o,'B',rightmost, font, 1,(0,0,255),2)
cv2.putText(o,'C',topmost, font, 1,(0,0,255),2)
cv2.putText(o,'D',bottommost, font, 1,(0,0,255),2)
#--------绘制图像-----------------
cv2.imshow("result",o)
#--------释放窗口-----------------
cv2.waitKey()
cv2.destroyAllWindows()
```

# 渲染

- cv2.putText 文字
- cv2.polylines 多边形
- cv2.line 线
- cv2.circle 圆
- cv2.rectangle 矩形
- cv2.ellipse 椭圆
- cv2.drawContours 轮廓

# 金字塔操作（Pyramid）

## 高频、低频

- 图像可以看成是不同频率成分的叠加：
- 高频：图像中快速变化的部分（边缘、细节、纹理）
- 低频：平滑缓慢变化的部分（大块颜色或光照、轮廓）
- 高斯金字塔保留低频，Laplace金字塔提取高频。

| 图像成分 | 高频 / 低频 |
| ---- | ------- |
| 边缘   | 高频      |
| 纹理   | 高频      |
| 颜色渐变 | 低频      |
| 光照背景 | 低频      |
| 噪声   | 高频      |

## 高斯金字塔 （Gaussian Pyramid）

- 是一种多分辨率图像表示方法，核心就是不断下采样和模糊
- 图像每向上一层，分辨率宽高各减半，同时图像会先进行高斯平滑（去掉高频噪声），保留低频

## pyrUp、pyrDown（上下采样）

- pyrDown：下采样，尺寸减半，同时经过高斯模糊（去除高频，保留低频）
- pyrUp：上采样，尺寸倍增，依然模糊

```
import cv2
import numpy as np
o=cv2.imread("lena.bmp")
r1=cv2.pyrDown(o)
r2=cv2.pyrDown(r1)
r3=cv2.pyrDown(r2)
print("o.shape=",o.shape)
print("r1.shape=",r1.shape)
print("r2.shape=",r2.shape)
print("r3.shape=",r3.shape)
cv2.imshow("original",o)
cv2.imshow("r1",r1)
cv2.imshow("r2",r2)
cv2.imshow("r3",r3)
cv2.waitKey()
cv2.destroyAllWindows()

o=cv2.imread("lenas.bmp")
r1=cv2.pyrUp(o)
r2=cv2.pyrUp(r1)
r3=cv2.pyrUp(r2)
print("o.shape=",o.shape)
print("r1.shape=",r1.shape)
print("r2.shape=",r2.shape)
print("r3.shape=",r3.shape)
cv2.imshow("original",o)
cv2.imshow("r1",r1)
cv2.imshow("r2",r2)
cv2.imshow("r3",r3)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Laplace金字塔

- 是多分辨率图像表示方法，在高斯金字塔的基础上，要保留每层的高频细节，用于无损恢复
- 原图减去低频的模糊图，剩下的就是清晰的边缘和纹理（高频部分）
- 流程：原图 → 下采样 → 上采样 → 差值 = 高频图

```
O = cv2.imread("lena.bmp")       # 原图
G0 = O                           # 高斯金字塔第0层
G1 = cv2.pyrDown(G0)             # 下采样，得到低频信息
L0 = O - cv2.pyrUp(G1)           # 先上采样恢复尺寸，原图-低频=高频细节，Laplace 金字塔的核心操作
RO = L0 + cv2.pyrUp(G1)          # 通过 Laplace 重建原图
```

## Laplace无损案例

```
O=cv2.imread("lena.bmp")
#=================生成高斯金字塔======================
G0=O
G1=cv2.pyrDown(G0)
G2=cv2.pyrDown(G1)
G3=cv2.pyrDown(G2)
#===============生成拉普拉斯金字塔====================
L0=G0-cv2.pyrUp(G1) #拉普拉斯金字塔第0层
L1=G1-cv2.pyrUp(G2) #拉普拉斯金字塔第1层
L2=G2-cv2.pyrUp(G3) #拉普拉斯金字塔第2层
#=================复原G0======================
RG0=L0+cv2.pyrUp(G1)  #通过拉普拉斯图像复原的原始图像G0
print("G0.shape=",G0.shape)
print("RG0.shape=",RG0.shape)
result=RG0-G0  #将RG0和G0做减法
#计算result的绝对值，避免求和时负负为正3+(-3)=0
result=abs(result)  
#计算result所有元素的和
print("原始图像G0与恢复图像RG0差值的绝对值和：",np.sum(result))   
#=================复原G1======================
RG1=L1+cv2.pyrUp(G2) #通过拉普拉斯图像复原G1
print("G1.shape=",G1.shape)
print("RG1.shape=",RG1.shape)
result=RG1-G1  #将o和ro做减法
print("原始图像G1与恢复图像RG1差值的绝对值和：",np.sum(abs(result)))
#=================复原G2======================
RG2=L2+cv2.pyrUp(G3) #通过拉普拉斯图像复原G2
print("G2.shape=",G2.shape)
print("RG2.shape=",RG2.shape)
result=RG2-G2  #将o和ro做减法
print("原始图像G2与恢复图像RG2差值的绝对值和：",np.sum(abs(result)))
```

# 直方图 Histogram

## 概念作用

### 普通直方图

- 是一种统计图，每个灰度值（0~255）出现的“像素数量”。
- 对灰度图来说，横轴是 像素值（0～255），纵轴是 该灰度值出现的次数。
- 对彩色图像来说，每个通道（R、G、B）都有一个独立的直方图。
- 直方图能非常直观地反映图像的整体特征，在 图像分析、增强、分割、特征识别 等方面都有重要作用。

| 应用方向             | 作用说明                     |
| ---------------- | ------------------------ |
| **亮度/对比度分析**     | 观察图像偏亮、偏暗还是灰度集中（对比度低）    |
| **图像增强（直方图均衡化）** | 自动拉伸亮度分布，增强对比度           |
| **阈值分割**         | 通过直方图找到前景与背景分界点（如 Otsu法） |
| **特征描述**         | 灰度分布模式可作为图像特征进行匹配        |
| **颜色校正**         | 分析 RGB 各通道直方图判断色偏或曝光问题   |

|  直方图形态  |           图像特性          |
| :-----: | :---------------------: |
| 分布集中在左边 |           图像偏暗          |
| 分布集中在右边 |           图像偏亮          |
|  分布窄而集中 |        对比度低、灰度层次少       |
|  分布宽而均匀 |        对比度高、层次丰富        |
|   双峰形状  | 通常表示图像有明显的前景与背景（适合阈值分割） |

### 归一化直方图 cv2.normalize

- 如果两张图大小不同（比如一张 100×100，一张 1000×1000），灰度为 128 的像素数量就无法直接比较。
- 归一化直方图统计的是每个灰度级像素出现的“概率”而不是“次数”。它把像素数量转为比例，使不同大小或亮度范围的图像可直接比较。所有灰度的概率之和等于1

| 项目        | 普通直方图  | 归一化直方图       |
| --------- | ------ | ------------ |
| 数值含义      | 像素数量   | 像素比例（概率）     |
| 是否受图像大小影响 | ✅ 会受影响 | ❌ 不受影响       |
| 应用场景      | 观察亮度分布 | 图像比较、匹配、统计分析 |
| 总和        | 不定     | 恒为 1         |

| 应用场景              | 为什么要用归一化直方图    |
| ----------------- | -------------- |
| 图像特征提取（例如直方图匹配）   | 尺寸不同但分布需可比     |
| 图像分类 / 检索         | 可作为纹理或亮度特征输入   |
| 图像相似度计算（如巴氏距离）    | 需要概率分布形式       |
| 图像增强（直方图均衡化算法的基础） | 算法内部需归一化累积分布函数 |

### dims、range、bins

| 名称      | 中文含义          | 控制什么        | 举例               |
| ------- | ------------- | ----------- | ---------------- |
| `dims`  | 维度（Dimension） | 要计算的颜色通道数量  | 灰度图是1维，彩色图RGB是3维 |
| `range` | 取值范围          | 灰度或颜色值的上下限  | 一般是 `[0, 256]`   |
| `bins`  | 等级分片 | 把灰度值分成多少个区间进行统计 | 一般为 256          |

## 统计 cv2.calcHist

下面案例的参数作用

| 参数        | 含义     | 示例值       | 说明              |
| --------- | ------ | --------- | --------------- |
| `[img]`   | 输入图像列表 | `[img]`   | 可以传多张图像（一般只有一张） |
| `[0]`     | 通道索引   | `[0]`     | 对灰度或B通道统计       |
| `None`    | 掩膜     | `None`    | 不使用掩膜（即全图参与统计）  |
| `[256]`   | bin 数  | `[256]`   | 共有256个灰度区间      |
| `[0,255]` | 范围     | `[0,255]` | 灰度值从0到255       |


```
import cv2
import matplotlib.pyplot as plt

img = cv2.imread('lena.bmp', 0)  # 读入灰度图
hist = cv2.calcHist([img],[0],None,[256],[0,255])
print(type(hist)) # 其实就是一个 NumPy 数组。
print(hist.shape) # 共 256 行（对应 256 个灰度值 bin）
print(hist.size) # 256 个统计点
print(hist) # 每一行代表对应灰度值的像素数量。例如：hist[0][0] 是灰度为0的像素个数（黑），hist[255][0] 是灰度为255的像素个数（白）
```

## 均衡化 cv2.equalizeHist

- 案例见绘制篇章内
- 增强图像对比度，使暗亮区域更分明，便于后续处理（如边缘检测、分割）
- 直方图更加平坦，灰度级利用更充分。
- 应用场景：医学影像处理CT、X光、MRI 提高可见细节，摄像头图像增强，低光照条件下提高可见度。OCR/文字识别，使文字与背景对比增强。计算机视觉算法预处理，边缘检测、分割、目标识别

## 绘制 plt.plot

### xy轴简单案例

```
import cv2
import matplotlib.pyplot as plt

x = [0,1,2,3,4,5,6]
y = [0.3,0.4,2,5,3,4.5,4]
plt.plot(x,y)
plt.show()
```

### 缺省x轴

默认从1整数递增

```
y = [0.3,0.4,2,5,3,4.5,4]
plt.plot(y)
plt.show()
```

### 两条线

均衡化绘制案例有更丰富的两个数据绘制在同一图里

```
import matplotlib.pyplot as plt
a = [0.3,0.4,2,5,3,4.5,4]
b=[3,5,1,2,1,5,3]
plt.plot(a,color='r')
plt.plot(b,color='g')
plt.show()
```

### 绘制黑白统计

```
import matplotlib.pyplot as plt
o=cv2.imread("boatGray.bmp")
histb = cv2.calcHist([o],[0],None,[256],[0,255])
plt.plot(histb,color='b')
plt.show()
```

### 绘制彩色统计

```
import cv2

import matplotlib.pyplot as plt
o=cv2.imread("girl.bmp")
histb = cv2.calcHist([o],[0],None,[256],[0,255])
histg = cv2.calcHist([o],[1],None,[256],[0,255])
histr = cv2.calcHist([o],[2],None,[256],[0,255])
plt.plot(histb,color='b')
plt.plot(histg,color='g')
plt.plot(histr,color='r')
plt.show()
```

### 绘制局部统计（掩码）

掩码就像一个“选择框”，告诉函数“只处理这里，不处理那里”，可以对图像进行 局部分析、局部增强或局部特征提取。

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
image=cv2.imread("girl.bmp",cv2.IMREAD_GRAYSCALE)
mask=np.zeros(image.shape,np.uint8)
mask[200:400,200:400]=255
histImage=cv2.calcHist([image],[0],None,[256],[0,255])
histMI=cv2.calcHist([image],[0],mask,[256],[0,255])
plt.plot(histImage)
plt.plot(histMI)
plt.show()
```

### 绘制均衡化

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

#-----------读取原始图像---------------
img = cv2.imread('equ.bmp',cv2.IMREAD_GRAYSCALE)
#-----------直方图均衡化处理---------------
equ = cv2.equalizeHist(img)
#-----------显示均衡化前后的直方图---------------
cv2.imshow("original",img)
cv2.imshow("result",equ)
#-----------在同一个窗口绘制直方图---------------
plt.figure("灰度直方图对比")
# ravel将二维图像展平成一维，用于绘制直方图
plt.hist(img.ravel(), bins=256, range=(0,255), color='blue', alpha=0.5, label='原始图像')
plt.hist(equ.ravel(), bins=256, range=(0,255), color='red', alpha=0.5, label='均衡化图像')
plt.xlabel('灰度值')
plt.ylabel('像素数量')
plt.title('原始图像 vs 均衡化图像直方图')
plt.legend()
plt.show()
#----------等待释放窗口---------------------
cv2.waitKey()
cv2.destroyAllWindows()
```

### 多个直方图 plt.subplot

- 不是一个直方图上两条线，而是将2个直方图绘制到一个窗口里
- plt.subplot(121)：窗口分成 1 行 2 列，当前绘制在第 1 个区域
- plt.subplot(122)：同上，第 2 个区域

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread('equ.bmp',cv2.IMREAD_GRAYSCALE)
equ = cv2.equalizeHist(img)
plt.figure("subplot示例")
plt.subplot(121),plt.hist(img.ravel(),256)
plt.subplot(122),plt.hist(equ.ravel(),256)
plt.show()
```

### 绘制彩色图片 plt.imshow

- OpenCV 读取彩色图像时是 BGR，而Matplotlib 显示图像时是 RGB，所以要cvtColor转换
- plt.imshow直接显示 OpenCV 读入的 BGR 图像

```
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread('girl.bmp')
imgRGB=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
plt.figure("显示结果")
plt.subplot(121)
plt.imshow(img),plt.axis('off')
plt.subplot(122)
plt.imshow(imgRGB),plt.axis('off')
plt.show()
```

### 绘制灰度图片

| 子图位置 | 数据       | cmap | 显示效果 | 说明                     |
| ---- | -------- | ---- | ---- | ---------------------- |
| 221  | 彩色图像 BGR | 默认   | 颜色偏蓝 | Matplotlib 默认是 RGB，未转换 |
| 222  | 彩色图像 BGR | gray | 灰度映射 | 强制灰度显示，数据未改变           |
| 223  | 灰度图像 g   | 默认   | 伪彩色  | Matplotlib 自动映射为彩色显示   |
| 224  | 灰度图像 g   | gray | 正确灰度 | 标准灰度显示，最常用             |


```
import cv2
import numpy as np
import matplotlib.pyplot as plt
o = cv2.imread('girl.bmp')
g=cv2.cvtColor(o, cv2.COLOR_BGR2GRAY)
plt.figure("灰度图像显示演示")
plt.subplot(221)
plt.imshow(o),plt.axis('off')
plt.subplot(222)
plt.imshow(o,cmap=plt.cm.gray),plt.axis('off')
plt.subplot(223)
plt.imshow(g),plt.axis('off')
plt.subplot(224)
plt.imshow(g,cmap=plt.cm.gray),plt.axis('off') # 这个是正确的，其余的色彩模式是错误的
plt.show()
```

### 灰度图像的colormap色彩映射表

| 子图位置 | cmap                   | 说明             |
| ---- | ---------------------- | -------------- |
| 221  | gray / plt.cm.gray     | 正常灰度显示，亮→白，暗→黑 |
| 222  | gray_r / plt.cm.gray_r | 反转灰度显示，亮→黑，暗→白 |
| 223  | gray                   | 同 221，标准灰度显示   |
| 224  | gray_r                 | 同 222，反转灰度显示   |

应用场景：

- gray_r 适合突出图像暗区或需要反色显示的情况
- 在医学图像、热图、掩码可视化等场景常用
- 不改变图像数据，只改变显示效果

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
o = cv2.imread('8.bmp')
g=cv2.cvtColor(o, cv2.COLOR_BGR2GRAY)
plt.figure("灰度图像显示演示")
plt.subplot(221); plt.imshow(g, cmap=plt.cm.gray)
plt.subplot(222); plt.imshow(g, cmap=plt.cm.gray_r)
plt.subplot(223); plt.imshow(g, cmap='gray')
plt.subplot(224); plt.imshow(g, cmap='gray_r')
plt.show()
```

# 傅里叶变换

## 重要概念

- 频谱、频域：都是指的通过傅里叶变化（np.fft.fft2、cv2.dft）后的初步结果数组
- 低频区域，即频谱中心，是通过np.fft.fft2得到的矩阵（即频谱）的中心
- 通过中心化操作后得到的结果应是中心低频（0、白，代表光照不均或大面积阴影）四周高频（1、黑，信息量大）


## numpy的傅里叶

### 变换

- 二维Fourier Transform
  
    原始频谱 = np.fft.fft2(原始图像) ，对灰度图做二维傅里叶、得到复数数组，每个点代表某个频率的振幅（幅度）+相位信息。
- 频谱中心化
  
    频谱值 = np.fft.fftshift(原始频谱)，结果零频率默认左上角，将其移到图像中心便于观察。
- 取绝对值得到灰度图
  
    像素新值 = 20*np.log(np.abs(频谱值))，复数数组转为0-255的灰度值

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('lena.bmp',0)
f = np.fft.fft2(img)
fshift = np.fft.fftshift(f)
magnitude_spectrum = 20*np.log(np.abs(fshift))
plt.subplot(121)
plt.imshow(img, cmap = 'gray')
plt.title('original')
plt.axis('off')
plt.subplot(122)
plt.imshow(magnitude_spectrum, cmap = 'gray')
plt.title('result')
plt.axis('off')
plt.show()
```

### 逆变换

FFT → 频谱平移 → 逆平移 → IFFT 会还原原图

- 把中心化后的频谱移回原来的布局
  
    ishift = np.fft.ifftshift(fshift)

- 逆傅里叶变换恢复图像

    iimg = np.fft.ifft2(ishift)

- 取绝对值得到灰度图

    iimg = np.abs(iimg)

```
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('boat.jpg',0)
f = np.fft.fft2(img)
fshift = np.fft.fftshift(f)
ishift = np.fft.ifftshift(fshift)
iimg = np.fft.ifft2(ishift)
#print(iimg)
iimg = np.abs(iimg)
#print(iimg)
plt.subplot(121),plt.imshow(img, cmap = 'gray')
plt.title('original'),plt.axis('off')
plt.subplot(122),plt.imshow(iimg, cmap = 'gray')
plt.title('iimg'),plt.axis('off')
plt.show()
```

## opencv的傅里叶

### 变换

| 功能   | numpy.fft | cv2.dft     |
| ---- | --------- | ----------- |
| 输入格式 | 任意数组      | float32     |
| 输出格式 | 复数矩阵      | 两通道矩阵（实/虚）  |
| 性能   | 较慢        | 更快（大图更明显）   |
| 工业用  | 较少        | 常用（尤其大图、实时） |


- cv2.dft不能处理uint8。默认输出频谱为两通道（[:,:,0] = 实部、[:,:,1] = 虚部）、shape = (H, W, 2)
  
    dft = cv2.dft(np.float32(img), flags=cv2.DFT_COMPLEX_OUTPUT)
- 把低频移到中心、计算幅度谱
  
    dftShift = np.fft.fftshift(dft)  
    result = 20*np.log(cv2.magnitude(dftShift[:,:,0], dftShift[:,:,1]))

 
```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('lena.bmp',0)
dft = cv2.dft(np.float32(img),flags = cv2.DFT_COMPLEX_OUTPUT)
dftShift = np.fft.fftshift(dft)
result = 20*np.log(cv2.magnitude(dftShift[:,:,0],dftShift[:,:,1]))
plt.subplot(121),plt.imshow(img, cmap = 'gray')
plt.title('original'),plt.axis('off')
plt.subplot(122),plt.imshow(result, cmap = 'gray')
plt.title('result'), plt.axis('off')
plt.show()
#print(dft)
```

### 逆变换

过程类似于numpy的逆操作案例，仅逆变换回空间域操作函数不同，iImg = cv2.idft(ishift)

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('lena.bmp',0)
dft = cv2.dft(np.float32(img),flags = cv2.DFT_COMPLEX_OUTPUT)
dftShift = np.fft.fftshift(dft)
ishift = np.fft.ifftshift(dftShift)
iImg = cv2.idft(ishift)
iImg= cv2.magnitude(iImg[:,:,0],iImg[:,:,1])
plt.subplot(121),plt.imshow(img, cmap = 'gray')
plt.title('original'), plt.axis('off')
plt.subplot(122),plt.imshow(iImg, cmap = 'gray')
plt.title('inverse'), plt.axis('off')
plt.show()
```


## 高通滤波与低通滤波

| 项目              | **低通滤波 (Low-pass)**  | **高通滤波 (High-pass)**       |
| --------------- | -------------------- | -------------------------- |
| **核心目的**        | 保留低频，去掉高频            | 保留高频，去掉低频                  |
| **保留内容**        | 整体亮度趋势、大范围变化、轮廓      | 边缘、细节、纹理、快速变化              |
| **去除内容**        | 细节、噪声、边缘             | 平坦区域、背景、整体亮度趋势             |
| **图像效果**        | 模糊、变平滑               | 边缘增强，看起来更锐利                |
| **应用场景**        | 去噪、模糊、抗锯齿、下采样前滤波     | 边缘检测、锐化、特征提取               |
| **典型 mask**（频域） | 中心为 1（保低频），周围为 0     | 中心为 0（去低频），周围为 1           |
| **代码直观效果**      | fshift * mask → 模糊图像 | fshift * mask → 类似“素描/边缘图” |
| **数学意义**        | 平滑信号，去掉“快速变化”成分      | 强化信号变化，突出突变点               |


### 高通（强化边缘细节）

高通滤波用于边缘增强、锐化、去除光照、特征增强、边缘细节增强。案例的操作是很理想化的，直接置零，实际中要更复杂
- 取图像中心位置
  
    rows, cols = img.shape  
    crow, ccol = int(rows/2), int(cols/2) ，是整幅图的中心坐标，用来定位低频区域（频谱中心）
- 核心操作：屏蔽低频部分（高通滤波）

    fshift[crow-30:crow+30, ccol-30:ccol+30] = 0  
    对频谱中心 60×60 的区域置零，中心区域 = 低频，把低频设为 0 → 只剩中高频 → 高通滤波
- 逆shift、逆 Fourier 变换，回到空间域
  
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
img = cv2.imread('lena.bmp',0)
f = np.fft.fft2(img)
fshift = np.fft.fftshift(f)
rows, cols = img.shape
crow,ccol = int(rows/2) , int(cols/2)
fshift[crow-30:crow+30, ccol-30:ccol+30] = 0
ishift = np.fft.ifftshift(fshift)
iimg = np.fft.ifft2(ishift)
iimg = np.abs(iimg)
plt.subplot(121),plt.imshow(img, cmap = 'gray')
plt.title('original'),plt.axis('off')
plt.subplot(122),plt.imshow(iimg, cmap = 'gray')
plt.title('iimg'),plt.axis('off')
plt.show()
```

### 低通（模糊保留轮廓）

- 通过mask实现alpha测试的效果，去除了高频（四周），保留了低频（中心），实际结果是变模糊了

- mask要2通道的，矩形中心部分为1，四周为0，确保src保留中心部分内容
  
    mask = np.zeros((rows, cols, 2), np.uint8)  
    mask[crow-30:crow+30, ccol-30:ccol+30] = 1

- 频率屏蔽使用矩阵相乘（数学意义上的点乘，按 mask 清零），fShift = dftShift * mask
- 把频谱移回原来布局、做逆傅里叶变换、将结果变成真实图像
  
```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('lena.bmp',0)
dft = cv2.dft(np.float32(img),flags = cv2.DFT_COMPLEX_OUTPUT)
dftShift = np.fft.fftshift(dft)
rows, cols = img.shape
crow,ccol = int(rows/2) , int(cols/2)
mask = np.zeros((rows,cols,2),np.uint8)
#两个通道，与频谱图像匹配
mask[crow-30:crow+30, ccol-30:ccol+30] = 1
fShift = dftShift*mask
ishift = np.fft.ifftshift(fShift)
iImg = cv2.idft(ishift)
iImg= cv2.magnitude(iImg[:,:,0],iImg[:,:,1])
plt.subplot(121),plt.imshow(img, cmap = 'gray')
plt.title('original'), plt.axis('off')
plt.subplot(122),plt.imshow(iImg, cmap = 'gray')
plt.title('result'), plt.axis('off')
plt.show()
```

# 模板匹配

此枚举还有其它类型，以下仅案例里使用的

| 案例        | 方法                 | 特点                             |
| --------- | ------------------ | ------------------------------ |
| 单模板匹配平方差  | `TM_SQDIFF`        | 最小值为匹配点，亮度差越小越好，敏感光照变化         |
| 单模板匹配相关系数 | `TM_CCOEFF`        | 最大值为匹配点，考虑均值偏移，对亮度变化更稳健        |
| 多目标匹配     | `TM_CCOEFF_NORMED` | 找出所有匹配度高于阈值的位置，归一化后光照差异影响小，最常用 |


## 单目标

- 用平方差匹配法找到模板（小图，即src）在大图中的位置，两个都要是灰度的，因为模板匹配不支持彩色图直接用平方差

- 获取模板尺寸，th, tw = template.shape[::]，用于绘制找到的位置

- 执行模板匹配，cv2.TM_SQDIFF是匹配方式枚举。输出是结果矩阵，可以转为4角在大图上的坐标，绘制的rv内容显示的是匹配“得分矩阵”，不是图像
  
    rv = cv2.matchTemplate(img, template, cv2.TM_SQDIFF)


```
import cv2
import numpy as np
from matplotlib import pyplot as plt
img = cv2.imread('lena512g.bmp',0)
template = cv2.imread('temp.bmp',0)
th, tw = template.shape[::]
rv = cv2.matchTemplate(img,template,cv2.TM_SQDIFF)
minVal, maxVal, minLoc, maxLoc = cv2.minMaxLoc(rv)
topLeft = minLoc
bottomRight = (topLeft[0] + tw, topLeft[1] + th)
cv2.rectangle(img,topLeft, bottomRight, 255, 2)
plt.subplot(121),plt.imshow(rv,cmap = 'gray')
plt.title('Matching Result'), plt.xticks([]), plt.yticks([])
plt.subplot(122),plt.imshow(img,cmap = 'gray')
# 隐藏坐标轴刻度
plt.title('Detected Point'), plt.xticks([]), plt.yticks([])
plt.show()
```

## 多目标

- 通过设置阈值进行循环匹配，loc是匹配位置的坐标集合 (行索引, 列索引)
  
    loc = np.where(res >= threshold)
- 循环画矩形，  loc[::-1] → 反转顺序 → (列, 行) 对应 (x, y) 坐标，zip(*...) → 遍历每个匹配点

    for pt in zip(*loc[::-1])

```
import cv2
import numpy as np
from matplotlib import pyplot as plt
img = cv2.imread('lena4.bmp',0)
template = cv2.imread('lena4Temp.bmp',0)
w, h = template.shape[::-1] # [::-1] → 反转顺序 → (宽, 高)
res = cv2.matchTemplate(img,template,cv2.TM_CCOEFF_NORMED)
threshold = 0.9
loc = np.where( res >= threshold)
for pt in zip(*loc[::-1]):
    cv2.rectangle(img, pt, (pt[0] + w, pt[1] + h), 255, 1)
plt.imshow(img,cmap = 'gray')
plt.xticks([]), plt.yticks([])
plt.show()
```


# 分割、提取


## 提取简单不连接子物体边界

![](/cv/%E8%8E%B7%E5%8F%96%E8%BE%B9%E7%95%8C.png)

先进行腐蚀（erode）操作，然后计算原图与腐蚀图之间的差，得到边界，但仅适用于简单无连接子物体

- 定义卷积核，核越大，腐蚀效果越强。

    k = np.ones((5,5), np.uint8)
- 腐蚀操作，缩小亮区域（使白色部分变小）

    e = cv2.erode(o, k)
- 图像相减，计算原图与腐蚀图的差值（结果是二值图、仅0和255）。由于腐蚀会让物体边界“往里收缩”，因此 o - e 会突出物体的边缘。
  
    b = cv2.subtract(o, e)
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
o=cv2.imread("rice.png",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
e=cv2.erode(o,k)
b=cv2.subtract(o,e)
plt.subplot(131)
plt.imshow(o)
plt.axis('off')
plt.subplot(132)
plt.imshow(e)
plt.axis('off')
plt.subplot(133)
plt.imshow(b)
plt.axis('off')
plt.show()
```

## 距离变换函数

![](/cv/%E8%B7%9D%E7%A6%BB%E5%8F%98%E6%8D%A2.png)

距离变换对一个二值图像进行处理：对图像中的每个像素，计算它到最近的背景像素（通常是值为 0 的像素）的距离。结果是一张灰度图：越靠近前景中心的像素，距离值越大；靠近边界的值越小；背景像素的距离为 0。因此可以利用它找出物体中心区域。

- 二值化

    ret, thresh = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)

- 开运算去噪

    opening = cv2.morphologyEx(thresh, cv2.MORPH_OPEN, kernel, iterations=2)

- 距离变换

    dist_transform = cv2.distanceTransform(opening, cv2.DIST_L2, 5)

- 对距离变换图做阈值（取较高比例，例如 0.6~0.8 的最大值），只保留峰顶，就能得到 “确定的前景”。max()的目的就是避免边界模糊导致子物体合并

    ret, fore = cv2.threshold(dist_transform, 0.7*dist_transform.max(), 255, 0)

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('water_coins.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
ishow=img.copy()
ret, thresh = cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)
kernel = np.ones((3,3),np.uint8)
opening = cv2.morphologyEx(thresh,cv2.MORPH_OPEN,kernel, iterations = 2)
dist_transform = cv2.distanceTransform(opening,cv2.DIST_L2,5)
ret, fore = cv2.threshold(dist_transform,0.7*dist_transform.max(),255,0)
plt.subplot(131)
plt.imshow(ishow)
plt.axis('off')
plt.subplot(132)
plt.imshow(dist_transform)
plt.axis('off')
plt.subplot(133)
plt.imshow(fore)
plt.axis('off')
plt.show()
```

## 未知区域

![](/cv/%E7%A1%AE%E5%AE%9A%E6%9C%AA%E7%9F%A5%E5%8C%BA%E5%9F%9F.png)

在现实图像中，物体边缘部分可能既不是明显前景，也不是明显背景，如果直接用 markers = fore + bg，边缘区域可能被错误地标记成前景或背景。这会导致分水岭算法划分不准确，物体边界不清晰。
可理解为前景与背景的交界处，至于要作为前景还是背景则由用户来决定。
未知区域：unknown = bg − fore

- fore（白色核心）：物体中心 → 肯定是前景
- bg（膨胀背景）：明显背景 → 肯定是背景
- unknown（边缘区域）：既不是核心，也不是背景 → 等待算法自己判定

从结果来看unknown都是环状的，且通过subtract得到的是个二值图，元素值只有0和255

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('water_coins.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
ishow=img.copy()
ret, thresh = cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)
kernel = np.ones((3,3),np.uint8)
opening = cv2.morphologyEx(thresh,cv2.MORPH_OPEN,kernel, iterations = 2)
# 膨胀得到绝对背景区域
bg = cv2.dilate(opening,kernel,iterations=3)
dist = cv2.distanceTransform(opening,cv2.DIST_L2,5)
ret, fore = cv2.threshold(dist,0.7*dist.max(),255,0)
fore = np.uint8(fore)
un = cv2.subtract(bg,fore)
plt.subplot(221)
plt.imshow(ishow)
plt.axis('off')
plt.subplot(222)
plt.imshow(bg)
plt.axis('off')
plt.subplot(223)
plt.imshow(fore)
plt.axis('off')
plt.subplot(224)
plt.imshow(un)
plt.axis('off')
plt.show()
```

## 标注前景对象

![](/cv/%E6%A0%87%E6%B3%A8.png)

可理解为通过此方法获取每个前景连通组件一个唯一的整数标签，比如位置，序号等等

ret, markers = cv2.connectedComponents(二值图fore)

- markers：与原图同大小（二维数组），每个像素的值表示所属组件，背景像素 = 0，第一个前景连通区域 = 1，第二个前景连通区域 = 2
- ret：连通组件总数 包括背景，例如，如果图中有 5 个硬币，ret 会返回 6（背景 + 5 个前景区域）

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('water_coins.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
ishow=img.copy()
ret, thresh = cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)
kernel = np.ones((3,3),np.uint8)
opening = cv2.morphologyEx(thresh,cv2.MORPH_OPEN,kernel, iterations = 2)
sure_bg = cv2.dilate(opening,kernel,iterations=3)
dist_transform = cv2.distanceTransform(opening,cv2.DIST_L2,5)
ret, fore = cv2.threshold(dist_transform,0.7*dist_transform.max(),255,0)
fore = np.uint8(fore)
ret, markers = cv2.connectedComponents(fore)
plt.subplot(131)
plt.imshow(ishow)
plt.axis('off')
plt.subplot(132)
plt.imshow(fore)
plt.axis('off')
plt.subplot(133)
plt.imshow(markers)
plt.axis('off')
print(ret)
plt.show()
```

## 调整标注结果

![](/cv/%E7%BB%98%E5%88%B6%E4%B8%BA%E6%AD%A2%E5%8C%BA%E5%9F%9F.png)

- 标注前景
  
  ret, markers1 = cv2.connectedComponents(fore)  
  markers1：直接给每个连通组件一个标签（0 背景，1、2、… 前景），可以理解为最基础的 前景标记图

- 计算未知区域，unknown = 背景 - 前景核心。结果是边缘不确定区域（既不是核心前景，也不是肯定背景）。这一步是为 分水岭算法准备 markers 的标准做法

    foreAdv = fore.copy()  
    unknown = cv2.subtract(sure_bg, foreAdv)

- 再次标注后调整内容，markers2 + 1的作用是将二维数组里的每个值都加一，因为背景要置1，前景要从2开始，0用于未知区域

    ret, markers2 = cv2.connectedComponents(foreAdv)  
    markers2 = markers2 + 1  

- 通过unknown==255创建布尔掩码二维数组（unknown里值为255的元素为t，0为f），用布尔掩码选中markers2中对应像素（对应元素为t的被选中），设置为0

    markers2[unknown==255] = 0

结果：0是未知、1是背景、>=2是前景，作用是用于分割的参数（见cv2.watershed案例）

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('water_coins.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
ishow=img.copy()
ret, thresh = cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)
kernel = np.ones((3,3),np.uint8)
opening = cv2.morphologyEx(thresh,cv2.MORPH_OPEN,kernel, iterations = 2)
sure_bg = cv2.dilate(opening,kernel,iterations=3)
dist_transform = cv2.distanceTransform(opening,cv2.DIST_L2,5)
ret, fore = cv2.threshold(dist_transform,0.7*dist_transform.max(),255,0)
fore = np.uint8(fore)
ret, markers1 = cv2.connectedComponents(fore)
foreAdv=fore.copy()
unknown = cv2.subtract(sure_bg,foreAdv)
ret, markers2 = cv2.connectedComponents(foreAdv)
markers2 = markers2+1
markers2[unknown==255] = 0
plt.subplot(121)
plt.imshow(markers1)
plt.axis('off')
plt.subplot(122)
plt.imshow(markers2)
plt.axis('off')
plt.show()
```

## 分水岭 cv2.watershed

![](/cv/%E5%88%86%E6%B0%B4%E5%B2%AD.png)

- 用于未知区域的最终确定，判断是属于前景还是分割线
- 入参markers里的0是未知、1是背景、>=2是前景，出参就会将0的值进行改写为边界-1、或是前景或背景值
  
    markers = cv2.watershed(img, markers)  

- 通过markers == -1创建布尔掩码二维数组（markers里值为-1的元素为t，0为f），用布尔掩码选中img中对应像素（对应元素为t的被选中），设置为绿色用于绘制

    img[markers == -1] = [0,255,0]

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
img = cv2.imread('water_coins.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
img=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
ishow=img.copy()
ret, thresh = cv2.threshold(gray,0,255,cv2.THRESH_BINARY_INV+cv2.THRESH_OTSU)
kernel = np.ones((3,3),np.uint8)
opening = cv2.morphologyEx(thresh,cv2.MORPH_OPEN,kernel, iterations = 2)
sure_bg = cv2.dilate(opening,kernel,iterations=3)
dist_transform = cv2.distanceTransform(opening,cv2.DIST_L2,5)
ret, sure_fg = cv2.threshold(dist_transform,0.7*dist_transform.max(),255,0)
sure_fg = np.uint8(sure_fg)
unknown = cv2.subtract(sure_bg,sure_fg)
ret, markers = cv2.connectedComponents(sure_fg)
markers = markers+1
markers[unknown==255] = 0
markers = cv2.watershed(img,markers)
img[markers == -1] = [0,255,0]
plt.subplot(121)
plt.imshow(ishow)
plt.axis('off')
plt.subplot(122)
plt.imshow(img)
plt.axis('off')
plt.show()
```

## GrabCut 前景分割

算法原理：基于 GMM（高斯混合模型）+ 图割，算法会迭代更新 mask，把前景和背景分开

| 初始化方式    | 精度 | 操作难度 | 前景复杂度适应性 | 使用场景               |
| -------- | -- | ---- | -------- | ------------------ |
| 无 mask   | 低  | 简单   | 差        | 前景很明显或辅助 mask/rect |
| mask 是图片 | 高  | 较高   | 好        | 前景复杂，需要精确分割        |
| mask 是矩形 | 中  | 简单   | 中        | 前景大致规则，快速分割        |


### 无mask
此案例比较简单，分割效果不够好，仅用于演示函数作用

![](/cv/%E5%89%8D%E6%99%AF%E5%88%86%E5%89%B21.png)

- cv2.grabCut(o, mask, rect, bgdModel, fgdModel, 5, cv2.GC_INIT_WITH_RECT)

    参数说明：
    - o → 输入图像
    - mask → 同图片大小，初始化为0，被算法标记每个像素是前景还是背景
    - rect → 输入的粗略的前景矩形
    - bgdModel / fgdModel → 固定为 np.zeros((1,65), np.float64)
    - 5 → 迭代次数
    - cv2.GC_INIT_WITH_RECT → 迭代模式

    结果mask的标记值：

    - 0 = 确定背景
    - 1 = 确定前景
    - 2 = 可能背景
    - 3 = 可能前景
  
- mask2 = np.where((mask==2)|(mask==0), 0, 1).astype('uint8')

    把 GrabCut 输出的 mask 转为只有1前景、0背景的二值图，规则：
    - 将确定/可能背景（0,2）设为 0
    - 将确定/可能前景（1,3）设为 1
    - mask2 就可以直接用来提取前景的掩码

- ogc = o * mask2[:, :, np.newaxis]

    mask2[:,:,np.newaxis] → 将二维 mask 扩展成三通道  
    与原图逐元素相乘 → 得到只保留前景的图像，其余背景为 0

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
o = cv2.imread('lenacolor.png')
orgb=cv2.cvtColor(o,cv2.COLOR_BGR2RGB)
mask = np.zeros(o.shape[:2],np.uint8)
bgdModel = np.zeros((1,65),np.float64)
fgdModel = np.zeros((1,65),np.float64)
rect = (50,50,400,400)
cv2.grabCut(o,mask,rect,bgdModel,fgdModel,5,cv2.GC_INIT_WITH_RECT)
mask2 = np.where((mask==2)|(mask==0),0,1).astype('uint8')
ogc = o*mask2[:,:,np.newaxis]
ogc=cv2.cvtColor(ogc,cv2.COLOR_BGR2RGB)
plt.subplot(121)
plt.imshow(orgb)
plt.axis('off')
plt.subplot(122)
plt.imshow(ogc)
plt.axis('off')
plt.show()
```

### 加载mask图

![](/cv/%E5%89%8D%E6%99%AF%E5%88%86%E5%89%B22.png)

- 加载掩码图，mask2 作为手动标注的前景/背景辅助，0 → 背景，255 → 前景
  
    mask2 = cv2.imread('mask.png',0)      # 灰度  

- 更新 mask，将用户 mask 信息合并到 GrabCut 的 mask，0 = 背景，1 = 前景

    mask[mask2 == 0] = 0  
    mask[mask2 == 255] = 1

- 使用 mask 初始化 GrabCut 再次迭代，使用 cv2.GC_INIT_WITH_MASK，算法根据已有 mask 再优化前景分割

    mask, bgd, fgd = cv2.grabCut(o, mask, None, bgd, fgd, 5, cv2.GC_INIT_WITH_MASK)

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
o = cv2.imread('lenacolor.png')
orgb=cv2.cvtColor(o,cv2.COLOR_BGR2RGB)
mask = np.zeros(o.shape[:2],np.uint8)
bgd = np.zeros((1,65),np.float64)
fgd = np.zeros((1,65),np.float64)
rect = (50,50,400,500)
cv2.grabCut(o,mask,rect,bgd,fgd,5,cv2.GC_INIT_WITH_RECT)
mask2 = cv2.imread('mask.png',0)
mask2Show = cv2.imread('mask.png',-1)
m2rgb=cv2.cvtColor(mask2Show,cv2.COLOR_BGR2RGB)
mask[mask2 == 0] = 0
mask[mask2 == 255] = 1
mask, bgd, fgd = cv2.grabCut(o,mask,None,bgd,fgd,5,cv2.GC_INIT_WITH_MASK)
mask = np.where((mask==2)|(mask==0),0,1).astype('uint8')
ogc = o*mask[:,:,np.newaxis]
ogc=cv2.cvtColor(ogc,cv2.COLOR_BGR2RGB)
plt.subplot(121)
plt.imshow(m2rgb)
plt.axis('off')
plt.subplot(122)
plt.imshow(ogc)
plt.axis('off')
plt.show()
```

### mask是矩形


![](/cv/%E5%89%8D%E6%99%AF%E5%88%86%E5%89%B23.png)
- 初始化 mask2（自定义前景/背景），mask2 初始全 0 → 确定背景

    mask2 = np.zeros(o.shape[:2], np.uint8)  
    mask2[30:512,50:400] = 3  对行 30~511 和列 50~399 区域赋值为可能前景 
    mask2[50:300,150:200] = 1  设定 确定前景  
    这样就定义了一个粗略的前景区域（1）和更大的可能前景区域（3）

```
import numpy as np
import cv2
import matplotlib.pyplot as plt
o = cv2.imread('lenacolor.png')
orgb=cv2.cvtColor(o,cv2.COLOR_BGR2RGB)
bgd = np.zeros((1,65),np.float64)
fgd = np.zeros((1,65),np.float64)
mask2 = np.zeros(o.shape[:2],np.uint8)
mask2[30:512,50:400]=3
mask2[50:300,150:200]=1
cv2.grabCut(o,mask2,None,bgd,fgd,5,cv2.GC_INIT_WITH_MASK)
mask2 = np.where((mask2==2)|(mask2==0),0,1).astype('uint8')
ogc = o*mask2[:,:,np.newaxis]
ogc=cv2.cvtColor(ogc,cv2.COLOR_BGR2RGB)
plt.subplot(121)
plt.imshow(orgb)
plt.axis('off')
plt.subplot(122)
plt.imshow(ogc)
plt.axis('off')
plt.show()
```
