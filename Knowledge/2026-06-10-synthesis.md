# Knowledge Synthesis — 2026-06-10

## 핵심 개념
- **Hermes Agent**: NousResearch의 자율 에이전트 프레임워크로, Docker 기반으로 실행하는 지속적 에이전트
- **지식 볼트(Knowledge Vault)**: 클로드 대화 내역과 Claude Code 작업 내역을 통합하는 개인 지식 관리 시스템
- **자율 에이전트 레벨 구분**: Level 1(스케줄된 일일 루틴) vs Level 2(지속적 자율 에이전트)
- **Obsidian**: 마크다운 기반 개인 지식 관리 도구 — 일일 노트, 템플릿, 플러그인 생태계 지원
- **Claude Code 세션 파싱**: 로컬 세션 로그를 파싱해 지식 자산으로 변환하는 파이프라인 설계

## 주요 결정 / 발견
- Hermes Agent를 로컬 Docker 대신 **Fly.io 클라우드**로 이전하기로 결정 — 로컬 디스크 공간 부족 문제의 현실적 해결책
- Claude Code 세션 로그를 지식 볼트에 포함시키는 **시스템 확장** 설계 완료 (`parse_cc_sessions.py` 작성)
- 일일 자율 루틴으로 "당일 대화·작업 내용을 지식으로 저장"하는 방식 채택 — 교수 권장 Obsidian 활용과 연계
- Obsidian Daily Notes + Templates 플러그인으로 **일일 노트 자동화** 기반 구축
- 클라우드 이전 후 로컬 데이터 삭제로 저장 공간 절약 원칙 확립

## Claude Code 작업
### MYAGENT 프로젝트 (3세션, 총 도구 호출 약 180+회)

1. **Hermes Agent 설치 및 클라우드 이전** (`Bash×92`)
   - Docker 이미지 풀링, Colima 환경 점검
   - Fly.io 배포를 위한 `Dockerfile`, `entrypoint.sh`, `fly.toml` 작성
   - 디스크 부족 문제로 로컬 → 클라우드 전략 전환

2. **지식 볼트 확장: Claude Code 세션 통합** (`Bash×52`)
   - Claude Code 로컬 히스토리 구조 분석 (`~/.claude/projects/*/memory/`)
   - `parse_cc_sessions.py` 개발 — 세션 파싱 및 GitHub 업로드 자동화
   - `.env` 파일(`cc-parser.env`)로 설정 분리

3. **Obsidian 연동 및 스케줄 자동화** (`Bash×32`, `RemoteTrigger×7`)
   - `MyKnowledgeVault` Obsidian 볼트 초기화 및 플러그인 설정
   - Daily Note Template 작성, 일일 노트 자동 생성 구성
   - Claude Code `RemoteTrigger`를 활용한 자동화 루틴 등록

## 탐구할 질문
- Fly.io 무료 티어로 Hermes Agent를 **지속적으로** 운영하기에 충분한가? 비용 구조는?
- 클라우드 기반 에이전트가 로컬 파일 시스템과 상호작용해야 할 때의 아키텍처 패턴은?
- Obsidian Daily Notes를 자동 생성하는 것과 직접 작성하는 것 사이에서 **지식의 깊이**를 어떻게 유지할까?
- Level 2 지속적 에이전트가 실질적으로 유용하려면 어떤 트리거·목표·경계가 필요한가?
- Claude Code 세션 파서가 놓치는 맥락은 무엇이고, 어떻게 보완할 수 있을까?

## 연결되는 주제
- 자율 에이전트 아키텍처 (Hermes, Claude Code Automations, RemoteTrigger)
- 개인 지식 관리 (PKM) 시스템과 AI 통합 — Obsidian + Claude 시너지
- 클라우드 vs 로컬 컴퓨팅 트레이드오프 (디스크·비용·보안)
- Docker 컨테이너화와 Fly.io 배포 패턴
- 지식 합성 자동화 파이프라인 설계
