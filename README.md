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

## 4. nodown - 장기할부 피해 검토를 위한 규칙 엔진

가맹점 폐업으로 남은 할부금을 부담하는 소비자의 피해를 다룬 4인 팀 프로젝트에서 팀장을 맡았습니다.

**개인 역할**
거래 탐지, 가맹점 상태 모의조회와 사례 생성 API, 기본요건 규칙 엔진을 Python과 Flask로 구현했습니다. 판정 결과에 조건 충족 여부와 제외 사유를 포함하고, 누락된 값은 추가자료 확인 상태로 처리했습니다. 요건 판정과 생성형 AI의 설명 기능을 분리했습니다.

**검증 결과**
합성 카드거래 12건에서 기본조건을 충족한 후보 7건과 그중 폐업 상태에 따른 알림 대상 4건을 확인했습니다. 정상 입력, 경계조건과 누락 입력을 단위 및 API 테스트로 점검했습니다.

[팀 프로젝트 코드](https://github.com/10502R/nodown)

## 5. AIBOMBOMBass - AI 모델 구성명세 생성과 모듈 통합

AI 모델과 데이터셋, 실행 환경의 구성정보를 연결하는 3인 팀 프로젝트에서 Model BOM 구현과 모듈 통합을 담당했습니다.

**개인 역할**
Hugging Face 모델 메타데이터를 수집하고 requirements.txt, config.json과 모델 카드의 의존성을 파싱했습니다. SPDX 3.0.1 AI Profile을 참고해 모델 구성명세를 생성하고, Python과 FastAPI로 다른 팀원이 담당한 Dataset BOM 및 Environment BOM 모듈과 연결했습니다.

**검증 결과**
외부 API 연결 실패 시 규칙 기반 분석으로 전환하는 경로를 구현했습니다. 통합 과정에서 모듈별 대체 경로를 연결하고 규칙 기반 분석 경로에서 통합 API 3종의 응답을 확인했습니다.

## 6. Windows 악성코드 분석 - 자동실행과 명령제어 통신 추적

대학 전공 개인과제에서 Windows 악성코드의 프로세스 실행 기록과 API 호출을 분석했습니다.

**분석 내용**
예약 작업을 통한 자동실행, 분석 도구 탐지, 문자열 복호화와 명령제어 서버 연결 과정을 추적했습니다. 수집하는 시스템 정보와 수신 명령별 동작을 살펴보고, 분석 근거를 프로세스명, 파일 경로와 함수 호출로 보고서에 정리했습니다.
