# Anomaly Detection by PCA and GMM(Gaussian Mixture Modeling)

## 1.IP Address Encoding
### 1-1. ip를 모두 octat으로 분리
src_ip : a.b.c.d, dst_ip : e.f.g.h
 -> oct1 = a, oct2 = b, ..., oct8 = h
### 1-2. 중복되는 src_ip 행 제거
5,820,310 rows -> 31,032 rows

## 2. PCA: IP dimension 축소
- variance_ratio_를 계산하여 누적 variance가 75%를 넘는 차원을 선택
- 8차원 -> 5차원

## 3. GMM: IP 주소 클러스터링 & Anomaly Detection
### 3-1. BayesianGuassianMixture 클래스
불필요한 군집을 줄이고, 최적의 클러스터 수 탐색
- 3개의 클러스터 생성
### 3-2. score_samples() 메서드
클러스터 내의 데이터 포인트의 밀도 측정
threshold를 설정하여 그보다 낮은 밀도를 가진 구간의 데이터를 anomal data라고 판단
- 전체 31,032개 src_ip중 1,242개의 ip를 이상ip로 탐지
- 1,242개 중 동일 대역 ip는 930개
