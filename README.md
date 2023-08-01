# **Future Engineer 2023 season**

* team name: be firing Future


* Teammates: Joe Lin  Michael Chen Maxwell Wong


* match name: Future Engineer


* apparatus: Nvida Jetson nano BO1

# Teammates introduce

![](https://github.com/katakusan/image/blob/master/image/IMG20230724231254.jpg)

Joe Lin From Taiwan

age:16

Hi my name is Joe I'm a coder and writer on this team, the job I'm responsible for is:

* research how to use Jetson nano 
* write the github 
* research how to use yolov5

![](https://github.com/katakusan/image/blob/master/image/1690213362682.jpg)

Michale Chen From Taiwan

age:16

Hola. My name is Michale, my job in WRO Future Engineers are these: 

* studied Jetson Nano with Joe 
* write engineer's notes mainly 
* training AI model
* Prepare for filing

![](https://github.com/katakusan/image/blob/master/image/126321.jpg)

Maxwell Wong From Taiwan

age:17

Hello my name is Maxwell, the job I'm responsible for is:

* research Ackerman steering
* car modification
* car test
* Prepare for filing



# **About jetson nano**
## why we are choose Jetson nano? 

* 1. Low power consumption and compact size: Jetson Nano consumes less than 10 watts of power and has a compact size, making it highly suitable for self-propelled vehicle

* 2. High-performance GPU: Jetson nano has powerful GPU than other apparatus, a higher GPU can be the camera run faster

* 3. freedom AI framework support: Jetson nano has more freedom in software development environment, including TensorFlow, PyTorch, Caffe, and ONNX, which allows developers to easily build and train machine learning models

* 4. More Connectivity Options: Jetson Nano comes with multiple connectivity options, including USB 3.0, HDMI, Ethernet, GPIO, and CSI camera connectors, allowing integration with peripherals and sensors.


Jetson nano version: BO1

## Basic setup 

### Write micro sd card



[**_write sd card URL_**](https://github.com/katakusan/wro2023-befiring/blob/main/Jetson%20nano/basic%20setup/write%20micro%20SD%20card.md) 



**We encountered  problem:I cannot use the SD card burner.**


**Solution: We searched for a lot of information online and finally discovered that it was a Jetpack version issue. Because we were using an older hardware version of Nano, the highest supported Jetpack version is 4.6. We used the higher version of 5.1, which caused it to not work.**

### Fan setup

First lock fan on jetson nano  ventilated rib

* Like this

![](https://github.com/katakusan/image/blob/master/image/IMG_20230723_173857.jpg)

Use this code to open fan

 ```
   sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm' 
 ```

and write this Lets when your Jetson nano open your fan will be open

```
cd /etc

sudo touch rc.local

sudo chmod u+x rc.local

sudo vim rc.local
```
open a vim file

```
#!/bin/bash

sleep 10

sudo /usr/bin/jetson_clocks

sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
```
write this into your vim file 

press ESC and write :wp and press enter

the fan is open when your Jetson nano open 

**We encountered  problem:  We can't find the fan header.**

**Solution: We initially thought that the fan was connected to the GPIO pins. However, after searching online, we discovered that the fan has its dedicated connector labeled "J15 FAN".**

## Image recognition

Open Jetson nano terminal 

```
sudo apt update
sudo apt install -y python3-pip
pip3 install --upgrade pip

```
Upgrade the system and download pip.

```
git clone https://github.com/ultralytics/yolov5
```
clone yolov5 file on your Jetson nano

download pytorch and torchvision

```
wget https://nvidia.box.com/shared/static/fjtbno0vpo676a25cgvuqc1wty0fkkg6.whl -O torch-1.10.0-cp36-cp36m-linux_aarch64.whl

pip3 install torch-1.10.0-cp36-cp36m-linux_aarch64.whl
```
wait some time and pytorch will be download

```
cd
sudo apt install -y libjpeg-dev zlib1g-dev
git clone --branch v0.9.0 https://github.com/pytorch/vision torchvision
cd torchvision
sudo python3 setup.py install
```

wait some time and Torchvision will be download

```
sudo apt upgrade
```

Upgrade 

```
sudo apt install build-essential libssl-dev zlib1g-dev libncurses5-dev libncursesw5-dev libreadline-dev libsqlite3-dev libgdbm-dev libdb5.3-dev libbz2-dev libexpat1-dev liblzma-dev libffi-dev libc6-dev
```

Install necessary packages.

```
wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tar.xz
tar -xf Python-3.8.12.tar.xz
cd Python-3.8.12
./configure --enable-optimizations
make -j4 
sudo make altinstall
``` 
Install python3.8

```
python3.8 -m pip install --upgrade pip

python3.8 -m pip install yolov5
```

Update pip and download yolov5.

```
python3.8 detect.py --weights yolov5n6.pt --nosave --source 0
```

open yolov5 detect  (_weights version can be chang ex:yolov5s yolov5m......_)

**Beware: The number after "source" represents the camera name. The default name is usually 0. If there are more than two cameras set up, you can use the following code to find the camera.**

and you can detect like this

![](https://github.com/katakusan/image/blob/master/image/image.jpg)


We have an old solution: [**_yolov5 old_**](https://github.com/katakusan/wro2023-befiring/tree/main/Jetson%20nano/yolov5%20old)


**What are the differences between the new and old solutions?**


In the old solution, we followed the common practice found online, which involved using the requirements.txt file from yolov5 to download all the necessary files. However, when trying to download Ultralytics, which was not included in the requirements.txt file, we had to set up a Python 3.8 environment specifically for this purpose, which took a lot of time.

After multiple attempts, we came up with a new approach. Instead of relying on the requirements.txt file from yolov5, we directly updated pip to the Python 3.8 version and then proceeded to download the official yolov5 package provided by Ultralytics. This method saved us a lot of time as we no longer needed to set up a separate Python 3.8 environment specifically for downloading Ultralytics. The direct download of the official package proved to be a more efficient and straightforward solution for our needs.

* yolov5 new

  * Pros: The new solution simplifies the previously cumbersome process and saves a significant amount of time.

  * Cons: Updating pip may cause conflicts with Python 3.6 if you need to use it.

* yolov5 old

  * Pros: The old solution, which involved setting up a separate environment, doesn't affect the original Python 3.6 environment and is more convenient to work with.
  
  * Cons: The process is complicated, prone to errors, and time-consuming.













































