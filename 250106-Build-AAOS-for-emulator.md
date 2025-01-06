# How to build AAOS Emulator Images (AAOS 14.0.0_r17)

2025/01/06 :

This page decribes how to get AAOS sources and build AAOS's emulator output images for x86 machine. 
Ubuntu 20.04 x86_84 machine will be used to do this activity.
  

### 1. preparation for ubuntu 20.04 x86 
```
sudo apt update
sudo apt install -y openjdk-11-jdk git-core gnupg flex bison build-essential zip curl zlib1g-dev gcc-multilib g++-multilib libc6-dev-i386 lib32ncurses5-dev x11proto-core-dev libx11-dev lib32z-dev ccache libgl1-mesa-dev libxml2-utils xsltproc unzip python3
```
 
### 2. make working directory 
```
mkdir -p ~/AAOS_emul/android-14.0.0_r17
cd ~/AAOS_emul/android-14.0.0_r17
```
 
### 3. fetch AAOS - 14.0.0_r17
```
repo init -u https://android.googlesource.com/platform/manifest -b android-14.0.0_r17 --depth=1
repo sync --current-branch --no-tags
```
after repo sync, we can find sources having about 113GByte size...
 
### 4. How to build
1. build  - "sdk_car_x86_64-userdebug" 
```
source build/envsetup.sh
lunch sdk_car_x86_64-userdebug
export OUT_DIR=out/sdk_car_x86_64-userdebug
make -j$(nproc)
```

2. build  - "sdk_car_md_x86_64-userdebug" - multi displays 
make clobber는 이거 하면 out도 다 지워지고 이전에 빌드한거 다 지워지는거임...
```
make clobber   
source build/envsetup.sh
lunch sdk_car_md_x86_64-userdebug
export OUT_DIR=out/sdk_car_md_x86_64-userdebug
make -j$(nproc)
```

3. build  - "sdk_car_portrait_x86_64-userdebug"  - portrait mode
```
make clobber
source build/envsetup.sh
lunch sdk_car_portrait_x86_64-userdebug
export OUT_DIR=out/sdk_car_portrait_x86_64-userdebug
make -j$(nproc)
```
이제 만들어진 out폴더의 3개의 target이 확인되면 AVD로 가져가서 emulator에서 동작시켜보자.
