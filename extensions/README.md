# Extension controller 

# Extension controller install

- Argo CD 처음 설치 시  
아래 방식을 이용할 경우, Argo CD 신규 설치 및 Extension controller도 같이 설치가 됩니다.
    ```
    kustomize build . | kubectl apply -f - -n argocd
    ```

- Argo CD 설치가 되어있고, Extension controller 추가 시
아래 방식을 이용할 경우, 설치 되어 있는 Argo CD에 Extension controller를 설치 합니다.
    ```
    cd ./manifests
    for i in $(ls) ; kubectl apply -f $i
    ```

# rollout-extension install

```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj-labs/rollout-extension/v0.2.1/manifests/install.yaml
```