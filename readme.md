## NOTICE
- 현재, Mac OS로 개발하였기에 명렁어가 다를 수 있습니다.
- port 번호, library는 제 컴퓨터에 맞춰 구현되어 있습니다. 알맞게 변경해주시면 감사하겠습니다.   
- [Colab(Frido-Demo Colab 실습)](https://colab.research.google.com/drive/1m4M6L0y0G97EQjDheeIgJBpfv4ZBJAVG?usp=sharing)에서 Pre-trained 모델을 사용해보려고 했으나, OOM의 문제로 사용할 수 없었습니다. 

<hr>

### Docker Part 

- 버전 관리 및 배포를 편하게 하기 위해서, docker 구현.<br>

- Docker Build *(default port 8010)*
    - 오류나면, --recv-keys {Your Key} 기입. Dockerfile에 주석으로 달아놓았습니다. <b>시간이 조금 걸립니다.</b>

```
cd docker

docker build -t frido-practice:latest . 
or 
Check -> scripts/build :D 
```

- Docker Run
```
cd .. 

docker run --name frido-practice --gpus all -v $(pwd):/Frido-Practice -dit --ipc=host frido-practice:latest 
```

- Docker Attach
```
docker attach frido-practice
```

<hr>

### 가상환경 생성

- Create venv Environment
```
python -m venv venv
source ./venv/bin/activate
```

- ```setup.py``` 설치
```
pip install -e "."
```