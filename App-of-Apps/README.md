## 배포 방식 - App of Apps

App of Apps는 새로운 App이 추가가 되어도 구조가 바뀌지 안도록 하기 위함입니다.
하나의 폴더에 child Application 생성을 할 수있는 패턴이 App of Apps 패턴으로 사용을 합니다.

단, 해당 데모에선 같은 서비스를 이름만 변경을 하여 하지만 실제로 사용을 하려면 한 Service에 필요한 Application 배포를 할 때 사용을 합니다.
`예: web = apache + tomcat + mysql or A serivce = a eks, b eks, c eks`

App of Apps의 Parent Application의 namespace는 무조건 `Argo CD`를 사용을 해야 Child Application이 배포가 됩니다.

## 사용방법
1. Argo CD Application **생성**을 클릭 
2. **Edit as yaml**을 클릭
3. **d-application.yaml** 내용을 복사를 하여 붙여 넣기 후 **SAVE** 클릭
4. **Create** 클릭하여 Application을 생성
5. 생성한 Application을 선택 후 **Sync** 클릭
6. 확인