# Purpose

현재 Jetson과 ZED를 사용하여 비전 인식을 해야하는 Task가 주어져 있고 Strero Camera인 ZED2를 비전 인식에 활용하기 위한 방법을 찾아야 한다. ZED2는 SDK 및 API 위한 Document와 예제 코드를 제공하므로, 코드를 익히면서 Vision 인식을 위해 SDK에서 사용해야하는 기능들을 찾아본다.

# ZED SDK 설치

ZED SDK는 Strerolabs 사이트([Link](https://www.stereolabs.com/developers/release/))에서 다운로드 받을 수 있다. Cuda 와 OS 버전에 따라 다운로드 받을 파일이 달라지니 미리 Cuda와 OS 정보를 찾은 후 다운로드를 진행해야 한다. Cuda가 없으면 다운로드([Link](https://developer.nvidia.com/cuda-downloads)) 받는다.

SDK를 다운로드 받으면 .run 파일을 실행시켜야 한다. .run file을 실행시키기 위한 명령어는 다음과 같다.

```
sudo su ".run file"
```

하지만 실행이 안되는 경우가 발생하는데, 실행 권한을 줌으로써 run 파일을 실행할 수 있다.

```
chmod a+x ".run flie"
```

# Python API 설치

SDK 설치 이후, 적용할 언어에 따라 API를 다르게 설치해야 한다. C++, Python을 적용할 수 있는데 Python API를 설치하기로 하였다. Strerolabs GitHub([Link](https://github.com/stereolabs))에서 설치 방법을 찾아볼 수 있는데, Python API는 zed-python-api [(Link)](https://github.com/stereolabs/zed-python-api)에 방법이 있다. 

Python API를 설치하기 위해서 필요한 필수 조건(Prerequisites)는 다음과 같다.

- [ZED SDK 3.1](https://www.stereolabs.com/developers/) and its dependency [CUDA](https://developer.nvidia.com/cuda-downloads)
- Python 3.5+ x64 (3.7 recommended, [Windows installer](https://www.python.org/ftp/python/3.7.6/python-3.7.6-amd64.exe))
- [Cython 0.28](http://cython.org/#download)
- [Numpy 1.13](https://www.scipy.org/scipylib/download.html)
- OpenCV Python (optional)
- PyOpenGL (optional)

cython과 numpy는 필수로 설치해야 하기 때문에 사용하는 python 환경에 설치되어 있지 않다면 pip를 사용하여 설치한다.

```sh
python -m pip install cython numpy
```

opencv 및 opengl은 비전 처리에 필요하기 때문에 설치를 권장한다.

```sh
python -m pip install opencv-python pyopengl
```

설치된 ZED SDK 폴더(`/usr/local/zed`)에 있는 `get_python_api.py`를 실행하면 설치에 필요한 필수요소를 점검해주고 API를 설치하기 위한 Script를 띄워준다.

```sh
python -m pip install pyzed-3.1-cp37-cp37m-linux_x86_64.whl
```

pip에 설치가 되었는 지 확인한다.

```sh
pip list
```



# ZED Python API

API 설치 이후, Docs([Link](https://www.stereolabs.com/docs/getting-started/))를 통해 API 정보를 확인할 수 있다. 하지만 처음부터 API를 보면서 공부하기 어렵기 때문에, 예제 코드([Link](https://github.com/stereolabs/zed-examples))를 통해 ZED를 사용해볼 수 있다. 예제 코드를 Clone 하면 튜토리얼 및 Camera Control, Depth Sensing 등 ZED에서 사용가능한 기능들을 실행할 수 있도록 제공해준다. 예제를 보면서 ZED에 어떻게 접근하는 지 확인할 것이다. 

Document에 있는 Using the Video API([Link](https://www.stereolabs.com/docs/video/using-video/)) 항목을 참조하면서 문서를 작성한다.

## ZED Import

ZED를 사용하기 위한 python API를 Import 한다.

```python
import pyzed.sl as sl
```

## 카메라 초기 설정

Camera Object를 생성하고 `InitParameters`를 사용하여 초기화 파라미터를 지정해준다.

```python
# Create a ZED camera object
zed = sl.Camera()
 
# Set configuration parameters
init_params = sl.InitParameters()
init_params.camera_resolution = sl.RESOLUTION.HD1080 
init_params.camera_fps = 30 
```

### Initial Parameter

API에 내장되어 있는 Initial parameter의 종류는 다음과 같다.

*  Camera Configration Parameters: `camera_*`(resolution, Image flip 등)
* SDK Configration Parameters: `sdk_*` (verbosity, GPU device used 등)
* Depth Configration Parameters: `depth_*` (depth mode, minimum distance 등)
* Coordinate Frames Configration Parameters: `coordinate_*`(filename, real-time mode 등)

## 카메라 열기

`InitParameters`를 사용하여 초기 설정을 완료했다면, `zed.open(init_params)`를 사용하여 카메라를 연다.

```python
# Open the camera
err = zed.open(init_params)
if (err != sl.ERROR_CODE.SUCCESS) :
    exit(-1)
```

## 이미지 캡쳐

카메라에 수신되는 영상을 캡쳐하여 이미지화 할 수 있다. `sl.Mat()`을 사용하여 Mat 이미지를 생성할 수 있으며, 이미지 위에 OpenCV를 사용하여 인식한 물체의 Bounding Box를 넣는 작업이 가능하다.

```python
# Create Mat Object
image = sl.Mat()
# Create Runtime Parameter
runtime_parameters = sl.RuntimeParameters()

if zed.grab(runtime_parameters) == sl.ERROR_CODE.SUCCESS:
    # A new Image is available if grab() return SUCCESS
    zed.retrieve_image(image, sl.VIEW.VIEW_LEFT) # Retrieve the left image
```

* `zed.grab()`
  * 가장 최근에 카메라에서 촬영된 이미지를 가져옵니다.
  * `sl.RuntimeParameters()`([Link](https://www.stereolabs.com/docs/api/python/classpyzed_1_1sl_1_1RuntimeParameters.html)) 에서 설정된 파라미터에 따라 촬영되는 방법이 달라집니다.
  * API Docs. ([Link](https://www.stereolabs.com/docs/api/python/classpyzed_1_1sl_1_1Camera.html#a0360703f876c79cfc890cf87a69867bc))

* zed.retrieve_image(py_mat, View, Type)
  * 카메라나 SVO 파일에서 이미지를 찾습니다.
  * 해당 함수가 호출 시, GPU 메모리에 있는 이미지가 RAM으로 복사됩니다. 
  * 사용할 수 있는 View 목록([Link](https://www.stereolabs.com/docs/api/python/classpyzed_1_1sl_1_1VIEW.html))
  * API Docs. ([Link](https://www.stereolabs.com/docs/api/python/classpyzed_1_1sl_1_1Camera.html#a81c0b6777dfbdf39795b500ead89a358))

## 카메라 촬영

스테레오 랩스의 전용 파일 형식인 SVO 형식을 사용하여 타임스탬프, 센서 데이터 같은 메타데이터와 함께 비디오를 저장합니다. 

```python
# Create a ZED camera object
zed = sl.Camera()

# Enable recording with the filename specified in argument
recodingParams = RecordingParameters("myVideoFile.svo", sl.SVO_COMPRESSION_MODE.H264)

err = zed.enable_recording(recodingParams)

while !exit_app :
    if zed.grab() == SUCCESS :
        # Each new frame is added to the SVO file
        zed.record()

# Disable recording
zed.disable_recording()

```

* zed.enable_recording(RecordingParameters)
  * SVO 파일을 기록하기 위해 사용하는 함수입니다.
  * `RecordingParameters`([Link](https://www.stereolabs.com/docs/api/structsl_1_1RecordingParameters.html))을 사용해서 녹화 옵션을 지정합니다.

## 카메라 닫기

카메라 사용이 끝난 경우, `zed.close()`를 사용하여 카메라를 닫는다.

```python
# Close the camera
zed.close()
return 0
```

# Conclusion

SDK 및 API 설치와 ZED2에서 사용할 수 있는 API의 기본 기능들에 대해 훝어보았다. SDK에 내장되어 있는 다양한 기능들을 활용한다면 향후의 비전 Task를 진행할 때 유용하게 사용할 수 있을 것이라 생각한다. Nvidia Jetson 제품들이랑 연동해서 사용할 예정이고 이후 연구는 Jetson을 사용하기 위한 방법들에 대해 작성한다.







