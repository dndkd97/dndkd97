# 최다영

**"설계부터 트러블슈팅까지 끝까지 책임지는 개발자"**
문제의 겉면이 아니라 원인을 먼저 보는 백엔드 개발자입니다.

📮 enqn12_14@naver.com &nbsp;|&nbsp; 🔗 [github.com/dndkd97](https://github.com/dndkd97)

<br>

## Skills

**Backend**
`Java` `Spring Boot` `Spring Security` `JWT` `Redis` `MyBatis` `JPA` `Oracle DB`

**Frontend**
`React` `Redux Toolkit` `redux-saga` `Thymeleaf` `Ant Design`

**Infra**
`AWS EC2` `Nginx` `Git / GitHub Actions`

**AI / API**
`OpenAI GPT API` `RAG` `Google Docs/Drive API` `Discord Webhook` `Swagger`

<br>

## Projects

### 🏢 SpringBreeze ERP — 사내 통합 ERP 시스템
4인 팀 프로젝트 · **프로젝트 / 프로젝트 멤버 / 태스크** 모듈 전담 → v3에서 **채용관리(RAG)** 모듈 신규 구축

| 버전 | 스택 | GitHub |
|---|---|---|
| v3 | Spring Boot 3 + JPA + JWT/Redis + Next.js(React) + OpenAI GPT API | [SBErpV3](https://github.com/yoonguri988/spring-breeze-erp/tree/main/spring-breeze-erp-v3) |
| v2 | Spring Boot + MyBatis + Thymeleaf + Oracle | [SBErpV2](https://github.com/yoonguri988/spring-breeze-erp/tree/main/spring-breeze-erp-v2) |
| v1 | Spring MVC + JSP + MyBatis + MySQL | [SBErpV1](https://github.com/dndkd97/SB_ERP_V1) |

**핵심 구현**
- **태스크 의존성 & 병목(Critical Path) 탐색**: `parent_task_id` 자기참조 트리 + 재귀 CTE + DFS 순환탐지. "본인은 지연됐지만 부모는 정상"인 태스크를 시발점으로 판별하는 자체 알고리즘 설계, Frappe Gantt에 강조 표시 연동
- **채용관리(RAG) 모듈**: Recruit/Applicant/Resume/ResumeChunk 설계 및 전 계층 구현, Oracle 18c XE의 VECTOR 미지원을 JSON/CLOB 저장 + Java 코사인 유사도 계산으로 우회
- **인증 체계 이원화**: 사내 직원 JWT 인증과 지원자용 소셜 로그인(Kakao/Naver/Google)을 완전히 분리된 라우팅으로 구성, provider+providerId 소유권 검증으로 IDOR 차단
- **보안 취약점 점검**: `comId` 검증 공통화(`SecurityUtil.checkComIdAccess`), `ROLE_ADMIN` 권한 오분류 수정
- **운영 자동화**: GPT 기반 프로젝트 리스크 분석 → Discord 알림, 주간 리포트 Google Docs 자동화, 개인 PDF 리포트(PDFBox) 생성

<br>

## Troubleshooting Highlight

> 태스크 순환 참조 탐지 로직에서 NPE 발생

- **원인**: `isCyclic` 로직의 `.map().findFirst()` 처리 순서 오류
- **해결**: DFS 기준으로 탐색 순서 재정리
- **학습**: 재귀/그래프 탐색 로직은 조건 순서 하나로도 예외 지점이 달라진다는 것을 체감, 이후 순서를 먼저 문서화하고 구현

<br>

## Career Path

| 기간 | 활동 |
|---|---|
| 2026.03 ~ 2026.10 | AI 활용 풀스택 부트캠프 (더조은컴퓨터아카데미) — Java/Spring 백엔드, React 프론트, Git/CI-CD |
| 2017.03 ~ 2021.02 | 경운대학교 항공소프트웨어공학과 졸업 |
