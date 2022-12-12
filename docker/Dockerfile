FROM pytorch/pytorch:1.9.0-cuda10.2-cudnn7-devel
# RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys {Your Key}
RUN apt-get -y update

RUN apt-get -y install libgl1-mesa-glx && apt-get -y install libglib2.0-0

RUN python -m pip install --upgrade pip
RUN pip install --no-cache torch==1.9.0+cu111 torchvision==0.10.0+cu111 -f https://download.pytorch.org/whl/torch_stable.html

RUN apt-get install -y libsm6 libxext6 libxrender-dev
RUN pip install opencv-python

RUN apt-get update && apt-get install -y git

EXPOSE 8010

# RUN pip install -r requirements.txt

WORKDIR /Frido-Practice/