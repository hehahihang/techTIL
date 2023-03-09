## Kubernetess
* 무중단 배포
  - 서비스 중단 없이 application을 배포하기 위해, k8s에서 rollingUpdate를 지원
  - rollingUPdate : 전체 Pod를 일시에 중단/업데이트 하는 것이 아니라, 한번에 n개씩 pod를 순차적으로 update
  - maxSurge : rolling update시 동시에 생성할 수 있는 pod의 최대 개수
    - "%" 단위로 지정하면 원하는 개수의 파드 비율이 반올림되어 지정됩니다.

### configmap
- 일반적으로 컨테이너를 사용할때 dev, prd 컨테이너는 환경이 같아야 함(환경적 차이에서 오는 에러 방지)
- configMap은 컨테이너에 필요한 환경 설정을 컨테이너와 분리해서 제공하는 방식을 사용
