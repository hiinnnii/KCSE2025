![image](https://github.com/user-attachments/assets/4ccff766-1846-4d53-b22b-07f0a88824ab)2025 한국 소프트웨어공학 학술대회 | “지능형 개발 기술과 소프트웨어 공학의 미래”
논문을 작성할 주제로 Dacon에서 진행된 "이미지 색상화 및 손실 부분 복원 AI 경진대회"의 데이터 셋을 활용하여, 이미지 색상화 및 손실 부분을 복원하는 인공지능 모델 개발하기로 결정하였습니다.

팀원 | 박혜인, 이신화, 최승효, 엄다현, 지정원 (지도교수님 : 김준화 교수님)

# 주제 및 문제 정의
흑백 이미지 복원을 위한 Stable Diffusion 및 GAN 기반 하이브리드 프레임 워크 
Stable Diffusion and GAN-Based Hybrid Framework for Gray-scale Image Recovery

## 문제 정의
- 과거의 흑백 사진이나 역사적 가치가 높은 오래된 사진의 변색 및 훼손 문제 발생
- 물리적 마모, 환경적 손상 또는 인간의 훼손으로 인해 손실 이미지 발생

## 연구 목적
- 흑백 이미지 및 손상된 이미지를 복원하는 기술 개발을 목표
- 디지털 복원을 통해 문화재 및 원형 가치를 되살리고, 기존의 이미지 복원 방법에 비해 손상된 이미지를 효과적으로 복원하는 하이브리드 프레임워크를 제안하고자 함

# 연구 방법
## 데이터셋
데이콘(Dacon)에서 진행된 대회인 "이미지 색상화 및 손실 부분 복원 인공지능 경진대회"에서 제공한 데이터 셋 활용
Train set (29604장), Test set (100)장에 대해 Mask 추출 *Test set은 정답 데이터 미제공으로 인해 직접 Mask 지정
학습 셋을 8:2 비율로 나누어 실험 진행

<img width="677" alt="image" src="https://github.com/user-attachments/assets/29eaa4f9-f4bb-423f-9bb9-903db78aab88" />

## Flow Chart
![flowchart3](https://github.com/user-attachments/assets/6deea5d5-d19c-4407-9ef4-4d592882bffa)

# 연구
## Stable Diffusion 기반 이미지 복원
### 프롬프트 작성
Mask 영역 채우기를 위한 이미지 복원에 Stable Diffusion 활용, 세가지 프롬프트 작성 후 실험 진행

<img width="740" alt="image" src="https://github.com/user-attachments/assets/ea8d9463-1f63-44b7-92fe-980805991a1f" />

### 복원 결과

<img width="593" alt="image" src="https://github.com/user-attachments/assets/cd00aeac-3c28-4050-bd2e-94db003d4573" />

## 품질 평가
원본을 흑백으로 변환한 이미지와 결과물간의 MSE(Mean Squre Error)와 SSIM(Structural Similarity Index)을 각각 계산, 평균 내어 평가 진행

<img width="408" alt="image" src="https://github.com/user-attachments/assets/32e26990-efa5-4330-a2eb-7c1c2cd6085a" />

## GAN 기반 이미지 색상화
### 모델 구조

<img width="804" alt="image" src="https://github.com/user-attachments/assets/3db2d4cf-8614-473f-b0e0-9d3f0f24481d" />

### 복원 결과

<img width="699" alt="image" src="https://github.com/user-attachments/assets/dc740226-4451-4e1a-98bc-e09893d781bc" />

# 실험 결과
## 이미지 복원 성능 비교
세가지 프롬프트를 사용하여 동일한 입력 이미지에 대한 복원 결과 비교했습니다. 
MSE 기준으로는 Prompt 3이 가장 우수하였지만 SSIM을 기준으로는 프롬프트 간 성능 차이가 그다지 크지 않았습니다.

<img width="844" alt="image" src="https://github.com/user-attachments/assets/658d9a20-4ca9-4eed-8e6c-0eaf683dd017" />

불필요한 글자나 문맥적 맥락에 어긋나는 부분들이 발생하였고, 프롬프트를 자세히 작성할수록 원하는 결과를 추출해낼 수 있다는 사실을 알 수 있었습니다. 

<img width="668" alt="image" src="https://github.com/user-attachments/assets/77749889-8ba5-4bca-919c-f7c166375ce7" />


## 이미지 색상화 성능 비교
프롬프트 결과물 데이터를 사용하여 학습을 진행하였고, GAN의 최적화 함수는 Adam을 활용하였습니다. loss 계산은 Generatordp는 MSE를 활용하였고, Discriminator에는 BCE를 활용하였습니다.

### 테스트셋에 대한 색상화 결과 Dacon 산출 점수
<img width="387" alt="image" src="https://github.com/user-attachments/assets/25aa60fd-768b-498b-807d-f2507e5430c5" />

## 색상화 결과
<img width="435" alt="image" src="https://github.com/user-attachments/assets/97126f39-f3e8-48cd-959d-40c1fa2a97bd" />

## 최종 결과
<img width="587" alt="image" src="https://github.com/user-attachments/assets/aaf1c3f7-f36e-4458-935e-67610be69aa7" />

# 결론 및 향후 계획
- Stable Diffusion을 이용한 마스크 기반 복원에서 프롬프트의 구체성과 제약조건이 복원 품질에 중요한 요소임을 시사
- GAN을 활용한 색상화에서는 UNet Generator와 PatchGAN Discriminator의 조합을 통해 자연스러운 색상화를 구현, 복원과 색상화는 독립적인 과정이 아닌 상호 연관된 단계임을 확인

- Stable Diffusion과 GAN의 조합에 더해, 최신 이미지 복원 및 색상화 기술을 비교 분석하여 복원 품질을 향상시킬 수 있는 방안을 모색
- 최적의 프롬프트 설정을 위한 추가적인 연구가 필요함을 확인하여, 프롬프트 엔지니어링을 통해 복원 품질을 개선할 수 있는 방법 탐구



