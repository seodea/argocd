# ApplicationSet 사용을 위한 테스트 manifest

원하는 서비스를 원하는 Cluster에 배포하기위한 방식으로 ApplicationSet을 사용하면 조금더 편합니다.
App of apps보다 조금더 자유롭게 사용이 가능하며, 디렉토리 구조 및 manifest가 조금더 간단해 질수있습니다.

## 목표 
원하는 서비스를 원하는 Cluster에 배포하자!
- svc-echosever = A account의 dev,test,prod Cluster
- svc-guestbook = B account의 dev,test,prod Cluster

file 구조 :
```sh
Applicationset/
├── Readme.md
├── appset-cluster-dev.yaml # eks-info folder에 있는 config.json 파일을 참고하여 모든 환경의 EKS에 서비스 배포
├── appset-git-file-dev.yaml # eks-info folder에 있는 dev폴더의 config.json 파일만 참고하여 모든 환경의 EKS에 서비스 배포
├── appset-git-file-all.yaml # eks-info folder에 있는 config.json 파일을 참고하여 모든 환경의 EKS에 서비스 배포
├── appset-list-total.yaml # 용도에 따라서, dev용으로만 사용 가능
├── dev # git-file 테스트 
│   ├── a-config.json
│   └── b-config.json
└── eks-info # git-file 테스트 용 (각 계정 별로 config 파일을 작성)
    ├── dev
    │   └── a-eks-config.json
    │   └── b-eks-config.json
    ├── test
    │   └── a-eks-config.json
    │   └── b-eks-config.json
    └── prod
        └── a-eks-config.json
        └── b-eks-config.json
```
## ApplicationSet 사용 방법
ApplicationSet의 경우 Argo CD Console에서 application yaml 파일을 사용하여 배포가 불가능 합니다.
Argo CD cli를 이용해서 git or cluster or list에 대한 application yaml을 배포를 해야 합니다.
자세한 배포 방식은 아래 참고 바랍니다.

## 사전 준비
- Argo CD cli 설치
- Argo CD login 진행
    ```
    argocd login '{Argo CD URl}'  --username '{계정}' --password '{사용자 암호}' --insecure
    ```

## ApplicationSet generators - git
- git에는 files, directory 2가지 종류 제공
    - directory : App of apps와 비슷하게 해당 폴더에 있는 yaml 파일을 참고를 하여 배포 진행
    - files : config.json 파일을 참고하여 json안에 있는 내용을 가지고 원하는 서비스를 원하는 Cluster에 배포 진행

- 사용 방법
    ```sh
    argocd appset create application-git-file-dev.yaml
    ```

## ApplicationSet generators - list
- List는 application yaml 파일내에 기입을 하여 사용
    - List : key/value 형식으로 원하는 parameter를 사용 가능하여, 원하는 서비스를 원하는 Cluster에 배포 진행

- 사용 방법
    ```sh
    argocd appset create application-list-total.yaml
    ```

## ApplicationSet generators - cluster
- Argo CD secrets에 등록된 cluster의 Label을 이용하여 배포할 cluster를 정합니다.
- Label 등록 방식
    - Argo CD에서 cluster 등록 후 `kubectl label secrtes <cluster> <label>` 로 등록
    
- 사용 방법
    ```sh
    argocd appset create application-cluster-dev.yaml
    ```