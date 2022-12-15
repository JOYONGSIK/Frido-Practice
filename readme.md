## NOTICE
> Reference: [Frido Github Link](https://github.com/davidhalladay/Frido)

- 현재, Mac OS로 개발하였기에 명렁어가 다를 수 있습니다.
- port 번호, library는 제 컴퓨터에 맞춰 구현되어 있습니다. 알맞게 변경해주시면 감사하겠습니다.   
- [Colab(Frido-Demo Colab 실습)](https://colab.research.google.com/drive/1m4M6L0y0G97EQjDheeIgJBpfv4ZBJAVG?usp=sharing)에서 Pre-trained 모델을 사용해보려고 했으나, OOM의 문제로 사용할 수 없었습니다. 

<br>
- Readme 아래에 <b>Notice 2</b>가 있습니다. 먼저 읽어주시면 감사하겠습니다. 

<hr>

### Docker Part 
- <b>MacBook M1 으로 인해, Docker는 구현만 하고 가상환경에서 진행했습니다.</b>
```python
# MacBook M1이므로 device = torch.device('mps') 로 진행됩니다.
# pip install --pre torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/nightly/cpu 
print(f"mps 사용 가능 여부: {torch.backends.mps.is_available()}")
print(f"mps 지원 환경 여부: {torch.backends.mps.is_built()}")
```

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

- Docker Start & Attach
```
docker start frido-practice 
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


<hr>


### Datasets setup 
> 🎶 Reference : [Frido Repo README](https://github.com/davidhalladay/Frido)

#### COCO-stuff 2017 
##### Segmentation challenge split (Layout2I & SG2I), 사용 X
- We follow [LDM](https://arxiv.org/pdf/2112.10752.pdf) and [HCSS](https://arxiv.org/pdf/2105.06458.pdf) to perform layout-to-image experiment on COCO-stuff segmentation challenge split, which can be downloaded from [official COCO website](https://cocodataset.org/#download).
- Please make sure the `deprecated-challenge2017` folder is downloaded and saved in `annotations` dir.
- Please create a folder name `2017` and collect the downloaded data and annotations as follows.

   <details><summary>COCO 2017 Segmentation challenge split file structure</summary>

   ```
   >2017
   ├── annotations
   │   └── deprecated-challenge2017
   │        └── train-ids.txt
   │        └── val-ids.txt
   │   └── captions_val2017.json
   │   └── ...
   └── val2017
      └── 000000000872.jpg
      └── ... 
 
    # 기존의 coco-Dataset 저장하는법.
    mkdir 2017 
    cd coco 
    wget http://images.cocodataset.org/zips/val2017.zip 
    unzip val2017.zip  
    rm val2017.zip  
    ```
   </details>
> Data의 크기가 너무 커서, coco-minitrain을 사용할 계획입니다. -> [coco-minitrain github](https://github.com/giddyyupp/coco-minitrain)
 



 #### 참고하면 좋은 Repo or Colab.

 - [Latent Diffusion Model Colab Version](https://colab.research.google.com/drive/1EfHJc7LqOi9Ad8j1c_MzrOsCstX9UU3T?usp=sharing)
 - [fine-tuning openai diffusion model Colab Version](https://colab.research.google.com/drive/1VLkKg1OF27x5C5vCJzqH8f-Gf1jzp79p)


<hr>

 ### Notice 2 

 - 2022.12.15일 기준으로 coco dataset, Frido Model 구현을 마무리 하지 못했습니다.
 - 현재까지 진행된 것은 아래의 Colab에 가시면 확인할 수 있습니다. [LDM Training Code Colab Link](https://colab.research.google.com/drive/1ak_IMbnyQ5Y3NP6odXsSmIi8EeUwLExw?usp=sharing)
    - 개발 환경을 구축하였으나, 데이터의 용량 문제와 OOM으로 인해 시간이 지체되었습니다. <br>
    이에 <b>Diffusion Model Tranin Code</b>를 Colab으로 급하게 준비해보았습니다. 
    - 현재 MNIST Dataset으로 코드가 되어있습니다. 
    - Practice를 마무리 하지 못해 매우 아쉽습니다. <br> 만약 UNIST에 합격하게 된다면, 더욱 더 좋은 모습 보여드리도록 노력하겠습니다. 