---
layout: post
title: Tranformasi Hough untuk deteksi garis lurus dan lingkaran
excerpt: "Praktikum PPCD 9"
tags: [sample post, code, highlighting]
modified: 2015-11-24
comments: true
---

Hough Transform adalah suatu metode untuk mendeteksi garis , lingkaran , atau bentuk lainya.Dasar dari Hough transform adalah transformasi garis, yang mana digunakan untuk mencari garis lurus pada citra biner.Pada Hough line transform digunakan titik-titik pada citra biner sebagai bagian dari himpunan kemungkinan garis.Titik pada tiap garis direpresentasikan sebagai titik koordinat polar(rho,theta).Persamaan untuk tiap garis adalah `rho = x cos theta + y sin theta`.

### Source Code Python

{% highlight python%}
import cv2
import numpy as np

img = cv2.imread('dor.jpg')
gray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(gray,50,150,apertureSize = 3)
minLineLength = 100
maxLineGap = 10
lines = cv2.HoughLines(edges,1,np.pi/180,100,minLineLength,maxLineGap)
for x1,y1,x2,y2 in lines[0]:
    cv2.line(img,(x1,y1),(x2,y2),(0,255,0),2)

cv2.imwrite('houghlines5.jpg',img)
cv2.imshow('hough trans', img)
cv2.imshow('canny',edges)
cv2.waitKey(0)                 # Waits forever for user to press any key
cv2.destroyAllWindows()
{% endhighlight %}

Selain untuk mendeteksi garis, pada Hough transform juga terdapat metode untuk mendetesi lingkaran pada citra.Hough transfrom untuk lingkaran membutuhkan penggunaan memori yanglebih daripada Line Hough Transfrom, karena pada metode ini digunakan parameter tambahan yaitu titik radius. Oleh karena itu, digunakan trik untuk mengatasi masalah tersebut yaitu memanggil method `CV_HOUGH_GRADIENT` dari library opencv.

###Source Code Hough Circle
{% highlight python %}
import cv2
import cv2.cv
import numpy as np

img = cv2.imread('images.png',0)
img = cv2.medianBlur(img,5)
cimg = cv2.cvtColor(img,cv2.COLOR_GRAY2BGR)

circles = cv2.HoughCircles(img,cv2.cv.CV_HOUGH_GRADIENT,1,20,
                            param1=50,param2=30,minRadius=0,maxRadius=0)

circles = np.uint16(np.around(circles))
for i in circles[0,:]:
    # draw the outer circle
    cv2.circle(cimg,(i[0],i[1]),i[2],(0,255,0),2)
    # draw the center of the circle
    cv2.circle(cimg,(i[0],i[1]),2,(0,0,255),3)

cv2.imshow('detected circles',cimg)
cv2.waitKey(0)
cv2.destroyAllWindows()
{% endhighlight %}


