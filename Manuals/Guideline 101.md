__________________________________________________________________________________

# 1. 설치 전 작업(USB->파티션 분배)

> https://velog.io/@whattsup_kim/Linux-윈도우-리눅스우분투-듀얼부팅-세팅하기

- [ ] 위 링크 리눅스 설치 전까지 단계별로 따라가기
- [ ] 우분투 USB의 경우 랩에 있는거 사용하기
- [ ] 파티션 분배 시, 실수로 불필요하게 나눴을 경우 "**볼륨 확장**"을 통해 원상복구 시키기

__________________________________________________________________________________

# 2. 설치 작업

> https://velog.io/@whattsup_kim/Linux-윈도우-리눅스우분투-듀얼부팅-세팅하기

> https://shanepark.tistory.com/230

- [ ] 위 두 링크 모두 확인하며 단계별로 따라가기

_______________________________

# 3. 한글키보드 설정

> https://shanepark.tistory.com/231

- [ ] 우측 **Alt**키 바인딩할 때(altwin 수정할 때), "**symbols[Group1] = [Hangul] };**"를 **Ctrl+C** 한 다음, vi 편집기(터미널) 상에서 기존의 항목을 **Del**키로 삭제한 뒤, **Ctrl+Shift+V** 로 붙여넣기.
- [ ] altwin 수정 완료 이후, **:wq!** 입력 뒤 **enter** 눌러서 저장하기.(편집기 명령 관련하여 아래 표 참고)

