# Contributing to SafeView

SafeView는 카메라 접근 제어와 AI 기반 모자이크 기술을 결합한 오픈소스 프로젝트입니다.
이 문서는 SafeView에 기여하기 위한 절차, 규칙, 커밋 컨벤션, 코드 가이드라인을 정의합니다.

## 1. 기여 방식 개요

SafeView는 다음과 같은 형태의 기여를 환영합니다.

| 구분 | 예시 |
|------|------|
| 기능 추가 (Feature) | 새로운 권한 레벨, 모자이크 필터링 옵션, AI 추론 기능 추가 |
| 버그 수정 (Bug Fix) | 권한 검증 오류, 토큰 만료 처리 문제, UI 비정상 표시 |
| 문서 개선 (Docs) | README, API 문서, 개발 가이드 수정 |
| 테스트 코드 (Test) | JUnit, Pytest, Jest 테스트 케이스 보완 |
| 보안 강화 (Security) | 인증, 암호화, 로그 접근 제한 개선 |
| 성능 개선 (Optimization) | AI 추론 속도 개선, 비동기 처리 리팩터링 |
| 인프라 (Infra) | Dockerfile, CI/CD, AWS 배포 파이프라인 개선 |

## 2. 브랜치 전략

SafeView는 GitHub Flow를 기본으로 합니다.

```
main → 프로덕션 배포용 안정 브랜치
develop → 통합 개발 브랜치
feature/* → 새로운 기능 개발
fix/* → 버그 수정
chore/* → 설정, 빌드, 환경 등 관리 작업
docs/* → 문서 관련 수정
```

브랜치 생성 예시:

```
git checkout -b feature/access-policy
```

## 3. 커밋 컨벤션 (Conventional Commits)

커밋 메시지는 다음 형식을 따릅니다.

```
<type>(<scope>): <subject>
```

### Type 목록

| Type | 설명 |
|------|------|
| feat | 새로운 기능 추가 |
| fix | 버그 수정 |
| docs | 문서 수정 |
| style | 코드 스타일 변경 (로직 변경 없음) |
| refactor | 코드 리팩터링 |
| test | 테스트 코드 추가/수정 |
| chore | 설정, 빌드, 의존성 변경 |
| perf | 성능 개선 |

### Scope 예시

backend, frontend, ai, camera, auth, api, db

### Subject 작성 규칙

간결하게 요약 (50자 이내)

끝에 마침표 금지

명령형으로 작성

예시:
```
feat(auth): add JWT refresh token reissue logic
fix(camera): correct access level policy evaluation
docs(api): update camera metadata API usage example
```

## 4. PR(Pull Request) 규칙

PR은 항상 dev 브랜치를 기준으로 생성합니다.

제목은 명확히 작성합니다.
예시:
```
[FEAT] Add mosaic scheduler for Camera-AI
[FIX] Resolve null pointer in AccessController
```

PR 설명에는 다음 내용을 포함합니다.

변경 요약

관련 이슈 번호 (Closes #12)

테스트 여부

Reviewer 최소 1인 지정 필수

## 5. 코드 가이드라인

### 5.1 Backend (Spring Boot)

Java 21 이상

Controller → Service → Repository 계층 구조 유지

DTO, Entity, Domain 객체 명확히 구분

Validation, ExceptionHandler, JWT Filter 일관성 유지

API 응답은 ResponseEntity<ApiResponse<T>> 형태 권장

### 5.2 Camera-AI / AI-Server (Python)

Python 3.10 이상

모델 및 inference 모듈은 /modules 디렉토리에 위치

PEP8 스타일 가이드 준수

함수명은 snake_case, 클래스명은 PascalCase

예외처리는 명시적 예외 클래스 사용 (raise ValueError("..."))

### 5.3 Frontend (React / TypeScript)

파일명 PascalCase, 컴포넌트 단위 분리

API 호출은 /services 모듈에서만 수행

상태관리는 Zustand 또는 Redux Toolkit 기반

UI 컴포넌트는 /components/ui 디렉토리로 통합

## 6. 코드 리뷰 규칙

PR 생성 후 최소 1명 이상의 Reviewer 승인 필요

Reviewer는 다음 항목을 검토해야 합니다:

로직 및 보안상의 문제

코드 중복 여부

테스트 누락 여부

커밋 메시지 컨벤션 준수 여부

## 7. 보안 및 윤리적 고려

SafeView는 프라이버시 보호를 핵심 가치로 합니다.
기여 시 다음 원칙을 반드시 준수해야 합니다.

개인 식별이 가능한 데이터를 저장하거나 출력하지 않는다.

AI 모델 학습에 사용되는 데이터셋은 비식별화된 자료만 허용한다.

사용자 로그 접근 시 반드시 인증/권한 검증 단계를 거친다.

감시 목적의 비윤리적 기능 추가는 금지한다.

## 8. 기여 절차 요약

Repository를 Fork한다.

브랜치를 생성한다. (feature/...)

커밋 컨벤션에 맞게 커밋한다.

테스트 코드와 같은 방식을 통해 충분한 테스트로 검증한다.

Pull Request를 생성한다.

Reviewer의 피드백을 반영하고 Merge한다.

## 9. 문의 및 지원

이슈 제안: https://github.com/SafeView/issues

보안 관련 제보: hanjun5559@naver.com

## 부록: 커밋 예시 모음

| 유형 | 예시 |
|------|------|
| 기능 추가 | feat(camera): implement face detection filtering pipeline |
| 버그 수정 | fix(api): resolve token expiration handling issue |
| 문서 수정 | docs(readme): update system architecture diagram |
| 코드 리팩터링 | refactor(service): simplify access control logic |
| 테스트 추가 | test(auth): add jwt reissue test cases |
| 설정 변경 | chore(docker): optimize base image for ai-server |
| 성능 개선 | perf(ai): reduce frame encoding latency |
