# _Argo Rollout Canary_

Argo CD에서 제공하는 Rollouts 중 Canary 배포를 사용하는 예시 코드입니다.  
해당 코드는 ALB Controller를 이용을 하여 배포를 진행을 합니다.

# 사전 필요 사항
- ALB controller 설치 필수

# 사용방법

`rollout-application-ALB.yaml`를 사용하여 console에서 Application을 생성을 합니다.

## 생성되는 서비스

- Deployment - 1개
- service - 3개 
    - root service
    - stable service
    - canary service
- Ingress - 2개
    - main ingress - 1개의 ALB에 Rule로 자동 설정  
    해당 도메인으로 `stable.seodae.tk` canary 서비스만 접속이 가능한 Ingress Rule  
    해당 도메인으로 `canary.seodae.tk` canary 서비스만 접속이 가능한 Ingress Rule  
    해당 도메인으로 `www.seodae.tk` stable+canary traffic 비율(rollout object에서 정의한 `setWeight`참고)로 서비스 정상 유무 확인 Rule  
    해당 도메인으로 `www.seodae.tk/canary` canary 서비스만 접속이 가능한 Ingress Rule  
    - canary ingress(canary 테스트용) - 따로 할 경우, Ingress service 추가로 비용 증가  
    해당 도메인으로 `canary-demo.seodae.tk` canary 서비스만 접속이 가능한 Ingress 

# 추가 업데이트 필요 내용

Rollouts에 대한 helm chart 생성 예정