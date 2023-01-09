# _Argo Rollout Canary_

Argo CD에서 제공하는 Rollouts 중 Canary with Blue/Green 배포를 사용하는 예시 코드입니다.  
해당 코드는 ALB Controller를 이용을 하여 배포를 진행을 합니다.  
Canary 배포전략에서 제공하는 `setCanaryScale`를 사용하여 Blue/Green과 같이 동일한 Pods를 준비를 하고  
`Setweight`으로 Canary의 Traffic 비율 조절을 합니다.

```
- setCanaryScale:
        replicas: 4 # spec.replicas와 동일한 비율로 기입
    - setWeight: 10
    - pause: { duration: 1m } 
    - setWeight: 30
    - pause: { duration: 1m } 
    - setWeight: 70
    - pause: {}
```

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
- Ingress - 1개
    - main ingress - 1개의 ALB에 Rule로 자동 설정    
        stable+canary traffic 비율(rollout object에서 정의한 `setWeight`참고)로 서비스 정상 유무 확인 Rule  
        canary 서비스만 접속이 가능한 Ingress Rule  

# 추가 업데이트 필요 내용

Rollouts에 대한 helm chart 생성 예정