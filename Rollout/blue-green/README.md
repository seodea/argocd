# _Argo Rollout Blue/Green_

Argo CD에서 제공하는 Rollouts 중 Blue/Green 배포를 사용하는 예시 코드입니다.  

# 사용방법

`rollout-blue-green.yaml`를 사용하여 console에서 Application을 생성을 합니다.

## 생성되는 서비스

- Deployment - 1개
- service - 2개 
    - active service
    - preview service

# 추가 업데이트 필요 내용

Rollouts에 대한 helm chart 생성 예정