---
layout: post
title: "Transformasi Citra menjadi grayscale dengan opencv python"
author: Gusti Bimo
modified:
excerpt: "Praktikum PPCD 1"
tags: []
---

Halo,ini adalah postingan pertama saya,kali ini saya ingin berbagi apa yang sejauh ini pelajari tentang pengolahan citra digital menggunakan library Opencv. Setelah membaca membaca dokumentasi opencv dan melihat tutorial yang diberikan oleh asisten praktikum, saya ingin mencoba praktekan sendiri tentang bagaimana cara mengubah citra RGB menjadi citra grayscale.Bahasa pemrograman yang saya gunakan adalah python, berikut saya tamplikan source code nya:

{% highlight python %}
# Konversi RGB ke Grayscale
import cv2

image = cv2.imread("haha.jpg")
gray= cv2.cvtColor(image,cv.COLOR_BGR2GRAY) # konversi RGB ke Grayscale menggunakan library opencv
cv2.imwrite("gray.jpg", gray)
cv2.imshow('color_image',image)
cv2.imshow('grayimage',gray) 
cv2.waitKey(0)                 
cv2.destroyAllWindows()       
{% endhighlight %}

{% highlight python %}
author: Gusti Bimo
{% endhighlight %}
