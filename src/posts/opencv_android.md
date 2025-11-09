---
layout: "post.njk"
title: "OpenCV on Android: practices and tips"
date: 2018-03-08
tags:
    - android
    - computer vision
---

# Transfer Mat objects from Android to NDK

The main idea is to use the address of a Mat object in order to manipulate
the data.

Basically, we have a function acting as a bridge between Java APIs and NDK:

```java
public native void function_name(long matAddress);
```

To call the function, we use Mat's address by calling `getNativeObjAddr()`.
All computations in NDK will affect the content of Mat in both Java and
NDK layers.

In the NDK code, to use `cv::Mat` object regarding `java Mat`, we can use
`static_cast`:

```cpp
Mat& im = *(static_cast<Mat*>(addrImg));
```

## Notes

There is a huge difference in image channels between `Java OpenCV` and `NDK OpenCV`.
When we decode the path or file to a bitmap in Java, we have to convert
the bitmap to `ARGB_8888` color channel, otherwise it does not work. Actually,
it also can work on `RGB_565` but for some reasons I cannot remember, I always
use `ARGB_8888` in the project.

```java
Bitmap bm32_image = bm.copy(Bitmap.Config.ARGB_8888, true);
```

To manipulate the image correctly in NDK, we should convert it to the normal
RGB channel, otherwise sometimes we get some bugs that are frustrating.

```java
// convert ARGB_8888 to RGB
Mat im = new Mat();
Mat rgb_im = new Mat();
Utils.bitmapToMat(bm32_image, im);
Imgproc.cvtColor(im, rgb_im, Imgproc.COLOR_RGBA2RGB, 3);

function_name(rgb_im.getNativeObjAddr());
```

Another practice is to put some assertions in NDK code to make sure that we
use the correct format for the input.

# OpenCV's Camera

OpenCV supports 3 types of camera:

- `CameraBridgeViewBase`.
- `JavaCameraView`.
- `CameraSurfaceGLView`.

## JavaCameraView

1. Create the layout of the camera. For example, we can put the following lines
to the Activity xml file:

```xml
<org.opencv.android.JavaCameraView
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    android:id="@+id/opencvcamera_view"
></org.opencv.android.JavaCameraView>
```

2. Next, in the activity which controls the camera, we have to implement
required methods from the `CvCameraViewListener2`. The 3 methods are:

- `onCameraViewStarted`.
- `onCameraViewStopped`.
- `onCameraFrame`.

Prior to processing the camera, we need to initialize the variable holding
callbacks of the three aforementioned methods:

```java
private CameraBridgeViewBase mOpenCVCamera;
```

In the `onCreate` method:

```java
mOpenCVCamera = (CameraBridgeViewBase) findViewById(R.id.opencvcamera_view);
mOpenCVCamera.setVisibility(CameraBridgeViewBase.VISIBLE);
mOpenCVCamera.setCvCameraViewListener(this);
```

Next, we implement the 3 required methods:

```java
@Override
public void onCameraViewStarted(int width, int height) {
    // initialize images, variables, settings
}

@Override
public void onCameraViewStopped() {
    // release the resources
}

@Override
public Mat onCameraFrame(CameraBridgeViewBase.CvCameraViewFrame inputFrame) {
    // retrieve the frame from `inputFrame`
    // - the grayscale frame by inputFrame.gray()
    // - the RGBA frame by inputFrame.rgba()
    Mat im = inputFrame.rgba();

    // do things
    // postprocess: convert back to the RGBA image
    return im; // `im` will show in the UI
}
```

Note that OpenCV's Camera is not able to set the portrait orientation. One workaround
is to set the Activity to `landscape` by putting the following line inside the `Activity`
tag in `AndroidManifest.xml`:

```xml
android:screenOrientation="landscape"
```

# Data Manipulation

### `unsigned char` Mat

It is troublesome when we want to assign a value of 255 to an `unsigned char` Mat
because Java does not support `unsigned char` as a primitive type.
One workaround is to allocate a `CV_16S` Mat, manipulate that matrix, and
finally convert to `CV_8U`.

### Point2f and Point

To convert `MatOfPoint` to `MatOfPoint2f`, we use the constructor:

```java
MatOfPoint matofpoint = new MatOfPoint(matofpoint2f.toArray());
```

## Accessing the pixel values

In order to retrieve and assign pixel values, we use the getter/setter from `Mat`.

```java
short[] pixel = new short[nchannels];

m.get(i, j, pixel); // retrieve pixel values at (i, j)
// in this example, the pixel has 3 channels
pixel[0] = 255;
pixel[1] = 0;
pixel[2] = 125;
m.set(i, j, pixel);
