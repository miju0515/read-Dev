## 유연하고 안전하게 배포 Pipeline 운영하기
- 읽은날짜 2023/10/13
- 업로드날짜 2023/10/12
- [토스](https://toss.tech/article/slash23-devops)
- 배포

---
- 토스뱅크에는 400개가 넘는 배포 pipeline이 있다
- Pipeline: 반복적인 일을 자동화하는 시스템, 서버 프로그램을 빌드하고 배포하는 pipeline이 대표적
- Compliance 요건 -> Pipeline에서 반드시 지켜야하는 요건
- Pipeline 도구: Jenkins, GitHub Actions, GoCD(<-토스뱅크에서 사용중)
- GoCD의 어려움
  1. 가시성: Pipeline이 많으면 웹 UI에서 확인이 어려움, 하나씩 설정을 보는 것도 어려움, 설정의 변화를 알기 어려움
  -> Pipeline as Code(Pipeline을 웹 UI에서 정의하지 않고 코드로 표현하여 Git에 저장하는 것)
  2. 생산성: Pipeline을 빠르고 정확하게 만들어야함, 이미 만들어진 설정을 복붙해서 새로운 Pipeline을 만들떄가 많음, 공통된 변경사항이 있을 때 모든 파일을 수정해야하는데 이때 실수하기 쉬움
  ->GoCD Template(Pipeine 동작을 추상화해서 Template으로 만들고 공유)
  3. 확장성: Pipeline 설정은 Git에서, Template 설정은 웹 UI에ㅓㅅ 해야되기 때문에 Template 수정이 불편하고, Template을 수정하면 많은 Pipeline에 한 번에 적용되기 때문에 실수를 했을 때 영향이 큼 -> Helm Template(Template Rendering 도구, 공통 부부분을 Template으로 만들고 고유한 부분을 Values로 주입하여 Rendering, Git 저장소에서 Pipeline 설정과 Template 설정을 한 곳에서 확인 가능)
  4. 복잡성: Pipeline Template은 시간이 지나며 점점 복잡해짐 -> CI(Continous Integration, 변경사항에 대하여 자동으로 검증을 진행하고 성공했을 때만 반영)
  