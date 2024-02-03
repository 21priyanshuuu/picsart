# picsart
#a opencv project to convert any picture into painting
#fixing resizing image
#removing impurities
#bilateral image filtering
#sharpning the image

import cv2
import numpy as np

img=cv2.imread('nature.jpg')

motionBlur=cv2.medianBlur(img,5)
motionBlur=cv2.medianBlur(motionBlur,1)
motionBlur=cv2.medianBlur(motionBlur,1)
motionBlur=cv2.edgePreservingFilter(motionBlur,sigma_s=5)


kernalBlur=cv2.GaussianBlur(motionBlur,(25,25),2)
bilateralBlur=cv2.bilateralFilter(motionBlur,10,5,10)
bilateralBlur=cv2.bilateralFilter(bilateralBlur,10,5,10)
bilateralBlur=cv2.bilateralFilter(bilateralBlur,1,50,1)
bilateralBlur=cv2.bilateralFilter(bilateralBlur,3,40,3)




guass=cv2.GaussianBlur(bilateralBlur,(5,5),2)
sharp1=cv2.addWeighted(bilateralBlur,1.5,guass,-0.5,1)


# cv2.imshow('blur',motionBlur)
cv2.imshow('og',img)
# cv2.imshow('bilateral',bilateralBlur)

cv2.imshow('addwei',sharp1)

cv2.waitKey(0)
cv2.destroyAllWindows()
