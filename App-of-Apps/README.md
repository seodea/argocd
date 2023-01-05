## 배포 방식 - App of Apps

App of Apps는 새로운 App이 추가가 되어도 구조가 바뀌지 안도록 하기 위함입니다.
하나의 폴더에 child Application 생성을 할 수있는 패턴이 App of Apps 패턴으로 사용을 합니다.

단, 해당 데모에선 같은 서비스를 이름만 변경을 하여 하지만 실제로 사용을 하려면 한 Service에 필요한 Application 배포를 할 때 사용을 합니다.
`예: web = apache + tomcat + mysql or A serivce = a eks, b eks, c eks`

App of Apps의 Parent Application의 namespace는 무조건 `Argo CD`를 사용을 해야 Child Application이 배포가 됩니다.

## 폴더 구조
App of Apps의 폴더 구조는 굉장히 단순합니다.  
Applications을 관리할 Main Application인 **app-of-apps-application.yaml** 이 있으며,  
apps/ 폴더 아래에 실제로 서비스를 배포를 하는 **Applications.yaml** 파일이 있습니다.  

**app-of-apps-application.yaml** 파일은 apps/ 폴더에 application.yaml 이 추가가 되거나 변경되거나 삭제가 되면,  
감지를 하고 **Out-of-sync**가 발생이 되며, 이때 **Sync**를 하면 applications이 생성 or 삭제가 이루어 집니다.  
apps/ 폴더 안에 있는 Application들이 실제 source code를 참고를 하고 있어서 source code가 변경 시 **Out-of-sync**를 나타냅니다.

```
.
├── README.md
├── app-of-apps-application.yaml
└── apps
    ├── dev-application.yaml
    ├── prod-application.yaml
    └── test-application.yaml
```

## 사용방법
1. Argo CD Application **생성**을 클릭 
2. **Edit as yaml**을 클릭
3. **d-application.yaml** 내용을 복사를 하여 붙여 넣기 후 **SAVE** 클릭
4. **Create** 클릭하여 Application을 생성
5. 생성한 Application을 선택 후 **Sync** 클릭
6. 확인