# COFA Probe 준비용 Skills / MCP 템플릿

이 폴더는 SK하이닉스 COFA Probe 시험 준비에 활용할 수 있는 **신규 작성 관리 템플릿**입니다. 사용자가 받은 Skills/MCP를 수집하거나 그대로 백업한 결과가 아닙니다. 실제 설치 목록, 공식 시험 범위, 데이터 형식, 허용 도구는 미확인입니다. 공식 시험 자료나 정답을 제공하지 않습니다.

## 구성

- `skills/cofa-data-review/SKILL.md`: 제공된 데이터의 품질과 분석 결과를 점검하는 스킬 예시
- `mcp/config.example.toml`: Codex MCP 설정 예시. 서버는 기본 비활성
- `inventory.example.json`: 실제 설치 목록을 추후 기록하기 위한 빈 목록
- `docs/SYNC.md`: 민감정보를 제외한 수동 동기화·복원 절차
- `.gitignore`: 이 폴더 안의 로컬 설정·인증·원본 데이터 제외

## 사용 순서

1. 시험 안내에서 AI, 인터넷, 외부 도구, 데이터 반출 허용 범위를 확인합니다.
2. 스킬 내용을 검토한 후 연습용 프로젝트의 `.agents/skills/cofa-data-review/SKILL.md`에 복사합니다. 같은 이름의 파일이 있으면 덮어쓰지 말고 비교합니다. 이 저장소의 `skills/`는 보관 위치이며 자동 설치 경로가 아닙니다.
3. MCP 예시 중 필요한 항목만 기존 로컬 설정에 병합합니다. 전체 설정 파일을 교체하지 않습니다. 서버 URL과 접근 범위를 검토한 뒤 필요한 항목의 `enabled`를 변경합니다.
4. 합성 또는 공개 가능한 연습 데이터로 먼저 확인합니다.
5. [동기화 안내](docs/SYNC.md)에 따라 실제 사용 항목의 출처·버전·검증 상태를 기록합니다.

예시 요청: “제공한 연습 CSV의 누락값, 중복, 단위와 결과 계산을 확인하고 사실·가정·추가 확인 항목을 구분해줘.”

MCP 없이도 이 스킬의 점검 절차를 사용할 수 있습니다. OpenAI Docs MCP는 Codex 설정 확인용이며 반도체 시험 규격이나 COFA 자료를 제공하는 서버가 아닙니다.

## 보관 원칙

공개 저장소입니다. 비밀키·토큰·개인 절대경로·실제 내부 서버 주소·사내 데이터·비공개 시험 자료는 커밋하지 않습니다. 예시는 자동 설치나 자동 동기화를 수행하지 않습니다. 실제 환경의 동작 검증은 아직 수행하지 않았습니다.

## 공식 참고 자료

2026-10-29 확인:
- [Skills 작성 및 검색 경로](https://learn.chatgpt.com/docs/build-skills)
- [Codex MCP 설정](https://learn.chatgpt.com/docs/extend/mcp?surface=cli)
- [OpenAI Docs MCP](https://developers.openai.com/learn/docs-mcp)
