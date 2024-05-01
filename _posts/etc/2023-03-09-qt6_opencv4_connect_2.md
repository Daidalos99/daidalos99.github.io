---
layout: post
title: Qt6(6.4.2)와 OpenCV4(4.7.0) 연동하기 - 2
date:   2023-03-09
excerpt: QT6와 OpenCV4를 연동해 보았다.
categories: [etc]
comments: true
---
Qt6(6.4.2)와 OpenCV4(4.7.0) 연동하기 - 2
---

앞의 포스트에 이어서 이제 몇가지 설정만 더 해주면 Qt6에서 OpenCV4를 사용할 수 있다.
거의 다 왔다. 조금만 더 힘내자!!
이번 게시물도 앞에서 나온 [Qt Wiki](https://wiki.qt.io/How_to_setup_Qt_and_openCV_on_Windows)의 방법과 거의 비슷하다. 앞에서도 말했지만, 위 링크에서는 Qt5와 OpenCV3 버전을 쓰므로 Qt6 + OpenCV4의 조합을 사용하는 나의 방법과 유사하지만, 조금 다르다는 것을 알고 보자.

이전에 설치한 Qt Creator(나의 경우 Qt 6.4.2를 사용하기 떄문에 Creator는 9.0.2)를 실행한다. 이제 Create Project를 한다. 다음과 같이 설정하면 된다.
![img1](/assets/img/etc/qt6_opencv4_connect_2/qt_widgets_application.png)

프로젝트 생성 시 'Qt Widgets Application'을 선택한다.
그 다음 제목과 경로를 설정해주고, 'Next'를 누른다.

다음으로, Build System을 설정하는데 여기서 'CMake'가 아닌 '**qmake**'로 설정을 해준다. 이렇게 해야 **.pro** 파일이 생기고, 거기에 OpenCV관련 전처리구문을 넣어줄 수 있다. .pro파일은 Qt Creator의 프로젝트파일이다. .pro파일에 대한 자세한 설명은 [생짜님의 블로그 게시물](https://saengjja.tistory.com/145)을 통해 확인할 수 있다.
![img2](/assets/img/etc/qt6_opencv4_connect_2/qmake.png)

Next를 누르면서 프로젝트 개인설정을 해주고, Kit Selection에서 컴파일러를 골라준다. 나의 경우는 'Desktop Qt 6.4.2 MinGW 64-bit'를 선택하고 'Next'를 눌러주었다.
![img3](/assets/img/etc/qt6_opencv4_connect_2/kit_selection.png)

이제 프로젝트와 소스파일이 생성되었을텐데 우리는 여기서 '제목.pro' 파일과 'mainwindow.cpp' 파일을 건드려줄 것이다. 

'제목.pro' 파일은 기존의 내용을 아래와 같은 내용으로 덮어씌운다.
Qt Wiki에 나오는 내용이지만, 내가 설치한 경로와 버전에 맞춰서 코드를 조금씩 수정하였다. 
또한, LIBS+= 하면서 추가할때, Wiki예제는 OpenCV3.2.0을 사용하지만, 나는 OpenCV4.7.0을 사용할 것이기에, 동적 라이브러리 파일(.dll) 뒷부분의 320을 470으로 바꿔주었다.

``` c++
    #-------------------------------------------------
    #
    # Project created by QtCreator 2017-03-05T12:30:06
    #
    #-------------------------------------------------

    QT       += core gui

    greaterThan(QT_MAJOR_VERSION, 4): QT += widgets

    TARGET = opencvtest
    TEMPLATE = app

    # The following define makes your compiler emit warnings if you use
    # any feature of Qt which as been marked as deprecated (the exact warnings
    # depend on your compiler). Please consult the documentation of the
    # deprecated API in order to know how to port your code away from it.
    DEFINES += QT_DEPRECATED_WARNINGS

    # You can also make your code fail to compile if you use deprecated APIs.
    # In order to do so, uncomment the following line.
    # You can also select to disable deprecated APIs only up to a certain version of Qt.
    #DEFINES += QT_DISABLE_DEPRECATED_BEFORE=0x060000    # disables all the APIs deprecated before Qt 6.0.0


    SOURCES += main.cpp\
            mainwindow.cpp

    HEADERS  += mainwindow.h

    FORMS    += mainwindow.ui

    INCLUDEPATH += C:\opencv\build\include

    LIBS += C:\opencv-build\bin\libopencv_core470.dll
    LIBS += C:\opencv-build\bin\libopencv_highgui470.dll
    LIBS += C:\opencv-build\bin\libopencv_imgcodecs470.dll
    LIBS += C:\opencv-build\bin\libopencv_imgproc470.dll
    LIBS += C:\opencv-build\bin\libopencv_features2d470.dll
    LIBS += C:\opencv-build\bin\libopencv_calib3d470.dll

    # more correct variant, how set includepath and libs for mingw
    # add system variable: OPENCV_SDK_DIR=D:/opencv/opencv-build/install
    # read http://doc.qt.io/qt-5/qmake-variable-reference.html#libs

    #INCLUDEPATH += $$(OPENCV_SDK_DIR)/include

    #LIBS += -L$$(OPENCV_SDK_DIR)/x86/mingw/lib \
    #        -lopencv_core320        \
    #        -lopencv_highgui320     \
    #        -lopencv_imgcodecs320   \
    #        -lopencv_imgproc320     \
    #        -lopencv_features2d320  \
    #        -lopencv_calib3d320
```

'mainwindow.cpp' 파일은 아래와 같이 대체한다.
``` c++
    #include "mainwindow.h"
    #include "ui_mainwindow.h"

    #include <opencv2/core/core.hpp>
    #include <opencv2/highgui/highgui.hpp>

    MainWindow::MainWindow(QWidget *parent) :
        QMainWindow(parent),
        ui(new Ui::MainWindow)
    {
        ui->setupUi(this);

        // read an image
        cv::Mat image = cv::imread("C://1.jpg", 1);
        // create image window named "My Image"
        cv::namedWindow("My Image");
        // show the image on window
        cv::imshow("My Image", image);
    }

    MainWindow::~MainWindow()
    {
        delete ui;
    }
```

'C:\1.jpg'라는 이미지를 띄우는 예제 코드이므로, 나는 'C:\\'에다가 '1.jpg'를 넣어주었다.

![img4](/assets/img/etc/qt6_opencv4_connect_2/my_image.png)

오... 된다!! 

이로써 Qt6에 OpenCV4 연동하기를 마친다.

이 글을 따라하셔서 잘 되셨다면, 혹은 잘 안되었더라도 댓글 한번씩만 남겨주시면 감사하겠습니다.