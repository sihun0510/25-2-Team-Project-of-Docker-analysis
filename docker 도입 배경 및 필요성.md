# Docker 도입 배경 및 필요성

---

## 1) 컨테이너의 개념과 생겨난 이유

하이퍼바이저(Hypervisor)는 가상머신(Virtual Machine, VM)을 생성하고 구동하는 소프트웨어이다.  
VM이라는 개념은 하이퍼바이저가 등장한 **1960년대부터 존재**해 온 오래된 기술이다.

가상머신(VM)은 물리 하드웨어 위에 하이퍼바이저를 두고, 하드웨어 자원을 각 VM에 분리·할당하여  
각 VM이 **독립적인 OS를 포함한 완전한 시스템처럼 동작**하도록 만든다.

그러나 VM 방식은 구조적인 한계를 가지고 있었다.

- OS 전체가 포함되므로 **부팅 시간이 길다**
- 하이퍼바이저를 거쳐 자원을 사용하므로 **성능 오버헤드 발생**
- 이미지 용량이 크고 **리소스 낭비가 심함**

이러한 문제를 해결하기 위해 리눅스에서는 **프로세스 단위 격리**라는 새로운 접근이 등장했다.

컨테이너는 하이퍼바이저와 달리,
- 리눅스 커널 수준에서 **cgroups**를 통해 CPU·메모리·디스크 자원을 제어하고
- **namespace**를 이용해 프로세스별 독립된 실행 공간을 제공한다

즉, OS 전체를 가상화하지 않고 **하나의 커널을 공유하면서 프로세스만 격리**하는 방식이다.

이로 인해 컨테이너는 다음과 같은 장점을 가진다.

- 매우 빠른 실행 속도
- 가벼운 구조
- 높은 자원 효율성

이는 실제 화물 운송에서 **물건을 컨테이너에 규격화해 운반을 쉽게 만드는 개념**과 유사하다.

> **Docker**는 이러한 컨테이너 기술을 기반으로 한  
> **컨테이너 기반 오픈소스 가상화 플랫폼**이다.

---

## 2) 기업·조직이 Docker를 선택하는 주된 이유

컨테이너 플랫폼은 다양하지만, 많은 기업이 **Docker를 사실상 표준**으로 채택하고 있다.  
그 이유는 **기술적 완성도 + 생태계 + 개발 생산성 + 표준화**가 뛰어나기 때문이다.

### Docker 이전의 기업 배포 환경 문제

#### (1) 환경 불일치 문제  
- 개발자 로컬 환경과 운영 서버 환경이 다름  
- OS, 라이브러리, 패키지 버전 차이로 실행 실패 빈번  
- 흔히 말하는 *“Works on my machine”* 문제 발생

#### (2) VM 기반 운영의 비효율  
- OS 전체 포함으로 이미지 용량이 큼  
- 부팅 시간이 느리고 서버 자원 낭비 심각  
- 인프라 비용 증가

#### (3) 확장·운영 자동화의 어려움  
- 서버 증가 시 수작업 설정 필요  
- 다수 서비스 환경 통일이 어려움  
- DevOps 파이프라인 구축 복잡

#### (4) 개발 속도 저하  
- 개발자별 환경 차이로 협업 난이도 증가  
- 재현 가능한 환경 구성 어려움

---

### Docker 도입 이후의 변화

Docker는 **이미지(Image)** 개념을 통해 다음을 가능하게 했다.

- 어디서 실행해도 **100% 동일한 환경 보장**
- 환경 설정을 `Dockerfile`로 **코드화**
- 설정 누락·버전 차이로 인한 오류 급감
- 배포 안정성 향상 → **운영 비용 절감**

또한 Docker는 다음 도구들과 자연스럽게 결합된다.

- GitHub Actions
- Jenkins
- GitLab CI

이를 통해 **코드 푸시 → 자동 빌드 → 자동 테스트 → 자동 배포**로 이어지는  
CI/CD 파이프라인을 쉽게 구축할 수 있다.

#### Docker 생태계의 강점

- **Docker Hub**: 세계 최대 컨테이너 이미지 저장소
- **Docker Compose**: 멀티 컨테이너 앱 구성 간소화
- **Docker Desktop**: 로컬 개발 환경 구축 단순화
- 풍부한 문서, 튜토리얼, 에러 사례

또한 대부분의 현대 분산 시스템은 **Kubernetes 기반**으로 운영되며,  
Kubernetes는 **Docker 이미지 포맷과 완전히 호환**되도록 설계되었다.

이로 인해 Kubernetes를 사용하기 위해서라도  
Docker 이미지 생태계를 활용할 수밖에 없는 구조가 형성되었다.

명령어가 직관적이고 Dockerfile 작성이 단순하다는 점 또한  
기업 입장에서 **학습 비용을 낮추는 중요한 요소**이다.

이러한 기술적·운영적·경제적 이유가 복합적으로 작용해  
Docker는 현재 **업계 표준 컨테이너 플랫폼**으로 자리 잡았다.

---

## 3) 실제 Docker를 채용한 대표 기업과 출처

### 1. Uber

- **uBuild: Fast and Safe Building of Thousands of Container Images**  
  Uber 공식 블로그에서 대규모 Docker 이미지 빌드 사례 언급  
  https://www.uber.com/en-KR/blog/ubuild-fast-and-safe-building-of-thousands-of-container-images/

- **Introducing Makisu: Uber’s Fast, Reliable Docker Image Builder**  
  “we adopted Docker in 2015” 명시  
  https://www.uber.com/en-KR/blog/makisu/

---

### 2. Airbnb

- Airbnb Engineering Blog – Docker 태그  
  https://medium.com/airbnb-engineering/all?topic=docker

- InfoQ 기사  
  *How Airbnb Simplified the Kubernetes Workflow for 1000+ Services*  
  Docker 이미지 빌드 언급  
  https://www.infoq.com/news/2019/03/airbnb-kubernetes-workflow/

---

### 3. Netflix

- *Getting Started with Microservices Using Netflix OSS & Docker*  
  Docker 기반 마이크로서비스 아키텍처 언급  
  https://nirmata.com/2014/08/13/getting-started-with-microservices-using-netflix-oss-docker/

- *Netflix OSS, Spring Cloud, or Kubernetes? How About All of Them!*  
  Linux Containers / Docker 활용 언급  
  https://blog.christianposta.com/microservices/netflix-oss-or-kubernetes-how-about-both/