![image](https://github.com/suninbaek/test/assets/144373604/5766cbeb-7bf8-4f26-9e11-e616a541a385)

____________________

# 4. Anaconda 설치

> https://otugi.tistory.com/380

- [ ] 위 링크 따라하기
- [ ] **(참고)** 23.11.14 기준 다운 명령어: `wget https://repo.anaconda.com/archive/Anaconda3-2023.09-0-Linux-x86_64.sh`
- [ ] **(참고)** 23.11.14 기준 설치 명령어: `sh Anaconda3-2023.09-0-Linux-x86_64.sh`
- [ ] 혹시 설치 과정에서 문제 생기면 아래 코드 순서대로 입력하여 삭제하고 다시 설치하기

`conda install anaconda-clean`   # install the package anaconda clean
`anaconda-clean --yes`          # clean all anaconda related files and directories 
`rm -rf ~/anaconda3`             # removes the entire anaconda directory
`rm -rf ~/.anaconda_backup`       # anaconda clean creates a back_up of files/dirs, remove it 
                                # (conda list; cmd shouldn't respond after the clean up)

___________________________

# 5. 가상환경 만들기

> https://chancoding.tistory.com/85

- [ ] base 말고 만든 가상환경에다가 라이브러리 설치 등 진행하기

**[명령어 정리]**

`conda create -n 가상환경이름 python=3.11` # "가상환경이름"을 명명할 이름으로 대체하기

`conda env list` # 가상환경 목록

`conda activate/deactivate 가상환경이름` # "가상환경이름" 활성화 및 비활성화

`conda env remove -n 가상환경이름` # '가상환경이름' 삭제

______________________________________

# 6. Conda 확인 및 업데이트

- [ ] `conda --version` # Conda 버전 확인
(23.11.14 기준 위 절차대로면 **conda 23.7.4** )
- [ ] `conda update -n base -c defaults conda` # Conda 최신 버전으로 업데이트
- [ ] 23.11.14 기준 업데이트 후 버전 : **conda 23.10.0**

______________________________________________  

# 7. 가상환경 (base) 자동 활성화 해제

`conda activate base` # **(base)~ :** 형태로 터미널에 표시되도록 함(base 가상환경으로 설정하는 명령어; 보통 이미 켜져있을듯)

`conda config --set auto_activate_base false` # 자동으로 **(base)**가 붙는 설정 해제(반대로 활성화하고 싶을 경우 true로)

- [ ] 이후, Conda 환경에서 작업하고자 할 때에는 위의 **5. 가상환경 만들기** 에 적혀있는 명령어를 참고하여 활성화하여 작업하기

__________________

# 8. ROS 설치

> https://velog.io/@deep-of-machine/ROS-ROS1-%EC%84%A4%EC%B9%98-Ubuntu20.04-ROS-Noetic

> https://wiki.ros.org/noetic/Installation/Ubuntu

- [ ] 위 두 링크는 동일(한글 설명, 공식 안내문)
- [ ] 아래의 단계를 제외하고 단계별로 따라하기

![image](https://github.com/suninbaek/test/assets/144373604/4a5af05a-2e2b-4086-80e0-bce254b8a38d)

_________________

## 8-1. **(필요한지 모르겠지만 일단 두고 추후 검토)** Python3 관련 패키지 설치

`sudo apt install python3-pip python3-all-dev python3-rospkg`

__________________

## 8-2. **(필요할거 같은데 추후 확실히 검토)** ROS 패키지 catkin_tools 설치

`sudo -H pip3 install catkin_tools`


________________

# 9-1. NVIDIA 드라이버 설치

(아래 순서대로 한 줄 한 줄 씩 진행. 혹시 진행 중 얘기치 못한 상황이 발생한 경우 아래 **IF**에 해당 내용이 있는지 확인)

**1. 기존에 설치된 드라이버 삭제**
> `sudo apt-get purge nvidia*`
>
> `sudo apt-get autoremove`
>
> `sudo apt-get autoclean`
>
> `sudo rm -rf /usr/local/cuda*`

**2. Key 추가**
> `sudo wget -O /etc/apt/preferences.d/cuda-repository-pin-600 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin`
>
> `sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub`
>
> `sudo add-apt-repository "deb http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/ /"`

**3. 설치할 드라이버 확인**

> `ubuntu-drivers devices`
>
> 아래와 같은 결과값 중 "**driver    :** "에 있는 디바이스가 설치 가능한 대상임.
![image](https://github.com/suninbaek/test/assets/144373604/674937e9-5cb6-4a13-a2da-f8170fb1666b)

**4. 설치할 드라이버 선택**
> 아래 링크의 Compatibility Support Matrix를 고려하여 설치할 드라이버 선택(실패 시 다시 하면 됨)
> https://docs.nvidia.com/deploy/cuda-compatibility/index.html#binary-compatibility__table-toolkit-driver
![image](https://github.com/suninbaek/test/assets/144373604/ce123088-e3d9-4548-9eac-17f448974155)

**5. 드라이버 설치**
> 아래 코드에 '520'으로 적힌 부분을 알맞게 수정하여 진행
>
> `sudo apt-get install nvidia-driver-520`
>
> `sudo apt-get install dkms nvidia-modprobe`
>
> `sudo apt-get update`
>
> `sudo apt-get upgrade`

**6. 재시작**
> `sudo reboot`

**7. 설치 확인**
> `nvidia-smi`
>
> 아래 같은 화면 뜨면 제대로 설치된 것. 해당 화면에 출력되는 **CUDA Version**은 신경쓰지말자. 어차피 따로 설치해야한다.
![image](https://github.com/suninbaek/test/assets/144373604/0dfa45d8-bb7a-4194-904e-3456dbc8af39)

________

# 9-2. CUDA 설치

(아래 순서대로 한 줄 한 줄 씩 진행. 혹시 진행 중 얘기치 못한 상황이 발생한 경우 아래 **IF**에 해당 내용이 있는지 확인)

**1. NVidia 개발자 사이트 방뭉 및 최신버전(혹은 필요한 버전) CUDA Toolkit 찾기**
> https://developer.nvidia.com/cuda-toolkit-archive
![image](https://github.com/suninbaek/test/assets/144373604/c55eed6b-308a-46b6-b3bc-7259f16625a3)
![image](https://github.com/suninbaek/test/assets/144373604/e9513a0b-3f32-41ab-86d1-e867c8fa69f7)

**2. 알맞은 버전(Linux -> x86_64 -> Ubuntu -> 20.04 -> runfile(local)) 선택**
> 만약 추후 ROS2 등을 사용하는 경우에 따라 Ubuntu 버전이 바뀌는 등의 변동이 있을 수 있음
![image](https://github.com/suninbaek/test/assets/144373604/b398b40c-117d-47e5-854e-2fb93530f567)

**3. 위 버전 선택에 따라 아래에 적힌 Base Installer 명령어를 통한 실행**
> **(참고)** 231115, ver12.3.0 기준 명령어
>
> `wget https://developer.download.nvidia.com/compute/cuda/12.3.0/local_installers/cuda_12.3.0_545.23.06_linux.run`
> 
> `sudo sh cuda_12.3.0_545.23.06_linux.run`

**4. CUDA Installer 실행 시, 아래와 같이 설정 후 설치**
> ![image](https://github.com/suninbaek/test/assets/144373604/ece7d27c-c48a-4f55-9fce-708d2997ad69)
>
> `↓` ==> `Continue` ==> `Enter`
>

> ![image](https://github.com/suninbaek/test/assets/144373604/faaccde4-57c5-4ff6-a3ad-572eb5e62be3)
>
> 'accept' ==> 'Enter'
>

> ![image](https://github.com/suninbaek/test/assets/144373604/7d3a5491-e992-46d2-b84f-8f43932759c3)
>
> `Space` ==> `↓ (Install까지)` ==> `Install` ==> `Enter`
>

> ![IMG_0655](https://github.com/suninbaek/test/assets/144373604/6478c783-b513-44af-a298-90b028b27e33)
> 
> `CUDA 설치 완료`
>

**5. PATH 설정**
> 아래 코드를 버전에 맞춰서 수정하여 활용 
>
> `sudo sh -c "echo 'export PATH=$PATH:/usr/local/cuda-12.3/bin'>> /etc/profile"`
>
> `sudo sh -c "echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-11.7/lib64'>> /etc/profile"`
>
> `sudo sh -c "echo 'export CUDADIR=/usr/local/cuda-11.7'>> /etc/profile"`
>
> `source /etc/profile`

**6. CUDA 설치 확인**
> `nvcc --version`
>
> 설치한 버전이 설치되어 있는지 확인. 만약 10.1로 버전이 뜨거나 nvcc를 찾을 수 없다고 나오면 PATH 지정에 문제 있을 가능성 농후. 아래에 적힌 "**IF CUDA PATH 지정 오류**" 확인 요함.





______________

## **IF** 아래와 같은 에러 (1)

> Err:1 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64  InRelease            
>   The following signatures couldn't be verified because the public key is not available: NO_PUBKEY A4B469963BF863CC
> 
> W: GPG error: https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 InRelease:
>   The following signatures couldn't be verified because the public key is not available: NO_PUBKEY A4B469963BF863CC 
> E: The repository 'https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 InRelease' is not signed. 
> N: Updating from such a repository can't be done securely, and is therefore disabled by default. 
> N: See apt-secure(8) manpage for repository creation and user configuration details.

다음 두 명령을 순서대로 입력

>  `sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/3bf863cc.pub`

> `sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/7fa2af80.pub`

## **IF** Sub-process /usr/bin/dpkg 에러 (1)

> https://forums.developer.nvidia.com/t/ubuntu-and-nvidia-provided-packages-conflict-breaking-installation/259150


## **IF** Sub-process /usr/bin/dpkg 에러 (2)

> https://jellybeanz.medium.com/tip-sub-process-usr-bin-dpkg-%EC%97%90%EB%9F%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-f2aaf33ca18c

## **IF** 망했다(검은화면 등등)

> https://hobbydev.tistory.com/54
> https://sdpcs.tistory.com/17


## **IF** CUDA PATH 지정 오류

> https://romillion.tistory.com/95



____________________________

설치과정에 문제 생길 경우 아래 링크들 참고

> 1. https://teddylee777.github.io/linux/ubuntu2004-cuda-update/#nvcc-%EB%B2%84%EC%A0%84-%ED%99%95%EC%9D%B8
> 2. https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=20.04&target_type=runfile_local
> 3. https://vividian.net/2022/11/1111
> 4. https://cow-kite24.tistory.com/331
___________

# 10. Pytorch 설치

> https://pytorch.org/get-started/locally/

- [ ] Deep Learning 라이브러리
- [ ] **(참고)** 231115 기준 명령어: `conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia`

![image](https://github.com/suninbaek/test/assets/144373604/78198825-5260-497c-a64f-d1c4bdb11086)



___________

# 11. OpenCV 설치

> https://anaconda.org/conda-forge/opencv

- [ ] CV를 위한 오픈소스 라이브러리
- [ ] (base)로 설치하지 않는 것 추천
- [ ] 작업할 **Conda 가상환경에서 설치** 진행

`conda install -c conda-forge opencv`

___________

# 12. Ultralytics 설치

> https://anaconda.org/conda-forge/ultralytics

- [ ] YOLOv8을 포함한 라이브러리
- [ ] 작업할 **Conda 가상환경에서 설치** 진행

`conda install -c conda-forge ultralytics`

___________

# 13. librealsense 설치

> https://github.com/IntelRealSense/librealsense/blob/master/doc/distribution_linux.md#installing-the-packages

- [ ] Realsense 라이브러리
- [ ] 작업할 **Conda 가상환경에서 설치** 진행


___________

# 14. Catkin Workspace 만들기

### Things to know before preceding.

- **Catkin Overview** : https://wiki.ros.org/catkin/conceptual_overview
- **Catkin, workspace, 그리고 package** : https://needs-searcher.tistory.com/49
- **`catkin_make` 와 `catkin build`의 차이** : https://robotics.stackexchange.com/questions/16604/ros-catkin-make-vs-catkin-build



### Catkin Workspace 설치(A: catkin_make / B: catkin build; 가급적 둘 중 한가지로만 진행)

**1. Directory 만들기**

> `mkdir -p ~/catkin_ws/src` : 프로젝트를 저장할 **catkin_ws**를 만들고 그 안에 **src**파일을 만든다.

**2. src에 CMakeLists.txt 생성**

> `cd ~/catkin_ws/src` : **src**파일로 이동
> 
> **A.** `catkin_init_workspace` : **CMakeLists.txt** 생성
> **B.** `catkin init` 
> 

**3. catkin_ws 디렉토리에서 build** 

> `cd ..` : 작업공간을 **~/catkin_ws/src**의 상위 디렉토리(**~/catkin**) 로 옮김
> 
> **A.** `catkin_make` : **CMakeLists.txt**를 활용하여 **build**
> **B.**  `sudo apt-get install python3-catkin-tools` ==> `catkin build`
> 
> `source devel/setup.bash` : **build** 과정으로 생성된 **devel**파일 안의 **setup.bash**를 실행하여 그 작업공간이 **ros**환경의 최상위에 **overlay**되도록 **shell**에 등록



**참고할만한 링크**
> https://needs-searcher.tistory.com/49
> https://hoonney.tistory.com/20
> https://wiki.ros.org/ko/catkin/Tutorials/create_a_workspace
> https://answers.ros.org/question/207433/catkin-build-gives-command-not-found/

## **IF** 오류 중 빌드가 이미 되어있다고 할 때

1. `rm -rf devel/`
2. `rm -rf build` 
3. `catkin build` or `catkin_make`


____________________


# 15. Catkin Package 만들기(일단은 SKIP)

https://wiki.ros.org/ko/catkin/Tutorials/using_a_workspace
https://hoonney.tistory.com/21
https://adioshun.gitbooks.io/ros_autoware/content/Fundamentals/catkin-make.html
___________

# 16. IntelRealsend SDK 2.0 설치

> https://dev.intelrealsense.com/docs/compiling-librealsense-for-linux-ubuntu-guide
> https://m.blog.naver.com/heennavi1004/222010773955

- [ ] 위 두 링크 참고하여 설치하기
- [ ] 디렉토리 확인 잘 해가며 진행하기(librealsense 디렉토리로 이동)
- [ ] 아래 사진과 같이 진행하여 Kernel 확인하기
![image](https://github.com/suninbaek/test/assets/144373604/fb20e04d-910b-4e82-ae15-c39510adecb1)

아래 링크는 참고용

> https://www.intelrealsense.com/sdk-2/

___________

# 17. IntelRealSense-ros wrapper 설치

> https://github.com/IntelRealSense/realsense-ros/tree/ros1-legacy

- [ ] 위 링크 단계별로 따라하기
- [ ] 중간에 `sudo apt-get install ros-$ROS_DISTRO-realsense2-description` 필히 하기
- [ ] 별도로 `sudo apt-get install ros-noetic-ddynamic-reconfigure` 안되어 있으면 하기

**[카메라 Launch command]**

- roslaunch realsense2_camera rs_camera.launch filters:=pointcloud
- roslaunch realsense2_camera rs_rgbd.launch
- roslaunch realsense2_camera rs_camera.launch
- roslaunch realsense2_camera rs_camera.launch align_depth:=true

___________

# **[ETC]**

- https://blog.naver.com/PostView.naver?blogId=jghsa6665&logNo=222503440223
- C++ CMakeLists 세팅법: `https://youtu.be/ujuEA_8jx70?si=DcH1TPvKwgB6vjfH`
- Code 안열릴때: `code --disable-gpu`
- GPU 실시간 모니터링: `watch -n 0.5 nvidia-smi`

___________
















