# 최다영

**"설계부터 트러블슈팅까지 끝까지 책임지는 개발자"**
문제의 겉면이 아니라 원인을 먼저 보는 백엔드 개발자입니다.

📮 enqn12_14@naver.com &nbsp;|&nbsp; 🔗 [github.com/dndkd97](https://github.com/dndkd97) &nbsp;|&nbsp; 📖 [Notion](https://app.notion.com/p/43af1d1d117583089d1301968d5084db)

<br>

## How I Work

- **원인을 먼저 본다** — 에러 메시지 하나로 끝내지 않고, 계층(뷰-컨트롤러-매퍼)을 하나씩 재현하며 근본 원인을 추적합니다
- **영향 범위를 먼저 그린다** — 기능 하나를 바꾸기 전에 연관 데이터·다른 모듈에 미치는 영향을 먼저 검토합니다
- **협업 규격을 문서로 남긴다** — API 스펙, DB 설계, 트러블슈팅 내역을 팀과 공유해 같은 문제가 반복되지 않게 합니다
  
## Skills

**Backend**
`Java` `Spring Boot` `Spring Security` `JWT` `Redis` `MyBatis` `JPA` `Oracle DB` `MySQL`

**Frontend**
`React` `Redux Toolkit` `redux-saga` `Thymeleaf` `Ant Design`

**Data & Analytics**
`Python` `Django` `Pandas` `Chart.js`

**Infra & Collaboration**
`AWS EC2` `Nginx` `GitHub Actions` `Git Flow` `Swagger`

**AI / API**
`OpenAI GPT API` `RAG` `Google Docs/Drive API` `Discord Webhook` `PDFBox`

<br>

## Projects

### 🏢 SpringBreeze ERP — 사내 통합 ERP 시스템
4인 팀 프로젝트 · **프로젝트 / 프로젝트 멤버 / 태스크 / 공지** 모듈 전담 → v3에서 **채용관리(RAG)** 모듈 신규 구축 → v4에서 **채용 데이터 분석 서버**(Python/Django/Pandas) 단독 추가 개발 및 배포

| 버전 | 스택 | GitHub |
|---|---|---|
| v4 | Python + Django + Pandas + AWS EC2/Nginx/GitHub Actions (단독) | [SBErpV4](https://github.com/dndkd97/sberp) |
| v3 | Spring Boot 3 + JPA + JWT/Redis + Next.js(React) + OpenAI GPT API | [SBErpV3](https://github.com/dndkd97/SB_ERP_V3) |
| v2 | Spring Boot + MyBatis + Thymeleaf + Oracle | [SBErpV2](https://github.com/dndkd97/SB_ERP_V2) |
| v1 | Spring MVC + JSP + MyBatis + MySQL | [SBErpV1](https://github.com/dndkd97/SB_ERP_V1) |

**핵심 구현**
- **태스크 의존성 & 병목(Critical Path) 탐색**: `parent_task_id` 자기참조 트리 + 재귀 CTE + DFS 순환탐지. "본인은 지연됐지만 부모는 정상"인 태스크를 시발점으로 판별하는 자체 알고리즘 설계, Frappe Gantt에 강조 표시 연동, 서브트리 단위 비관적 락(`SELECT FOR UPDATE WAIT 5`)으로 동시 수정 시 정합성 확보
- **채용관리(RAG) 모듈**: Recruit/Applicant/Resume/ResumeChunk 설계 및 전 계층 구현, Oracle 18c XE의 VECTOR 미지원을 JSON/CLOB 저장 + Java 코사인 유사도 계산으로 우회, GPT 프롬프트 기반 적합도(fit_score) 평가
- **인증 체계 이원화**: 사내 직원 JWT 인증과 지원자용 소셜 로그인(Kakao/Naver/Google)을 완전히 분리된 라우팅으로 구성, provider+providerId 소유권 검증 및 Redis 기반 Refresh Token TTL 관리로 IDOR 차단
- **하이브리드 Persistence 아키텍처**: 기존 복합 SQL 모듈은 MyBatis 기반 RestController API로 전환, 신규 채용 모듈은 JPA(Entity-Repository)로 설계 — 이력 보존용 연관관계(Recruit-Applicant)는 Cascade 미적용, 실제 소유 관계(Applicant-Resume)는 `cascade=ALL + orphanRemoval` 차등 적용
- **Spring Boot ↔ Django MSA 데이터 연동**: 오라클 통계 데이터를 Django REST API로 송수신하는 파이프라인 구축, Pandas로 합계·점유율 가공(`update_or_create`로 중복 적재 방지), Chart.js + `json_script` 필터로 대시보드 시각화
- **채용 데이터 분석 서버 구축 & 단독 배포 (v4)**: 채용관리 배포 이후 통계 요구에 대응해 Python/Django/Pandas 기반 읽기 전용 분석 서버를 단독 설계·구축, 전형 파이프라인(RECEIVED→HIRED) 전환율·정체율과 월별 지원자 추이를 산출하는 내부 API 2종 개발, 동일 EC2에 별도 프로세스로 추가 배포 후 Nginx 경로 라우팅과 GitHub Actions CI/CD 구성까지 단독 진행
- **파일 저장 구조 재설계**: 로컬 디스크 저장의 팀원 간 미공유 문제를 Oracle BLOB 저장 + 전용 다운로드 API로 재설계
- **보안 취약점 점검**: `comId` 검증 공통화(`SecurityUtil.checkComIdAccess`), `ROLE_ADMIN` 권한 오분류 수정(`isRoot`/`isAdminOrRoot` 분리)
- **운영 자동화**: GPT 기반 프로젝트 리스크 분석 → Discord 알림, 주간 리포트 Google Docs 자동화(`@Scheduled`), 개인 PDF 리포트(PDFBox 표지 제거) 생성
- **API 규격화 & 협업**: `@Schema(hidden=true)`/`@Valid` 정비, 중앙 CORS 설정 통합, Swagger로 프론트-백엔드 DTO 사전 협의, Git Flow 브랜치 전략 준수

<br>


## Career Path

| 기간 | 활동 |
|---|---|
| 2026.03 ~ 2026.10 | AI 활용 풀스택 부트캠프 (더조은컴퓨터아카데미) — Java/Spring 백엔드, React 프론트, Git/CI-CD |
| 2017.03 ~ 2021.02 | 경운대학교 항공소프트웨어공학과 졸업 |
