# 요청한 도구 7종

이 문서는 사용자가 명시한 도구 모두의 재설치용 구성을 보관합니다. 실행 파일, 패키지 소스 전체, 인증정보를 복사한 백업은 아닙니다.

| 도구 | 종류 | 목적 | 저장 위치 |
|---|---|---|---|
| Sequential Thinking | 로컬 stdio MCP | 복잡한 문제를 단계로 나누고 가설·검증 계획 정리 | mcp/requested-tools.example.toml |
| Context7 | 원격 HTTP MCP | 라이브러리 문서 검색 | 같은 파일 |
| GitHub | 원격 HTTP MCP | 저장소·이슈·PR 작업 | 같은 파일 |
| Figma | 원격 HTTP MCP | 디자인 문맥 조회 및 지원되는 디자인 작업 | 같은 파일 |
| pandas | Python 라이브러리 | 표 데이터 정리·집계 | python/requirements.txt |
| DuckDB | Python에서 사용하는 분석 DB | SQL 집계·데이터 조회 | 같은 파일 |
| pytest | Python 테스트 프레임워크 | 계산·처리 코드 검증 | 같은 파일 |

pandas·DuckDB·pytest 자체는 MCP나 Codex Skill이 아닙니다. 함께 사용할 신규 스킬은 `skills/python-data-workflow/SKILL.md`에 보관합니다. 기존 `cofa-data-review` 스킬과 OpenAI Docs MCP 예시도 유지합니다.

## MCP 설치 및 연결

1. `mcp/requested-tools.example.toml`에서 필요한 섹션만 기존 로컬 Codex 설정에 병합합니다. 같은 이름의 서버 또는 동일 기능의 플러그인이 이미 있으면 중복 등록하지 않습니다.
2. Sequential Thinking은 Node.js와 npm/npx가 필요합니다. 예시는 Windows용 실행 방식입니다. 다른 운영체제는 파일의 주석대로 변경합니다. 최초 실행 시 npm 패키지를 다운로드할 수 있습니다. 검증 후 패키지 버전을 고정하세요.
3. Context7은 계정에서 발급한 키를 로컬 `CONTEXT7_API_KEY` 환경변수로 제공합니다. 설정에는 키 이름만 저장합니다.
4. GitHub는 필요한 저장소와 작업에 맞는 권한의 PAT를 로컬 `GITHUB_MCP_TOKEN` 환경변수로 제공합니다. 연결된 GitHub 플러그인의 인증이 이 별도 서버로 자동 이전되지는 않습니다.
5. Figma는 계정 로그인과 파일 접근 권한이 필요합니다. Codex 앱에서는 공식 Figma 플러그인 설치가 권장되며, 수동 MCP 연결만으로 공식 Figma Skills까지 설치되지는 않습니다. CLI 수동 구성에서는 `codex mcp login figma`로 로그인합니다.
6. 사용할 서버의 `enabled = false`를 로컬에서 `true`로 변경하고 `codex mcp list`를 확인합니다. 환경변수를 변경했다면 이를 읽을 수 있도록 Codex를 다시 시작합니다.

.env 자동 로딩은 가정하지 않습니다. 실제 비밀값을 터미널 기록, 문서 또는 GitHub에 붙여넣지 마세요.

### 연결 확인 예시

- Sequential Thinking: 합성 연습 문제를 주고 검증 계획과 결론 요약을 요청합니다.
- Context7: 설치한 pandas 버전에 맞는 결측값 처리 문서를 요청합니다.
- GitHub: 이 저장소의 파일 목록을 조회합니다. 쓰기 작업은 사용자가 요청한 범위에서 수행합니다.
- Figma: 접근 가능한 연습용 디자인 링크의 구조를 조회합니다.

이 요청에서 인증이나 실제 MCP 연결 테스트는 수행하지 않았습니다.

## Python 도구 설치

저장소 루트에서 Python 3.11 이상을 사용해 별도 환경을 만듭니다. 선택한 패키지 버전의 Python 지원 범위도 확인하세요.

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r cofa-probe-toolkit/python/requirements.txt
.\.venv\Scripts\python.exe -c "import pandas, duckdb, pytest; print(pandas.__version__, duckdb.__version__, pytest.__version__)"
```

macOS/Linux:

```sh
python3 -m venv .venv
.venv/bin/python -m pip install -r cofa-probe-toolkit/python/requirements.txt
.venv/bin/python -c "import pandas, duckdb, pytest; print(pandas.__version__, duckdb.__version__, pytest.__version__)"
```

가상환경은 업로드하지 않습니다. 기존 루트 .gitignore를 바꾸지 않으려면 로컬 `.git/info/exclude`에 `.venv/`를 추가하세요.

requirements.txt는 세 패키지를 설치하는 입력 파일이며, 버전이 고정된 lock 파일은 아닙니다. 동작 검증 후 확인한 버전을 별도로 기록하세요. 환경 전체를 무분별하게 freeze하여 개인 경로나 사설 패키지 주소를 커밋하지 않습니다.

pytest로 프로젝트 테스트를 실행할 때는 해당 환경의 Python으로 `python -m pytest`를 실행합니다. 테스트 파일이 없는 상태의 실행을 성공 검증으로 기록하지 않습니다.

## 공식 출처

2026-10-29 확인:
- [Sequential Thinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)
- [Context7 Codex 설정](https://context7.com/docs/clients/codex)
- [GitHub MCP](https://github.com/github/github-mcp-server)
- [Figma MCP 설치](https://developers.figma.com/docs/figma-mcp-server/remote-server-installation/)
- [pandas](https://github.com/pandas-dev/pandas)
- [DuckDB Python](https://github.com/duckdb/duckdb-python)
- [pytest](https://github.com/pytest-dev/pytest)
