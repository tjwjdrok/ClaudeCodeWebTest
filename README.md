# Claude Code Web Test Repository

Claude Code Web 사용법과 프롬프트 작성 규칙을 정리한 테스트 레포지토리입니다.

## 목차

- [Claude Code Web이란?](#claude-code-web이란)
- [시작하기](#시작하기)
- [효과적인 프롬프트 작성법](#효과적인-프롬프트-작성법)
- [CLAUDE.md 작성 가이드](#claudemd-작성-가이드)
- [베스트 프랙티스](#베스트-프랙티스)
- [주요 기능](#주요-기능)
- [제한사항](#제한사항)
- [유용한 팁](#유용한-팁)

## Claude Code Web이란?

브라우저에서 사용하는 Claude의 AI 코딩 어시스턴트입니다. GitHub와 연동되어 비동기적으로 코딩 작업을 수행합니다.

**주요 특징:**
- 브라우저 기반 (설치 불필요)
- GitHub 네이티브 통합
- 격리된 샌드박스 환경
- 비동기 작업 실행

**접속:** `claude.ai/code`

## 시작하기

### 사전 요구사항
- Claude Pro ($20/월) 또는 Max 구독
- GitHub 계정

### 초기 설정 (5단계)

1. **`claude.ai/code` 방문**
2. **GitHub 계정 연결** - OAuth 인증
3. **GitHub App 설치** - 브랜치/PR 생성 권한 부여
4. **기본 환경 선택** - 런타임 및 네트워크 설정
5. **첫 작업 제출** - 원하는 작업 설명

### 예제

```
Task: "React + TypeScript로 반응형 버튼 컴포넌트를 만들어줘.
       유닛 테스트와 접근성 기준도 포함해서."

Claude가 자동으로:
- 코드베이스 분석
- 필요한 파일 생성
- 새 브랜치에 푸시
- PR 준비 완료
```

## 효과적인 프롬프트 작성법

### 1. 명확하고 구체적으로 작성

```markdown
# ❌ 나쁜 예
"UI가 느려"

# ✅ 좋은 예
"검색 결과가 많을 때 타이핑과 스크롤이 느림.
 메인 스레드를 블로킹하는 코드를 찾아서 비동기로 변경해줘."
```

### 2. 구조화된 형식 사용

XML, JSON, Markdown 등을 활용하면 Claude가 더 잘 이해합니다:

```xml
<task>
  <objective>사용자 대시보드 구축</objective>
  <requirements>
    <requirement>프로필 카드 표시</requirement>
    <requirement>최근 활동 피드</requirement>
    <requirement>데이터 내보내기 기능</requirement>
  </requirements>
  <constraints>
    <constraint>2초 이내 로딩</constraint>
    <constraint>모바일 반응형</constraint>
    <constraint>WCAG 2.1 AA 준수</constraint>
  </constraints>
</task>
```

### 3. 시각적 자료 포함

- 현재 상태 스크린샷
- 디자인 목업
- 에러 로그
- 성능 메트릭

### 4. 단계적 접근

1. **Explore**: 코드베이스 구조 먼저 분석
2. **Plan**: 상세 사양 및 마일스톤 작성
3. **Code**: To-do 리스트와 함께 구현
4. **Commit**: PR 워크플로우로 리뷰 및 병합

### 5. 피해야 할 것들

- ❌ 과도한 세부 지시 (마이크로매니징)
- ❌ 불필요한 추상화 요청
- ❌ 작업별 지시사항을 CLAUDE.md에 포함
- ❌ 린터로 할 일을 Claude에게 시키기

## CLAUDE.md 작성 가이드

레포지토리 루트에 `CLAUDE.md` 파일을 생성하여 프로젝트 정보를 제공합니다.

### 권장 구조 (300줄 이하로 간결하게)

```markdown
# 프로젝트 개요

## 기술 스택
- Frontend: React 18 + TypeScript
- Backend: Node.js + Express
- Database: PostgreSQL
- Testing: Jest + React Testing Library

## 프로젝트 구조
```
src/
  ├── components/    # React 컴포넌트
  ├── hooks/         # 커스텀 훅
  ├── utils/         # 유틸리티 함수
  └── tests/         # 테스트 파일
```

## 주요 명령어
- `npm install` - 의존성 설치
- `npm run dev` - 개발 서버 시작
- `npm test` - 테스트 실행
- `npm run lint` - 코드 스타일 체크

## 테스트 요구사항
모든 새 기능은 반드시:
- 80% 이상 커버리지의 유닛 테스트
- 필요시 통합 테스트
- UI 변경 시 접근성 테스트

## 코드 스타일
루트의 `.eslintrc.json` 설정을 따릅니다.
```

### 포함할 것 vs 제외할 것

**✅ 포함:**
- 기술 스택 및 버전
- 프로젝트 구조 개요
- 필수 설정 명령어
- 테스트 요구사항
- 공통 워크플로우 패턴

**❌ 제외:**
- 세부 코드 스타일 규칙 (린터 사용)
- 줄 길이, 들여쓰기 표준
- 주석 스타일
- 파일 명명 규칙 (린터 사용)

### Progressive Disclosure 패턴

메인 CLAUDE.md는 간결하게, 상세 문서는 별도 파일로:

```markdown
# 프로젝트 문서

## 빠른 시작
[getting-started.md](./docs/getting-started.md) 참고

## 아키텍처
[architecture.md](./docs/architecture.md) 참고

## 개발 가이드
[development-guide.md](./docs/development-guide.md) 참고
```

## 베스트 프랙티스

### 1. 코딩 전에 리서치

```
"먼저 현재 인증 시스템이 어떻게 구현되어 있는지 분석해줘"
```

Claude에게 코드베이스를 먼저 탐색하게 하면 성공률이 높아집니다.

### 2. 스펙 먼저 작성

구현 전에 요구사항, 범위, 마일스톤, 성공 기준을 포함한 사양서 작성을 요청하세요.

### 3. TDD (테스트 주도 개발) 적용

```
"먼저 실패하는 테스트를 작성해줘.
 그 다음 테스트를 통과하는 코드를 구현해줘."
```

### 4. Extended Thinking 활용

복잡한 문제에 대해:

```
"이 아키텍처 결정에 대해 신중하게 생각해줘"
"think harder about the trade-offs"
```

Claude가 더 많은 연산 시간을 할애하여 깊이 있는 솔루션을 제공합니다.

### 5. 실시간 피드백으로 조정

작업 진행 중 댓글로 방향 조정 가능:
- 진행 상황 실시간 모니터링
- 필요시 방향 수정 요청
- 설명이나 대안 요청

### 6. 컨텍스트 관리

- `/clear` 명령어로 집중된 컨텍스트 유지
- 긴 작업에서 컨텍스트 비대화 방지
- 관련 없는 작업은 새 대화 시작

## 주요 기능

### 지원 언어 & 기술
- **언어**: Python, Node.js, Ruby, PHP, Java, Go, Rust, C++
- **데이터베이스**: PostgreSQL 16, Redis 7.0
- **웹 프레임워크**: 모던 웹 개발 스택 전체 지원

### 핵심 기능

**코드 개발**
- 자연어 설명으로 완전한 기능 구축
- 코드베이스 전체 분석으로 디버깅
- 여러 파일에 걸친 코드 생성/리팩토링

**지능형 분석**
- 자동 코드 리뷰 및 PR 분석
- 버그 및 보안 취약점 탐지
- 아키텍처 개선 제안

**자동화**
- 반복적인 개발 작업 자동화
- 여러 레포지토리 배치 처리
- 테스트 생성 및 검증

### 병렬 실행

플랜에 따라 3-10개의 동시 작업 가능 (레이트 리밋 고려)

## 제한사항

### 리소스 제약

**파일 & 레포지토리 크기**
- 최대 파일 크기: 1MB
- 최대 레포지토리 크기: 500MB
- 500MB 초과 시: 느린 클론, 타임아웃 위험

**컴퓨팅 리소스**
- 작업당 RAM: 4GB
- 작업당 디스크: 10GB

**레이트 리밋**
- Claude/Claude Code 전체 사용량과 공유
- 병렬 작업은 비례적으로 소비

### 플랫폼 지원

**Git 호스팅**
- ✅ GitHub만 현재 지원
- ⏳ GitLab, Bitbucket: 2026년 Q2-Q3 예정
- 💡 비-GitHub 레포는 "Open in CLI" 사용

**브라우저**
- 표준 웹 브라우저 지원
- 모바일 브라우저 미지원

### 네트워크 & 보안

**네트워크 접근 모드**
- **제한 모드 (기본)**: 승인된 도메인만
  - GitHub, npm, PyPI, 메이저 클라우드 제공자
- **오프라인 모드**: 완전 오프라인
- **전체 인터넷 모드**: 제한 없음 (신뢰 레포만)

**샌드박스 제약**
- 로컬 시스템 파일 접근 불가
- SSH 키 사용 불가
- 세션 간 영구 저장소 없음
- 하드코딩된 자격 증명 접근 불가

## 유용한 팁

### 작업 성공률 높이기

**체크리스트 활용**
```
"Markdown 파일에 체크리스트를 만들어서 진행 상황을 추적해줘"
```

**시각적 반복**
```
"현재 UI 스크린샷을 첨부했어.
 디자인 목업과 일치하도록 개선해줘."
```

### 워크플로우 최적화

**로컬 연동**
- "Open in CLI" 버튼으로 로컬에서 계속 작업
- 세션 컨텍스트 보존

**CI/CD 통합**
- Claude가 파이프라인 실패 분석 가능
- GitHub Actions 통합

### 트러블슈팅

**작업 타임아웃**
- 레포지토리 크기 축소 (>500MB 문제)
- 더 작고 집중된 작업으로 분할

**레이트 리밋 초과**
- 병렬 작업 수 줄이기
- 시간 간격 두고 요청

**네트워크 이슈**
- 네트워크 접근 모드 확인
- 도메인이 허용 목록에 있는지 확인

## 참고 자료

### 공식 문서
- [Claude Code Overview](https://code.claude.com/docs/en/overview)
- [Claude Code on the Web](https://code.claude.com/docs/en/claude-code-on-the-web)
- [Claude Prompt Engineering](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices)

### 커뮤니티
- [ClaudeLog - 가이드 & 베스트 프랙티스](https://claudelog.com/)
- [Awesome Claude Code](https://github.com/hesreallyhim/awesome-claude-code)
- [HumanLayer CLAUDE.md 가이드](https://www.humanlayer.dev/blog/writing-a-good-claude-md)

### 로드맵 (2026)
- Q1: VS Code 확장 (로컬 우선 실행)
- Q2: GitLab, Bitbucket 지원
- Q3: 모바일 접근 (iOS/Android)
- Q4: 커스텀 모델 파인튜닝 (엔터프라이즈)

## 핵심 요약

### 10가지 골든 룰

1. ✅ **CLAUDE.md 준비** (300줄 이하로 간결하게)
2. ✅ **코딩 전에 계획** (탐색 및 사양 작성에 시간 투자)
3. ✅ **구체적인 프롬프트** (모호한 요청 → 평범한 결과)
4. ✅ **구조화된 형식** (XML, JSON, Markdown 라벨)
5. ✅ **피드백으로 반복** (후속 댓글로 작업 조정)
6. ✅ **제한사항 이해** (파일 크기, 레포 크기, 네트워크 접근)
7. ✅ **보안 활용** (Gvisor 샌드박싱)
8. ✅ **철저한 테스트** (테스트 먼저, 구현 나중에)
9. ✅ **레이트 리밋 모니터링** (동시 작업이 계정 리밋 공유)
10. ✅ **학습 문서화** (팀과 발견 사항 공유)

---

**마지막 업데이트**: 2026년 1월
**문서 버전**: 1.0

## License

[MIT](LICENSE)
