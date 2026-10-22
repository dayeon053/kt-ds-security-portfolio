# kt ds Security 지원 포트폴리오 - 황다연

정보보호를 전공하고 개인정보보호를 복수전공하며, 구성요소 분석과 보안 검증, 개인정보 관리 API를 구현했습니다.

## 1. 클라우드 기반 SBOM 생성 및 SCA 취약점 분석 자동화

소스 의존성과 실행 서버의 분석 결과를 함께 조회하기 위해 저장소 입력부터 분석 실행까지 연결한 화이트햇스쿨 6인 팀 프로젝트입니다.

**개인 역할**
SBOM 생성 자동화와 CodeCommit 저장소 주소의 S3 전달을 주로 맡았습니다. Lambda, Systems Manager와 EC2를 연결했고, Amazon Inspector 결과 검증, Maven SBOM과 Package URL 비교는 보조 담당으로 수행했습니다.

**결과**
팀은 저장소 입력, SBOM 생성, 서버 패키지 진단과 취약점 조회까지 이어지는 자동 분석 시나리오를 시연했습니다.

[팀 관련 SBOM 생성 및 DB 연계 코드](https://github.com/WhiteHatSchool/SBOM_Gen_and_Conn_DB)

## 2. LogosFuzz - AI 하네스 생성에 빌드 정보 연결

LLM이 생성하는 C/C++ 퍼징 하네스에 API와 헤더, 컴파일 옵션을 전달하기 위해 추출 결과와 생성 계획을 연결했습니다. 4인 팀에서 대상 프로필, API 분석과 지식베이스 연결을 담당했습니다.

**개인 구현**
CMake의 compile_commands.json에서 파일별 컴파일 플래그를 추출해 Clang AST 분석에 전달했습니다. 대상 프로필로 지식베이스를 생성하고 비-Bazel 빌드 단위를 하네스 계획에 연결했습니다. 프로필에 따라 기존 자동차용 규칙과 범용 분석의 적용 조건도 구분했습니다.

**검증 사례**
WSL의 libsndfile 1.2.2에서 92개 파일의 컴파일 정보를 추출하고 최소 하네스의 200회 실행을 확인했습니다. 정답셋 생성 단계에서 헤더 경로가 누락돼 컴파일이 실패하는 문제를 수정한 뒤 92개 파일의 컴파일을 확인했습니다. 선정 API 8개는 소스 라벨과 컴파일러 심볼 정답셋으로 각각 대조했습니다.

- [범용화 개발 브랜치](https://github.com/sesezz/LogosFuzz/tree/feature/generic-embedded)
- [대상 프로필 및 추출기 PR #71](https://github.com/sesezz/LogosFuzz/pull/71)
- [KB 연결 및 평가 PR #76](https://github.com/sesezz/LogosFuzz/pull/76)
- [구현 및 평가 기록](https://github.com/sesezz/LogosFuzz/blob/feature/generic-embedded/docs/GENERIC-A-kb.md)
- [프로필 기반 KB 테스트](https://github.com/sesezz/LogosFuzz/blob/feature/generic-embedded/tests/test_kb_profile.py)

## 3. 동의ON - 개인정보 위험도와 동의 이력 관리

개인정보처리방침의 항목을 바탕으로 위험도를 계산하고 동의 상태와 변경 이력을 관리하는 4인 팀 프로젝트에서 팀장을 맡았습니다.

**개인 역할**
일정과 요구사항을 조율하고 FAIR를 참고한 위험도 계산 로직, 동의항목 API와 회귀 검증을 담당했습니다. 데이터 민감도, 외부 제공, 보유기간, 처리 목적과 AI 활용을 위험도 변수로 다뤘습니다.

**구현 및 협업**
공용 모델과 동의항목 API를 개발 브랜치에서 관리하고 회귀 테스트를 추가했습니다. 팀원이 맡은 일을 진행하기 어려운 상황에서는 정기회의 전에 따로 만나 함께 작업하고 이후에도 대면 작업 방식을 유지했습니다. 연구 원고는 정보보호학회논문지에서 수정 후 재심 판정을 받았습니다.

- [개발 브랜치](https://github.com/dayeon053/dynamic-consent-system/tree/develop)
- [공용 모델 회귀 테스트 PR #20](https://github.com/dayeon053/dynamic-consent-system/pull/20)
- [동의항목 API PR #21](https://github.com/dayeon053/dynamic-consent-system/pull/21)