### 안드로이드 환경 세팅 트러블

`Execution failed for task ':app:compileDebugJavaWithJavac'.`

#### 시도 1. Invalidate Caches > 실패❌
```
File -> Invalidate Caches -> "Clear File system cache and Local History" 체크 -> Invalidate and Restart
```

#### 시도 2. 환경변수 오타 수정 > 성공⭕
```
이전 개발자분이 쓰시던 PC 포맷 안하고 그대로 받아서 쓰고 있는데 , 환경변수에 오탈자가 있어 수정

setting > build Tool > gradle 그래들 정보가 안읽혔었는데 환경변수 수정 후 그래들이 잡힘.
```

#### 시도 3. upgrade android gradle plugin from version > 성공⭕
```
아무래도 gradle 경로를 잘못 로드한 것 같아 버전을 이것저것 바꿔보다가 gradle 버전 업그레이드 하면서 sync 맞춰주니 빌드 성공
```