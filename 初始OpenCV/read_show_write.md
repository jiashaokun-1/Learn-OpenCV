## 图片的读 显 存
`cv.imread()`, `cv.imshow()`, `cv.imwrite()` 三个方法分别对应图片的读，显示，另存为。
- 读
```py
import numpy as np
import cv2 as cv
# Load a color image in grayscale
img = cv.imread('messi5.jpg',0)  # 第二个参数可取1,0,-1三个值，分别代表以彩色图、灰度值、包含alpha通道的方式读取图片
```
- 显示 与 存写
```py
cv.imshow("image", img)  # 第一个参数是给显示图片的窗口起名， 第二个参数是图片
k = cv.waitKey(0)  # 等待按键时间，键盘按下或时间结束时，图片窗口关闭
if k == ord('s'):
    cv.imwrite("first_save_img.png", img)  # 将img另存在当前工作目录下
cv.destroyAllWindows()  # 关闭所有图片窗口， 或可使用cv.destroyWindow(Window_name)关闭指定窗口
```

## matplotlib的运用
```py
img = cv.imread('messi5.jpg',0)
plt.imshow(img, cmap = 'gray', interpolation = 'bicubic')
plt.xticks([]), plt.yticks([])  # to hide tick values on X and Y axis
plt.show()
```
