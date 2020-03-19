# nowatermark

[![PyPI Version](https://img.shields.io/pypi/v/nowatermark.svg)](https://pypi.python.org/pypi/nowatermark)
[![Build Status](https://img.shields.io/travis/SixQuant/nowatermark/master.svg)](https://travis-ci.org/SixQuant/nowatermark)
[![Wheel Status](https://img.shields.io/badge/wheel-yes-brightgreen.svg)](https://pypi.python.org/pypi/nowatermark)
[![Coverage report](https://img.shields.io/codecov/c/github/SixQuant/nowatermark/master.svg)](https://codecov.io/github/SixQuant/nowatermark?branch=master)
[![Powered by SixQuant](https://img.shields.io/badge/powered%20by-SixQuant-orange.svg?style=flat&colorA=E1523D&colorB=007D8A)](https://sixquant.cn)

## Overview
Automatically find and remove the corresponding watermark in the picture according to the picture of the watermark template.


## Install

### Mac OS Install OpenCV for Python3

- with-python3 is used to tell brew to make opencv support python3,
- C ++ 11 is used to tell brew to provide c ++ 11 support,
- with-contrib is used to install opencv's contrib support.

```bash
$ brew install opencv3 --without-python --with-python3 --c++11 --with-contrib  
```

### Windows & Linux Installation

```bash
pip3 install opencv-python
```

Verifying the installation：

```python
import cv2
print(cv2.__version__)
```

If you got this error: "ImportError: No module named 'cv2'", then your symlink might be corrupted, you need to link your opencv to python site-packages:
```bash
$ brew link --force opencv3
```

### Install nowatermark (universal across all platforms)
```bash
$ pip3 install nowatermark
```

## Usage

```python
from nowatermark import WatermarkRemover

path = './data/'

watermark_template_filename = path + 'anjuke-watermark-template.jpg'
remover = WatermarkRemover()
remover.load_watermark_template(watermark_template_filename)

remover.remove_watermark(path + 'anjuke3.jpg', path + 'anjuke3-result.jpg')
remover.remove_watermark(path + 'anjuke4.jpg', path + 'anjuke4-result.jpg')

```

---

### Original
![Original](https://github.com/SixQuant/nowatermark/blob/master/data/anjuke2.jpg)

### Removed watermark
![Removed watermark](https://github.com/SixQuant/nowatermark/blob/master/data/anjuke2-result.jpg)

---

## Procedure

### Feature Matching
* Initialized the watermark template image, such as removing non-text parts after binarization, etc.
* Tried multiple algorithms of OpenCV
* For example ORB + Brute-Force, that is brute force matching, corresponding to the cv2.BFMatcher () method
* For example, SIFT + FLANN, namely fast nearest neighbor matching, corresponding to the cv2.BFMatcher () method
* For example, Template Matching, that is, template matching, corresponding to cv2.matchTemplate ()
* In the end, Template Matching was the easiest and most convenient.
* If the watermark position is fixed, you can skip Feature Matching and go directly to the next Inpainting (picture repair)

[MIT](https://tldrlegal.com/license/mit-license)
