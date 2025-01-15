<div align="center">
<h1> 🏅우리에프아이에스 아카데미 개인 기술세미나 우수상🏅</h1>
</div>


![image](https://github.com/user-attachments/assets/b47ed1c0-162a-4a26-a17f-52b0850288d3)
## 🎯 프로젝트 개요
GitOps를 활용하여 Kubernetes 환경에서 보안이 강화된 배포 자동화 파이프라인을 구축하는 프로젝트입니다. Git을 단일 진실 공급원(Single Source of Truth)으로 활용하여 인프라의 상태를 선언적으로 관리하고, 보안 취약점을 자동으로 검사하고 모니터링하는 시스템을 구현합니다.
<br>

## 🌟 구현 내용
- ArgoCD를 활용한 GitOps 워크플로우 구현
  - Pull 기반 배포 방식 적용
  - ArgoCD App of Apps 패턴 구현
  - Git 저장소 기반 상태 관리

- Starboard를 이용한 도커 이미지, 쿠버네티스 취약점 스캔 자동화
  - Starboard 취약점 스캐닝
  - CIS 벤치마크 검증
  - RBAC 기반 접근 제어
  - 컨테이너 이미지 보안 검사

- 프로메테우스/그라파나 기반 보안 메트릭 시각화
  - 프로메테우스 스택 배포
  - 보안 취약점 시각화
## 💡 주제 선정 이유 및 개념 설명
### 💭 왜 GitOps인가?
![image](https://github.com/user-attachments/assets/e17b1f50-b6d0-449f-b2a0-9b7ad11bd02b)
B2C 서비스가 보편화되면서 사용자의 니즈와 시장 변화에 신속하게 대응해야 하는 요구사항이 늘어났습니다. 이러한 변화 속에서 전통적인 개발-운영 분리 모델로는 빠른 시장 대응이 어려워졌고, 이는 DevOps라는 새로운 개발 문화를 탄생시켰습니다.

DevOps는 개발(Development)과 운영(Operations)을 유기적으로 결합하여
- 개발자는 비즈니스 로직과 새로운 기능 개발에 집중
- 운영팀은 안정적인 서비스 제공과 인프라 관리에 집중
- 두 팀이 협업하여 지속적인 통합과 배포를 수행

이를 통해 시장의 요구사항을 신속 대응할 수 있게 되었습니다.
### 🎉 GitOps의 등장
![image](https://github.com/user-attachments/assets/1240312a-4b8f-4812-9fad-9e6a5149d4e4)
클라우드 환경이 보편화되면서 컨테이너와 쿠버네티스를 통한  선언형 모델 인프라 관리가 일반화되었습니다. 이로 인해 다음과 같은 새로운 과제들이 등장했습니다.

- 수많은 마이크로서비스의 배포 상태 관리
- 여러 환경(개발/스테이징/운영)의 일관성 유지
- 인프라 변경 사항에 대한 감사(audit) 추적
- 장애 상황에서의 빠른 복구


![image](https://github.com/user-attachments/assets/b8df0c5f-e59a-4e1d-8ada-b1a0e72a8801)
이러한 과제들을 해결하기 위해 GitOps가 등장했습니다. GitOps는 Git을 "진실의 단일 원천(Single Source of Truth)"으로 사용하여

- 인프라의 상태를 코드로 정의(IaC)
- 선언적으로 시스템의 상태를 관리
- 자동화된 배포와 동기화를 수행
- 변경 사항의 버전 관리와 추적을 보장

이를 통해 현대적인 클라우드 환경에서 더욱 안정적이고 확장 가능한 운영이 가능해졌습니다.

## 🔄 GitOps 기반 배포 파이프라인 구축
### push vs pull 방식
![image](https://github.com/user-attachments/assets/b151c3d5-31b7-49dd-ae83-c147f53b33eb)
push 방식은 기존의 CI/CD 파이프라인에서 일반적으로 사용되는 방식으로, 파이프라인이 애플리케이션을 직접 배포 환경에 밀어넣는 방식입니다. 하지만 이 방식은 CI/CD 파이프라인이 쿠버네티스 클러스터에 직접 접근해야해서 클러스터에 접근하기 위한 인증 정보를 파이프라인에서 관리해야 합니다.

때문에 클러스터 자격증명이 외부에 노출될 위험이 있고 배포 프로세스가 외부에서 클러스터로 진행되기에 보안상 좋지 못합니다.



![image](https://github.com/user-attachments/assets/e5fd5df0-d9d3-4522-a718-67c3c7bb137e) pull방식은 GitOps의 핵심 패턴으로, 클러스터 내부의 operator가 Git 저장소의 변경사항을 감지하여 자동으로 동기화하는 방식입니다. 이는 배포에 필요한 인증정보를 클러스터 내부에서 관리하기에 push 방식보다 안전합니다. 

git에 원하는 상태를 선언하면 자동으로 클러스터에 동기화 되고, 버전관리가 가능하여 버전 추적 및 롤백에도 용이하다는 장점이 있습니다.



### ArgoCD를 선택한 이유

GitOps를 구현하는 ArgoCD, FluxCD, Jenkins X 비교 검토한 결과 ArgoCD를 선택했습니다.



#### 다른 도구들과의 비교

| 기능 | ArgoCD | Flux CD | Jenkins X |
|------|---------|----------|------------|
| UI 대시보드 | ✅ 강력한 UI | ⚠️ 제한적 | ✅ 제공 |
| 배포 전략 | ✅ 다양함 | ⚠️ 기본적 | ✅ 다양함 |
| 학습 곡선 | ✅ 완만함 | ⚠️ 가파름 | ❌ 매우 가파름 |
| 커뮤니티 | ✅ 매우 활성 | ✅ 활성 | ⚠️ 보통 |
| 보안 기능 | ✅ 강력함 | ✅ 강력함 | ⚠️ 보통 |

#### App of Apps 패턴 적용
![image](https://github.com/user-attachments/assets/d65f240c-d30f-4390-9112-3f976d13b542)
App of App 패턴은 하나의 레포지토리에서 모든 애플리케이션을 관리할 수 있으며 애플리케이션의 배포 상태를 한 눈에 파악 가능하다는 장점이 있습니다. 

![image](https://github.com/user-attachments/assets/da301e04-14b5-47a9-ba88-9ff0aeecfcde)

이를 통해 ArgoCD를 활용하여 Pull 기반의 GitOps 배포 파이프라인을 구현했습니다.


## 🔒 Kubernetes 보안 취약점 자동 스캔 구현
### CIS 벤치마크 검증
![image](https://github.com/user-attachments/assets/1b086ed9-f4fb-473b-bf09-6679c45ed65d)
CIS(Center for Internet Security) Kubernetes Benchmark는 쿠버네티스 환경의 보안 강화를 위한 국제 표준 가이드라인이며, 쿠버네티스 클러스터의 보안 설정에 대한 베스트 프랙티스를 제공합니다.

#### 주요 검증 항목
1. **Control Plane 구성 검증**
   - API 서버 보안 설정
   - Controller Manager 설정
   - etcd 구성
   - Scheduler 설정

2. **Worker Node 구성 검증**
   - kubelet 설정
   - 네트워크 정책
   - 권한 및 인증 설정

3. **정책 및 감사**
   - RBAC 설정
   - 서비스 계정 관리
   - Pod Security 정책

### Starboard 취약점 스캐닝
![image](https://github.com/user-attachments/assets/2f08d92f-208a-4e5f-86a9-ddf6633d74da)
StartBoard 프로젝트는 kube-bench를 지원하여 클러스터의 보안 취약점을 스캔 후 레포트를 발행합니다. 
![image](https://github.com/user-attachments/assets/af47a7e9-148c-4271-80a4-34b5b772810a)
![image](https://github.com/user-attachments/assets/63bc1455-5a69-4927-a553-d380c6f29b74)
더불어 Trivy도 함께 포함되어 있어 클러스터에서 사용되는 이미지까지 취약점을 스캔할 수 있고, 클러스터 및 이미지 보안정책에 크리티컬한 취약점이 발견될 시 배포를 중단시킬 수 있습니다. 

### 🛡️ 보안 모범 사례
#### 최소 권한 원칙 적용
![image](https://github.com/user-attachments/assets/7e6c193f-a654-4571-8304-afb4394d4aa0)
개발자에게 최소한의 git 저장소 접근 권한을 부여합니다. RBAC 권한으로는 Pod, Service, Deployment, ConfigMap, pod/logs, pod/exec 등의 리소스 조회와 트러블 슈팅을 위한 권한만 제공하도록 합니다.
#### 브랜치 보호 정책
![image](https://github.com/user-attachments/assets/2883b31e-adf6-4d15-9938-02ecf61b8e7c)
개발자에게는 feature 브랜치 생성 및 Pull Request 생성 권한을 부여하되, 주요 브랜치(main, staging)에 대한 직접적인 push는 제한합니다. 코드 리뷰와 승인 절차를 통해서만 변경사항이 반영될 수 있도록 설정합니다.


#### Sealed-Secret 사용
![image](https://github.com/user-attachments/assets/99d3f69d-3319-45b9-887b-60a77e083dbd)

Secret 파일을 안전하게 GitOps 환경에서 관리하기 위해서  Sealed-Secret으로 암호화를 해야 합니다.
#### 접근 권한 암호화
![image](https://github.com/user-attachments/assets/99f17ae6-8d3f-4db6-bfa9-555c7fb45d55)
Git 저장소와 쿠버네티스 클러스터 접근에 필요한 민감한 자격증명은 반드시 안전한 방식으로 관리되어야 합니다. 


### 📊 보안 모니터링 시스템 구축
#### 프로메테우스 스택 배포
![image](https://github.com/user-attachments/assets/dae48b5f-14eb-47bb-8bff-063f557fa8fd)

프로메테우스 스택을 배포하여 StarBoard에서 생성되는 벤치마크 보고서를 프로메테우스 매트릭으로 전송합니다.

#### 보안 취약점 시각화
![image](https://github.com/user-attachments/assets/e7a092ef-133b-42ae-992c-a812dd8ce9cc)
배포된 모든 Application의 취약점 레포트를 한눈에 확인 가능합니다.

## ❄️ 결론
쿠버네티스 환경에서는 배포 자동화와 보안의 균형이 중요합니다. 해당 프로젝트에서는 GitOps의 핵심 가치인 선언적 인프라 관리와 자동화를 실현하면서도, 보안을 최우선으로 고려한 배포 파이프라인을 구축했습니다.

Git을 신뢰할 수 있는 단일 원천으로 활용하여 인프라의 상태를 투명하게 관리하고, 모든 변경 사항을 추적할 수 있게 했습니다. ArgoCD의 Pull 기반 배포 방식을 통해 보안을 강화하고, Starboard를 활용한 자동화된 보안 취약점 스캐닝으로 보안 모니터링을 구현했습니다.

향후에는 보안 도구 통합을 확대하고, 취약점 대응을 더욱 자동화하며 모니터링 체계를 고도화할 계획입니다.