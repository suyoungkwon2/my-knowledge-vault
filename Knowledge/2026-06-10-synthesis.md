# Knowledge Synthesis — 2026-06-10

> 오늘의 일일 노트는 작성되지 않았습니다. Claude Code 세션 로그를 기반으로 합성합니다.

---

## 핵심 개념

- **자율 에이전트 아키텍처**: 영구(Persistent) 에이전트와 예약(Scheduled) 에이전트의 차이 — 영구 에이전트는 상태와 컨텍스트를 유지하며 지속 실행, 예약 에이전트는 정해진 시간에 작업을 트리거
- **Hermes Agent (NousResearch)**: Docker 기반 자율 AI 에이전트 프레임워크. 로컬 또는 VPS에서 실행 가능하며, `.hermes/config.yaml`로 동작 구성
- **Obsidian PKM**: 마크다운 기반 개인 지식 관리(Personal Knowledge Management) 도구. Daily Notes, Templates, 플러그인 시스템으로 구조화된 지식 축적 가능
- **Claude Code Scheduled 기능**: Claude Code의 자동화 트리거를 이용해 반복 작업(지식 합성, 일일 루틴)을 자율적으로 실행하는 패턴

## 주요 결정 / 발견

- **클라우드 이전 결정**: 로컬 디스크 공간 부족(Colima + Docker 사용량 과다)으로 Hermes Agent를 Fly.io에 배포하기로 결정. 이전 완료 후 로컬 데이터 삭제 예정
- **Level 1 과제 방향**: Codex Automations 대신 Claude Code의 Scheduled 기능을 선택 — 매일 나눈 대화와 작업 내역을 지식으로 저장하는 자동화 루틴 설계
- **Obsidian 첫 도입**: 교수의 권고에 따라 처음으로 Obsidian 설정. Daily Note 템플릿, 핵심 플러그인 활성화, Knowledge 폴더 구조 구성 완료
- **Knowledge Vault 범위 확장**: 기존 Claude 대화 전용에서 Claude Code 세션 로그까지 포함하도록 `parse_cc_sessions.py` 스크립트와 `.env` 확장

## Claude Code 작업

**프로젝트: MYAGENT (HW9)**

- **세션 1 — Hermes Agent Docker 설치**
  - NousResearch Hermes Agent 이미지 pull 시도
  - Colima 디스크 사용량 확인 및 공간 부족 문제 진단
  - `.hermes/.env`, `config.yaml`, `settings.local.json` 구성 파일 작성
  - 사용 도구: Bash×92, Edit×6, WebFetch×4

- **세션 2 — Knowledge Vault → Claude Code 세션 포함으로 확장**
  - Claude Code 로컬 세션 저장 구조(`~/.claude/`) 분석
  - `parse_cc_sessions.py` 파서 스크립트 작성
  - Fly.io 배포를 위한 `Dockerfile`, `entrypoint.sh`, `fly.toml` 작성
  - 사용 도구: Bash×52, Edit×6, Write×5

- **세션 3 — Obsidian 설정 및 일정 자율화 루틴 구성**
  - Obsidian vault 초기화 (`app.json`, `core-plugins.json`, `daily-notes.json`, `templates.json`)
  - Daily Note 템플릿 작성 (`Templates/Daily Note Template.md`)
  - 2026-06-09 일일 노트 생성
  - Claude Code Scheduled 기능으로 매일 지식 합성 자동화 설정
  - 사용 도구: Bash×32, Read×7, Write×7, RemoteTrigger×7

## 탐구할 질문

- Hermes Agent의 자율성 수준은 실제로 어느 정도인가? 다른 에이전트 프레임워크(AutoGPT, CrewAI 등)와 어떻게 다른가?
- Fly.io 무료 티어로 Hermes Agent를 안정적으로 운영할 수 있는가? 비용 구조는?
- Obsidian의 Graph View를 활용해 지식 간 연결을 시각화하면 어떤 인사이트를 얻을 수 있을까?
- 예약 자율 에이전트가 매일 생성하는 지식 합성의 품질을 어떻게 평가하고 개선할 수 있는가?
- 클라우드에서 실행되는 에이전트의 보안과 프라이버시를 어떻게 보장할 것인가?

## 연결되는 주제

- **자율 에이전트 설계** ↔ **PKM(개인 지식 관리)**: 에이전트가 자동으로 지식을 수집·정리하는 시스템 — AI와 인간의 지식 협업 모델
- **Docker/Colima** ↔ **Fly.io**: 로컬 컨테이너 실행의 한계(디스크)와 클라우드 배포의 이점 간 트레이드오프
- **Scheduled Automation** ↔ **Obsidian Daily Notes**: 자동화된 루틴이 구조화된 노트 시스템과 결합할 때 지식 축적의 복리 효과
- **Claude Code 세션 파싱** ↔ **지식 그래프**: 작업 이력을 구조화하면 미래의 유사 문제 해결에 참조 가능한 패턴 데이터베이스가 됨
