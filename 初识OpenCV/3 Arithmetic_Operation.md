## Image Adding
@TODO
## Image Blending
@TODO
## Bitwise Operations
This includes the bitwise AND, OR, NOT, and XOR operations.They will be highly useful while extracting any part of the image, defining and working with non-rectangular ROI's, and etc.  
** 案例 **：将图一中除背景外的部分粘贴到图二中，思路如下：
- 在图二中锁定图一将要粘贴的整块区域，成为目标区域ROI
- 将图一转化为灰度图 `cv.cvtColor(img2,cv.COLOR_BGR2GRAY)`
- 将灰度图转化为二值图：二值图可用做掩码图，用来区分背景和内容 `ret, mask = cv.threshold(srcIMG, threshold, maval, cv.THRESH_BINARY)`
- 在图二中，利用掩码图的invert取出目标区域的背景来，记作：ROI2 `cv.bitwise_and(roi,roi,mask = mask_inv)`
- 在图一中，利用掩码图取出图一的内容来，记作：ROI1 `cv.bitwise_and(img2,img2,mask = mask)`
- 将ROI1与ROI2进行算数加 `cv.add(img1_bg,img2_fg)`
- 最后，利用相加后的结果修改图二的ROI部分的内容
```py
# Load two images
img1 = cv.imread('messi5.jpg')
img2 = cv.imread('opencv-logo-white.png')
# I want to put logo on top-left corner, So I create a ROI
rows,cols,channels = img2.shape
roi = img1[0:rows, 0:cols]
# Now create a mask of logo and create its inverse mask also
img2gray = cv.cvtColor(img2,cv.COLOR_BGR2GRAY)
ret, mask = cv.threshold(img2gray, 10, 255, cv.THRESH_BINARY)
mask_inv = cv.bitwise_not(mask)
# Now black-out the area of logo in ROI
img1_bg = cv.bitwise_and(roi,roi,mask = mask_inv)
# Take only region of logo from logo image.
img2_fg = cv.bitwise_and(img2,img2,mask = mask)
# Put logo in ROI and modify the main image
dst = cv.add(img1_bg,img2_fg)
img1[0:rows, 0:cols ] = dst
cv.imshow('res',img1)
cv.waitKey(0)
cv.destroyAllWindows()

```
