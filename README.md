<div align="center">

# On 공문서 쓰기

원고나 AI 채팅의 글을 정부 공문서 꼴 한글(HWPX) 보고서·계획서·보도자료로 만드는 원격 MCP 서버

**한국어** · [English](README.en.md)

`https://onmunseo.kr/mcp/gov`

</div>

마크다운이나 짜임(`structure`)을 보고서·계획서·결과보고서·보도자료·기안문·공고문 꼴 한글 파일로 만듭니다(`on_write_gov`) — 휴먼명조·HY헤드라인M, 장 제목 막대, □ ○ - 단계 내어쓰기, 표 캡션·단위, 계획서·결과보고서는 표지·목차까지. 양식을 따로 말하지 않으면 보고서·계획서는 응급의료 기본계획(보건복지부) 꼴로 나옵니다. 예시 양식 66종 채우기, 글을 공문서 표로, 표 자료를 그래프 그림으로, 글머리를 체계도 그림으로도 만듭니다. AI 없이 규칙으로 하며, 원고에 없는 사실·숫자는 넣지 않습니다. 표·그래프·체계도는 숫자를 하나라도 잃으면 결과 대신 까닭을 돌려주고, 공문서 쓰기는 만든 파일을 다시 읽어 원고와 견준 결과(`check`)를 함께 줍니다.

이 저장소에는 연결 안내와 설정 파일(플러그인의 작은 띄우개 하나 포함)만 있습니다(웹 화면 없음 — 화면에서 쓰려면 [On 문서 웹 편집기](https://onmunseo.kr/app/)). 서비스의 엔진·서버 코드는 공개하지 않습니다.

- 그래프·체계도·표지·목차를 같은 도구에서 넣고, 만든 글은 결재 전 점검·법령 인용 확인(On 근거)으로 이어 봅니다. 표·그래프·체계도·양식 채우기는 원문 숫자를 하나라도 잃으면 결과 대신 까닭을 내고, `on_write_gov` 는 만든 파일을 다시 읽어 원고와 견준 결과(`check`)를 함께 줍니다.
- **문서가 가는 곳:** 이 주소로 보낸 문서는 On 문서 서버(국내 데이터센터)의 메모리에서만 처리하고 끝나면 버립니다(바깥 AI 회사로 보내지 않음). 서버를 거치는 이 주소에는 공개 문서와 본인 문서만 보내고, 기관 내부 문서는 [On 문서 웹 편집기](https://onmunseo.kr/app/)에서 브라우저 안에서 처리하는 기능(한글 열기·고치기·저장, 결재 전 점검, 개인정보 가리기)으로 다룹니다 — 웹 편집기라도 첨부 글 꺼내기·글자 인식·한글 파일 만들기는 서버를 거칩니다.

**바로 가기:** [왜 쓰나](#쉽게-말하면--왜-쓰나) · [설치 안내](#설치-안내사람ai-공통) · [성능](#성능) · [도구](#무엇을-하나) · [연결하기](#연결하기) · [쓰는 예](#쓰는-예) · [손님과 열쇠](#손님과-열쇠) · [안전](#안전) · [알아 둘 점](#알아-둘-점) · [측정과 비교(참고)](#측정과-비교참고)

## 쉽게 말하면 — 왜 쓰나

| 흔한 불편 | On 공문서 쓰기에서는 |
|---|---|
| AI 채팅이 만든 한글 파일이 한컴에서 빈 쪽으로 열린다 | 같은 원고 5편에서 AI 채팅만으로 만든 파일은 3편이 한컴에서 글이 하나도 보이지 않았고, 공문서 쓰기로 만든 파일은 0편이었습니다(아래 성능) |
| □ ○ - 단계·장 제목 막대·표지·목차를 손으로 맞춘다 | 꼴은 엔진이 맞춥니다 — 둘째 줄을 첫 줄 글자 자리에 맞추고, 쪽 끝에 제목만 남기지 않습니다 |
| 표·그래프·체계도를 따로 만들어 붙인다 | `on_table`·`on_chart`·`on_diagram` 이 원문 숫자·낱말로만 그리고, 어긋나면 그림 대신 까닭을 냅니다 |
| 어떤 꼴로 써야 할지 막막하다 | 계획·보고·행사·공고·보도자료 등 예시 양식 66종에서 골라 자료를 채웁니다(`on_list_templates`·`on_fill_template`) |

**이럴 땐 없이도 됩니다:** 기관이 정해 준 서식 파일이 있으면 그 서식에 채우는 것([On HWPX 만들기](https://github.com/on-munseo/on-hwpx)의 `on_fill`)이 맞습니다. 꾸밈 없는 한 쪽 메모는 `on_write` 로 충분합니다.

<!-- ai-install -->
## 설치 안내(사람·AI 공통)

길은 셋이고 **①부터** 권합니다. 어느 길도 열쇠·로그인이 없습니다. 이 저장소(On 공문서 쓰기 — 공문서 꼴 한글 쓰기)의 도구는 ① 내 PC 판(같은 만든 이 on-munseo 의 npm 꾸러미 `on-munseo-local` — 아래 확인할 거리)에 들어 있습니다 — 「설치해 줘」라고만 하면 ① 을 붙입니다. 이 저장소의 `plugin/`(Claude Code 플러그인)은 ①과 ② 를 붙이고, `server.json`(공식 MCP 목록용)은 ③ 서버 판(이 묶음) 주소입니다. 그래프·체계도 그림(`on_chart`·`on_diagram`)만 ③에 있고, 공문서 안의 그래프·체계도는 ①에서 표로 들어갑니다.

**① 내 PC 판 — 문서를 이 컴퓨터 밖으로 보내지 않음(먼저).** 글 꺼내기·신구 대비표·개인정보 찾기·가리기·결재 전 점검·공문서 쓰기·서식 채우기·한글 파일 만들기·글 다듬기를 이 컴퓨터 안에서 합니다. 이 프로그램은 인터넷을 쓰지 않습니다(설치 뒤 `on_local_info` 로 확인 — 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작이고, 그것까지 없애려면 `npm install -g on-munseo-local` 뒤 명령을 `on-munseo-local` 로). Node.js 20 이상이 있어야 합니다.
- **지금 쓰는 AI 도구에만**(AI 가 설치할 때는 이것 — 다른 도구의 설정은 건드리지 않음)
  ```bash
  claude mcp add -s user on-local -- npx -y on-munseo-local@0.3.1
  ```
  Codex 는 `codex mcp add on-local -- npx -y on-munseo-local@0.3.1` · 윈도우 Claude Code 는 `claude mcp add -s user on-local -- cmd /c npx -y on-munseo-local@0.3.1` · Cursor·Claude 데스크톱은 설정 파일의 `"mcpServers"` 에 `"on-local": { "command": "npx", "args": ["-y", "on-munseo-local@0.3.1"] }`(윈도우 `"on-local": { "command": "cmd", "args": ["/c", "npx", "-y", "on-munseo-local@0.3.1"] }`) · VS Code 는 `code --add-mcp '{"name":"on-local","command":"npx","args":["-y","on-munseo-local@0.3.1"]}'`
- **사람이 이 PC 의 여러 AI 도구에 한 번에** — Claude Code·Claude 데스크톱·Codex·Cursor·VS Code 를 찾아 모두 등록합니다(바꾸기 전에 백업, 이미 있으면 건너뜀, 미리 보기 `--dry-run`, 되돌리기 `--undo`, ②까지 `--pair`).
  ```bash
  npx -y on-munseo-local@0.3.1 setup --pair
  ```
- **판 고정** — 위 줄은 판 번호를 적어 붙입니다(`on-munseo-local@0.3.1`). 자동으로 새 판을 받지 않고, 사람이 올릴 때만 바뀝니다(npm 에 새 판이 올라와도 이미 붙인 판은 그대로 · 인터넷이 끊겨도 한 번 받은 판은 뜸). 새 판으로 올리기: `npx -y on-munseo-local@latest setup --update`(등록된 줄의 판 번호만 새 판으로 · 바꾸기 전 백업 · 미리 보기 `--dry-run`) · 바뀐 점: [CHANGELOG](https://github.com/on-munseo/on-local/blob/main/CHANGELOG.md)

**② 짝 주소(법령) — 도구에 넣은 낱말·글만 서버로.** 법령 원문·글 속 인용 확인(On 근거)은 서버에만 있습니다. 서버로 가는 것은 넣은 법령 이름·조문 번호·인용을 확인할 글이고, 파일을 보내는 도구는 없습니다. 인용을 확인할 글에 개인정보가 있으면 ① 의 `on_mask_text` 로 가린 뒤 넣습니다.
- 지금 쓰는 도구에만(① 의 `setup --pair` 는 ② 까지 함께 붙임):
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-geungeo https://onmunseo.kr/mcp/law
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-geungeo >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-geungeo"; then printf '\n[mcp_servers.on-geungeo]\nurl = "https://onmunseo.kr/mcp/law"\n' >> "$C/config.toml"; (cd / && codex mcp get on-geungeo >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-geungeo" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-geungeo)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-geungeo]`·`url = "https://onmunseo.kr/mcp/law"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-geungeo = { url = "https://onmunseo.kr/mcp/law" }` 를 더함).
- **Cursor** `"on-geungeo": { "url": "https://onmunseo.kr/mcp/law" }` · **VS Code** `code --add-mcp '{"name":"on-geungeo","type":"http","url":"https://onmunseo.kr/mcp/law"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 근거`, 주소 `https://onmunseo.kr/mcp/law` → 「연결」

**③ 서버 판(이 묶음) — Node.js 없이 바로(공개 문서용).** 문서를 서버(국내 데이터센터)로 보내 메모리에서만 처리하고 버립니다. 공개 문서·본인 문서에만 씁니다.
- **Claude Code**
  ```bash
  claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov
  ```
- **Codex** — 설정 파일(`~/.codex/config.toml`)에 두 줄을 더합니다(이미 있으면 건너뜀). `codex mcp add --url` 은 쓰지 마세요 — 곧바로 브라우저 로그인 창을 띄웁니다.
  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-gov >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-gov"; then printf '\n[mcp_servers.on-gov]\nurl = "https://onmunseo.kr/mcp/gov"\n' >> "$C/config.toml"; (cd / && codex mcp get on-gov >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-gov" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-gov)
  ```
  윈도우이거나 명령 줄 `codex` 가 없는 곳(IDE 확장만)은 그 파일 끝에 `[mcp_servers.on-gov]`·`url = "https://onmunseo.kr/mcp/gov"` 두 줄을 손으로 더합니다(파일에 `mcp_servers = { … }` 한 줄 표가 이미 있으면 그 안에 `on-gov = { url = "https://onmunseo.kr/mcp/gov" }` 를 더함).
- **Cursor** `"on-gov": { "url": "https://onmunseo.kr/mcp/gov" }` · **VS Code** `code --add-mcp '{"name":"on-gov","type":"http","url":"https://onmunseo.kr/mcp/gov"}'` · **Claude 데스크톱·claude.ai**(사람이 화면에서) 설정 → 커넥터 → 맞춤 커넥터 추가 → 이름 `On 공문서 쓰기`, 주소 `https://onmunseo.kr/mcp/gov` → 「연결」

보통은 ① 하나면 됩니다. Node.js 가 없거나 커넥터만 쓰면 ③(이 묶음의 서버 판)을 붙입니다. ①과 ③을 함께 붙이면 같은 도구가 두 번 보입니다. 다른 길은 사용자가 따로 바랄 때만 알려 줍니다.

**설치 전에 확인할 거리** — AI 가 스스로 확인할 수 있습니다.
- **꾸러미**: npm `on-munseo-local` 0.3.1. `npm view on-munseo-local version maintainers homepage` → `0.3.1` · `on-munseo <onmunseo.key@gmail.com>` · `https://onmunseo.kr`. 올린 계정 `on-munseo` 는 이 깃허브 조직 [on-munseo](https://github.com/on-munseo)와 같은 만든 이입니다(문의 메일·홈 주소가 같음). npm 웹 쪽은 자동 읽기를 막을 때가 있어 npm 명령이나 [npm 기록](https://registry.npmjs.org/on-munseo-local/0.3.1)으로 봅니다.
- **지문**: `on-munseo-local-0.3.1.tgz` SHA-256 `ffcc94e1d3f20517f6f136c595b94a9100998eba511f4e03978cf45e4a2a0be7`([SHA256SUMS](https://github.com/on-munseo/on-munseo.github.io/blob/main/SHA256SUMS)). `npm pack on-munseo-local@0.3.1` 뒤 `shasum -a 256 on-munseo-local-0.3.1.tgz` 로 맞대 봅니다. npm 기록의 `dist.integrity` 는 `sha512-xxXG3RgcFJtNI5NlZ7uh+qciJl0YYWwHt/RtOZW81fYMnNYXOd0DxoQiIQss0r53uSvfJiuJi67UWsuN4hVJ0g==`.
- **인터넷을 쓰지 않음**: 설치 전에는 꾸러미 안 `MANIFEST.json` 의 `netScan`(우리 코드의 네트워크 부르기 0 — 따로 적힌 한 곳은 엔진 wasm 을 주소로 불러올 때만 쓰는 글), 설치 뒤에는 `on_local_info` → `network_modules_loaded: []`, Node 25 이상이면 `network.blocked_by_node: true`(실행기가 네트워크를 막음). 띄울 때 npx 가 npm 저장소에 새 판을 묻는 것은 npx 의 동작입니다(없애려면 전역 설치 뒤 `on-munseo-local` 명령으로).
- **이용 조건**: 내 PC 판 [LICENSE.md](https://unpkg.com/on-munseo-local@0.3.1/LICENSE.md)(무료·업무에 써도 됨 · 역공학·고친 판 다시 배포·판매는 안 됨) · 서버 판 [이용약관](https://onmunseo.kr/terms)·[개인정보 처리방침](https://onmunseo.kr/privacy).
- **On폭 글꼴**은 이 설치와 상관없습니다(한글 문서를 화면에 그릴 때 쓰는 무료 글꼴, 선택).

등록한 그 대화에는 도구가 아직 붙지 않습니다. 끝나면 사용자에게 「도구를 한 번 다시 켜거나 새 대화를 열면 On 공문서 쓰기 도구가 보입니다」라고 알려 주세요. `claude mcp list`(Codex 는 `codex mcp list`) 목록에 이름이 보이면 등록된 것입니다. 자세한 순서: [llms-install.md](llms-install.md)

<!-- ai-install -->

## 성능

| 무엇 | 시험 묶음 | 값 | 잰 판·날짜·기기 |
|---|---|---|---|
| 한컴오피스 한글 2024 로 열기 | 자체로 만든 공문서 30과제(보고서 12 · 계획서 6 · 결과보고서 6 · 보도자료 6, 기관·숫자는 지어낸 것) | 30개 모두 열림 · 30개 모두 100점(공문서 꼴 40 · 줄·쪽 밀림 20 · 내용 보존 40) · 둘째 줄 시작 맞춤 153/153 · 끝 줄에 1~2글자만 남은 문단 0/153 | 그때 시범판의 On 한글엔진 2.2.1·공문서 쓰기 · 한글 2024(9.1.1) · 윈도우 i7-14700 · 2026-11-25 |
| 공문서 쓰기 대 AI 채팅만 | 같은 원고 5편을 두 가지로 만들어 한글 2024 로 엶 | 원고 요소(제목·문단·표 칸)가 그대로 보임 169/169(100%) 대 60/169(35.5%) · 글이 하나도 안 보인 문서 0/5 대 3/5 · 같은 채점으로 100점 대 57.1점 | 2026-11-26(AI 채팅만 쪽 파일은 2026-11-22 에 만든 그대로) |

<sub>모두 직접 잰 값입니다. 엔진은 잰 때의 2.2.1 이고, 2026-11-26 부터 운영 엔진은 2.2.3 입니다(아직 다시 재지 않음). 30과제는 우리가 만든 과제입니다. 5편은 작은 표본이고, 「AI 채팅만」은 MCP 없이 범용 AI 코딩 도구에 같은 요청을 한 번씩 해서 만든 그대로입니다(고르거나 다시 시키지 않음). AI 와 때에 따라 그 결과는 달라질 수 있고, 사람이 한컴에서 열어 보고 다시 시키면 나아질 수 있습니다. 점수 정의는 [측정 자료](https://github.com/on-munseo/on-munseo.github.io/blob/main/docs/benchmark.md#4-만들기--한컴-한글-2024-로-연-공문서-30과제)에 있습니다.</sub>

약한 곳: 끝 줄이 짧게 남는 문단이 많습니다 — 30과제의 두 줄 이상 □·○·- 문단 153개 가운데 89개는 끝 줄이 줄 폭의 1/3 이 안 됩니다(1~2글자만 남은 문단은 0). 더 줄이려면 문장을 고쳐야 합니다.

## 무엇을 하나

| 도구 | 이름 | 하는 일 | 손님 |
|---|---|---|---|
| `on_write_gov` | 공문서 쓰기 | 마크다운·짜임을 보고서·계획서·결과보고서·보도자료·기안문·공고문 꼴 HWPX 로. 결과에 고칠 곳(`quality`)·짧게 남은 둘째 줄(`short_last_lines`)·다시 읽어 견준 결과(`check`)·쪽 그림(`preview`) | ○ |
| `on_list_templates` | 예시 양식 목록 | 예시 양식 66종(계획·보고·행사·공고·보도자료 등)의 번호·갈래·이름·쪽 수 | ○ |
| `on_fill_template` | 양식 채우기 | 예시 양식 하나에 자료(글·파일)의 문단·표를 맞는 장에 넣음. 자리가 분명하지 않은 덩이는 넣지 않고 목록(`unplaced`)으로 | ○ |
| `on_table` | 글을 공문서 표로 | 「항목: 값」·탭·쉼표·「\|」 줄을 공문서 표로, 원문 숫자 대조·합계 확인. 마크다운 표 + 한글 파일 | ○ |
| `on_chart` | 표를 그래프 그림으로 | 표 자료를 막대·꺾은선·원·가로막대 그림(PNG)으로, 숫자·막대 길이 대조 | ○ |
| `on_diagram` | 글머리를 체계도 그림으로 | □ ○ - 글머리·「가 → 나 → 다」를 단계 흐름·추진체계·구성도 그림(PNG)으로, 상자 글은 원문 낱말 그대로 | ○ |

- 손님에게 보이는 도구 6개는 2026-11-26 운영 서버에 손님으로 `tools/list` 를 불러 확인했습니다.
- 한도: `on_table` 글 2만 자·200줄·20칸 · `on_chart` 자료 2만 자 · `on_diagram` 글 4천 자·큰 항목 8개·그 아래 8개 · `on_fill_template` 자료 글 30만 자·파일 4개(하나 25MB). 결과 파일 주소는 15분 동안 열립니다.

## 연결하기

위 [설치 안내](#설치-안내사람ai-공통)의 세 길(① 내 PC 판 · ② 짝 주소 · ③ 서버 판) 가운데, 아래는 ③ 서버 판(이 묶음)을 도구마다 붙이는 자세한 법입니다.

**Claude Code** — 터미널에 한 줄(`-s user` 는 모든 폴더에서 쓰기):

```bash
claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov
```

**Claude Code 플러그인** — ① 내 PC 판 + ② 법령 짝을 붙입니다(Node.js 20 이상, 윈도우도 그대로 — 작은 띄우개 `plugin/run-local.mjs` 가 npx 를 띄움). 제품 플러그인을 여럿 깔면 내 PC 판이 여럿 떠 같은 도구가 겹쳐 보이니 하나만 까세요. 한 줄(Claude Code 2.1.275 이상):

```bash
claude plugin install on-gov --marketplace on-munseo/on-gov
```

어느 앱이든 등록한 그 대화에는 도구가 아직 붙지 않습니다. 앱을 한 번 다시 켜거나(Claude Code 터미널은 `/exit` 뒤 `claude`, VS Code 는 새 대화) 새 대화를 열면 그다음부터 씁니다. 열쇠가 없으면 로그인 단계는 건너뛰고 손님으로 씁니다.

> 문서 도구 전부와 법령 원문(On 근거)을 함께 쓰려면 이 묶음 대신 `https://onmunseo.kr/mcp` 하나를 붙이세요(권장 — [On 문서](https://github.com/on-munseo/on-munseo.github.io)). 둘 다 붙이면 같은 도구가 두 번 보입니다.
>
> 공문서 쓰기에 글 다듬기·법령 원문까지 한 주소로 붙이려면 `https://onmunseo.kr/mcp/write`(서버 이름 `on-write`) — 받은 문서에서 글을 꺼내거나 점검·가리는 도구 없이 쓰기·다듬기·법령만 모은 주소(2026-11-27).

### Claude Code — 더 보기

- 열쇠가 있으면 Claude Code 안에서 `/mcp` → `on-gov` → 인증(Authenticate)을 누르면 On 문서 로그인 창이 뜹니다. 열쇠를 넣으면 끝입니다.
- 머리말로 넣으려면 `claude mcp add --transport http -s user on-gov https://onmunseo.kr/mcp/gov --header "Authorization: Bearer <열쇠>"` 처럼 붙입니다. 이렇게 하면 열쇠가 설정 파일(`~/.claude.json`)에 남으니 로그인 창 쪽을 권합니다.
- 플러그인을 두 줄로 붙이려면(옛 판): `claude plugin marketplace add on-munseo/on-gov` 다음 `claude plugin install on-gov@on-gov`. Claude Code 대화창에서는 `/plugin marketplace add on-munseo/on-gov` → `/plugin install on-gov@on-gov`.
- 확인 `claude mcp list` · 빼기 `claude mcp remove on-gov`.

### claude.ai · Claude 데스크톱(커넥터)

설정 → 커넥터 → 「사용자 지정 커넥터 추가」(화면에 따라 「맞춤 커넥터 추가」)에서 이름 `On 공문서 쓰기`, 주소 `https://onmunseo.kr/mcp/gov` 를 넣고 「연결」을 누릅니다. 열쇠가 있으면 뜨는 On 문서 로그인 창에 넣고, 없으면 손님으로 씁니다. 요금제·판에 따라 메뉴 이름이 다르거나 이 메뉴가 없을 수 있습니다.

Claude 데스크톱을 설정 파일로 붙이려면 중계 도구 `mcp-remote` 를 씁니다(Node.js 필요). 맥 `~/Library/Application Support/Claude/claude_desktop_config.json` · 윈도우 `%APPDATA%\Claude\claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "on-gov": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://onmunseo.kr/mcp/gov"
      ]
    }
  }
}
```

열쇠를 머리말로 넣으려면 `"args"` 끝에 `"--header", "Authorization:${ON_AUTH}"` 를 더하고 `"env": { "ON_AUTH": "Bearer <열쇠>" }` 를 둡니다(쌍점 뒤를 띄우지 않는 것은 윈도우에서 인자가 갈라지지 않게 하려는 것). 저장한 뒤 Claude 데스크톱을 다시 켭니다.

### 챗GPT

1. 설정 → 앱·커넥터 → 고급 설정에서 「개발자 모드」를 켭니다(화면 판에 따라 다를 수 있음).
2. 「만들기」(사용자 MCP 서버 추가)에서 이름 `On 공문서 쓰기`, 주소 `https://onmunseo.kr/mcp/gov`, 인증은 열쇠가 있으면 「OAuth」, 없으면 「없음」을 고릅니다.
3. 연결할 때 뜨는 On 문서 로그인 창에 열쇠를 넣고, 대화 창의 도구(+) 메뉴에서 켭니다.

- 챗GPT 에는 열쇠 대신 따로 만든 출입증이 갑니다(권한·하루 몫은 열쇠와 같음). 열쇠를 끊으면 출입증도 바로 막힙니다.

### Codex

열쇠 없이는 `~/.codex/config.toml` 에 두 줄을 넣습니다:

```toml
[mcp_servers.on-gov]
url = "https://onmunseo.kr/mcp/gov"
```

- 열쇠가 없으면 `codex mcp add --url` 은 쓰지 마세요 — 곧바로 On 문서 로그인 창(브라우저)을 엽니다. 위 두 줄을 터미널 한 줄로 더하려면(이미 있으면 건너뜀):

  ```bash
  C="${CODEX_HOME:-$HOME/.codex}"; mkdir -p "$C"; touch "$C/config.toml"; if ! (cd / && codex mcp get on-gov >/dev/null 2>&1); then if cp "$C/config.toml" "$C/config.toml.bak-on-gov"; then printf '\n[mcp_servers.on-gov]\nurl = "https://onmunseo.kr/mcp/gov"\n' >> "$C/config.toml"; (cd / && codex mcp get on-gov >/dev/null 2>&1) || { cp "$C/config.toml.bak-on-gov" "$C/config.toml"; echo "자동으로 더하지 못했습니다 — config.toml 에 손으로 더해 주세요"; }; else echo "백업을 만들지 못해 그만둡니다 — config.toml 은 그대로입니다"; fi; fi; (cd / && codex mcp get on-gov)
  ```

- 열쇠가 있으면 위 두 줄을 넣은 뒤 로그인합니다: `codex mcp login on-gov`

### Cursor

`~/.cursor/mcp.json`(모든 프로젝트) 또는 프로젝트의 `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "on-gov": {
      "url": "https://onmunseo.kr/mcp/gov"
    }
  }
}
```

Cursor 가 원격 MCP 로그인(OAuth)을 하지 못하는 판이면 `"headers": { "Authorization": "Bearer <열쇠>" }` 를 더합니다(열쇠가 파일에 남습니다).

### VS Code

작업 공간의 `.vscode/mcp.json`:

```json
{
  "servers": {
    "on-gov": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/gov"
    }
  }
}
```

열쇠를 머리말로 넣되 파일에 적지 않으려면, 처음 켤 때 묻게 합니다:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "on-key",
      "description": "On 문서 열쇠",
      "password": true
    }
  ],
  "servers": {
    "on-gov": {
      "type": "http",
      "url": "https://onmunseo.kr/mcp/gov",
      "headers": {
        "Authorization": "Bearer ${input:on-key}"
      }
    }
  }
}
```

### 직접 불러 보기(curl)

도구 목록(열쇠가 있으면 `-H "Authorization: Bearer <열쇠>"` 를 더함):

```bash
curl -s https://onmunseo.kr/mcp/gov \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list"}'
```

`on_write_gov` 부르기 — 글에 따옴표·줄바꿈이 많으면 이렇게 파일로 보내면 깨지지 않습니다:

```bash
cat > call.json <<'EOF'
{"jsonrpc": "2.0", "id": 1, "method": "tools/call", "params": {"name": "on_write_gov", "arguments": {"style": "결과보고서", "markdown": "# ○○ 회의 결과보고\n\n## Ⅰ. 회의 개요\n\n○ 일시: 2026. 11. 20.(금) 14:00\n○ 장소: ○○ 회의실\n\n## Ⅱ. 주요 내용\n\n○ 교육 과정 8회 운영, 수료 214명\n"}}}
EOF
curl -s https://onmunseo.kr/mcp/gov \
  -H "Content-Type: application/json" -H "Accept: application/json, text/event-stream" \
  --data-binary @call.json
```

결과보고서 3쪽·`check.same: true`·15분 주소(`file.url`)와 사용자에게 전할 말(`tell_user`)을 받았습니다(2026-11-26, 손님). 결과 `result.content` 의 글이 답입니다. 서버는 상태를 두지 않는 방식(Streamable HTTP, POST)이라 `initialize` 없이 `tools/call` 하나로 됩니다. 브라우저로 주소를 열면 안내 쪽이 보입니다.

## 쓰는 예

| 이렇게 말하면 | 이 도구가 |
|---|---|
| 「이 자료로 결과보고서 한글 파일을 만들어 줘」 | `on_write_gov` |
| 「보도자료 양식에는 뭐가 있어?」 | `on_list_templates` |
| 「이 내용을 행사 계획 양식에 채워 줘」 | `on_fill_template` |
| 「아래 연도별 숫자를 공문서 표로 만들어 줘」 | `on_table` |
| 「이 표로 막대그래프 그림을 그려 줘」 | `on_chart` |
| 「추진체계를 체계도로 그려 줘」 | `on_diagram` |

AI 가 어느 도구를 부를지는 AI 가 정합니다. 위는 흔히 불리는 예입니다.

## 손님과 열쇠

|  | 손님(열쇠 없음) | 열쇠 |
|---|---|---|
| 붙이는 법 | 인증 없이 주소만 붙임 | 연결할 때 뜨는 On 문서 로그인 창(OAuth)에 열쇠, 또는 `Authorization: Bearer <열쇠>` 머리말 |
| 이 주소의 도구 | 6개 | 6개 |
| 하루 몫 | 같은 인터넷 주소(IP)에서 하루 100번·1분에 12번(법령 도구 `law_`·`med_` 는 따로 하루 200번·1분에 30번) — On 문서의 모든 주소와 웹 화면을 합쳐 셈(Claude 앱 커넥터로 붙이면 요청이 Anthropic 서버 주소에서 오므로 주소 대신 연결마다 셈). 손님 전체의 하루 몫이 차면 한국 시간 자정까지 닫힘 | 열쇠마다 정해진 하루 몫과 동시에 처리하는 수 |
| 크기 | 요청 하나 6MB(base64 포함) | 파일 하나 25MB |
| 열쇠가 있어야 하는 것 | — | 없음(열쇠에 이 묶음이 들어 있어야 함 — 처음 받는 열쇠에는 없음) |

- 열쇠로 쓸 때는 열쇠에 이 묶음(공문서 쓰기)이 들어 있어야 합니다. 처음 받는 열쇠에는 없으니 신청할 때 함께 적어 주세요. 손님으로는 바로 씁니다.
- 열쇠 신청: `onmunseo.key [at] gmail.com`(제목에 「On 문서 열쇠 신청」). 쓰려는 곳(개인·업무·연구 등)과 필요한 묶음(예: On 공문서 쓰기)을 적어 주세요.
- 틀린 열쇠·끊긴 열쇠는 **401**, 열쇠에 없는 묶음은 **403** 입니다. 짧은 사이에 몰아 부르면 「너무 자주 요청」(429)이 나니 1분쯤 뒤 다시 부릅니다.
- 열쇠를 주소 뒤에 붙이지 마세요. 대화 기록과 접속 기록에 남습니다.

## 안전

1. **남기지 않습니다.** 보낸 문서와 글은 서버 메모리에서만 다루고 처리가 끝나면 버립니다. 서버에 문서 파일을 남기지 않고, 창구 기록에는 열쇠 별칭·도구 이름·보낸 크기·걸린 시간·성공 여부만 남깁니다(문서 내용·파일 이름은 남기지 않음).
2. **AI 없이 규칙으로 만듭니다.** 원고에 없는 사실·숫자는 넣지 않고, 그래프·체계도는 준 숫자·낱말로만 그립니다.
3. **숫자를 잃으면 알립니다.** 표·그래프·체계도(`on_table`·`on_chart`·`on_diagram`)는 원문 숫자를 하나라도 잃으면 결과 대신 까닭을 돌려주고, 공문서 쓰기(`on_write_gov`)는 만든 파일을 다시 읽어 견준 `check` 를 함께 줍니다(`check.same` 이 false 면 잃은 글이 있음 — `check.examples`).
4. **서버를 거치는 이 주소에는 공개 자료와 본인 자료만 보내 주세요.** 기관 내부 문서는 [On 문서 웹 편집기](https://onmunseo.kr/app/)에서 브라우저 안에서 처리하는 기능(한글 열기·고치기·저장, 결재 전 점검, 개인정보 가리기)으로 다루세요.
5. **보안 한도는 풀지 않습니다.** 압축 폭탄 같은 공격을 막는 크기 한도와 배포용 문서 거절 같은 안전 장치는 편의를 위해서도 풀지 않습니다.
6. **결과 파일은 15분.** 만든 파일은 15분 동안만 받을 수 있는 주소로 줍니다.

보안 문제는 [SECURITY.md](SECURITY.md)에 적힌 곳으로 알려 주세요.

## 알아 둘 점

- **무료 시범 서비스입니다.** 기능·하루 몫·주소는 바뀌거나 멈출 수 있습니다. 바뀌면 [CHANGELOG.md](CHANGELOG.md)에 적습니다.
- **결과는 참고용입니다.** 결재 전에 사람이 확인해 주세요.
- 한글 파일은 HWPX 로만 나옵니다(.hwp 는 HWPX 를 한글에서 열어 「다른 이름으로 저장」).
- 인터넷으로만 씁니다. 업무망(폐쇄망)에서는 쓸 수 없습니다.
- 앱마다 메뉴 이름과 판이 달라 화면이 위 설명과 다를 수 있습니다. 안 되면 [SUPPORT.md](SUPPORT.md)를 봐 주세요.

## 이용 조건·개인정보·고지

- 결과를 대량으로 모으거나 다른 AI 모델 학습에 쓰는 것은 금지합니다. 자동화로 남용하면(한도를 넘기려 열쇠 여러 개 쓰기, 쉬지 않고 계속 부르기, 결과 긁어 모으기 등) 미리 알리지 않고 열쇠를 끊습니다. 엔진·규칙·코드를 꺼내 가거나 거꾸로 풀어내는 것은 허락하지 않습니다.
- 요약은 [MCP 안내의 이용 조건](https://github.com/on-munseo/on-munseo.github.io/blob/main/MCP.md#5-이용-조건약관-요약), 전문은 [이용약관](https://onmunseo.kr/terms)·[개인정보 처리방침](https://onmunseo.kr/privacy)에 있습니다.
- 「한글」·「한컴」·「HWP」·「HWPX」는 주식회사 한글과컴퓨터의 상표(등록상표 포함)이며, On 문서는 한글과컴퓨터와 제휴·후원·승인 관계가 없는 독립 서비스입니다.
- Claude·ChatGPT·Cursor·VS Code 등 이름은 각 권리자의 것이며 연결 방법을 알리려고만 씁니다. 고지 전문은 [MCP 안내의 고지](https://github.com/on-munseo/on-munseo.github.io/blob/main/MCP.md#고지)에 있습니다.

## 말 풀이

- **MCP** — AI 도구가 바깥 도구를 부르는 공개 규약(Model Context Protocol). 이 주소를 MCP 서버로 붙이면 AI 가 대화 안에서 이 도구들을 부릅니다.
- **원격 MCP 서버** — 내 컴퓨터에 깔지 않고 인터넷 주소로 붙는 MCP 서버. 설치할 프로그램이 없습니다.
- **묶음 주소** — On 문서의 기능 하나만 담은 주소(`/mcp/text` 등). 전부는 `/mcp` 입니다.
- **열쇠** — On 문서가 주는 사용 권한 값. 하루 몫과 쓸 수 있는 묶음이 정해져 있습니다. 남에게 보이면 안 됩니다.
- **손님** — 열쇠 없이 쓰는 것. 도구 일부와 작은 하루 몫으로 바로 씁니다.
- **OAuth(로그인 창)** — 연결할 때 뜨는 On 문서 로그인 창에 열쇠를 넣는 방식. 앱에는 열쇠 대신 따로 만든 출입증이 갑니다.
- **HWPX** — 한글 문서의 XML 형식(KS X 6101 OWPML). .hwp 는 예전 형식입니다.
- **base64** — 파일을 글자로 바꾼 꼴. JSON 에 파일을 담아 보낼 때 씁니다.
- **개조식** — □ ○ - 기호와 「~함」「~임」 끝맺음으로 한 줄에 한 생각씩 적는 공문서 문체.
- **짜임(structure)** — 장·절·항목을 칸으로 나눠 주는 원고 꼴. 마크다운 대신 쓸 수 있습니다.

## On 문서의 다른 묶음

| 제품 | 저장소 | 주소(앞에 `https://onmunseo.kr`) |
|---|---|---|
| **On 문서(전부)** | [on-munseo.github.io](https://github.com/on-munseo/on-munseo.github.io) — 웹 편집기와 MCP 전부 | `/mcp` |
| On 글꺼내기 | [on-text](https://github.com/on-munseo/on-text) | `/mcp/text` |
| On 결재점검 | [on-check](https://github.com/on-munseo/on-check) | `/mcp/check` |
| On 개인정보 가리기 | [on-mask](https://github.com/on-munseo/on-mask) | `/mcp/mask` |
| On HWPX 만들기 | [on-hwpx](https://github.com/on-munseo/on-hwpx) | `/mcp/hwpx` |
| On 공문서 쓰기 | 이 저장소 | `/mcp/gov` |
| On 글 다듬기 | [on-tidy](https://github.com/on-munseo/on-tidy) | `/mcp/tidy` |
| On 근거 | [on-geungeo](https://github.com/on-munseo/on-geungeo) | `/mcp/law` |
| On폭 글꼴 | [napurrin/onpok-fonts](https://github.com/napurrin/onpok-fonts) — 무료 글꼴(SIL OFL 1.1) · MCP 설치와 상관없음(선택) | — |

## 측정과 비교(참고)

같은 문서·같은 채점으로 직접 잰 값입니다. 공식 순위가 아니며, 잰 판·조건·정의는 [측정 자료](https://github.com/on-munseo/on-munseo.github.io/blob/main/docs/benchmark.md)에 있습니다. 이 묶음만의 값은 위 [성능](#성능)에 있습니다.

| 한컴오피스 한글 2024 로 연 자체 공문서 30과제(같은 과제·같은 채점, 2026-11-19) | On 공문서 쓰기 | 공개 HWPX 보고서 생성 MCP |
|---|---|---|
| 평균 점수(100점) | 99.6 | 86.4 |
| 둘째 줄이 첫 줄 글자 자리에서 시작한 □·○·- 문단 | 100% | 18.5% |
| 쪽 끝에 제목만 남은 곳 | 0 | 4 |
| 내용 보존(원고 요소 그대로) | 100% | 100% |

- 지금 시범판 판은 같은 30과제 모두 100점입니다(2026-11-25). 끝 줄이 짧게 남은 문단도 우리가 적습니다(47 대 57, 2026-11-26 — 글은 그대로 두고 빈칸·자간·장평으로 줄임).
- 같은 원고 5편을 MCP 없이 AI 코딩 도구가 스스로 코드를 짜서 만든 HWPX 는 평균 57.1점이었고(3편은 한컴에서 본문 글이 0자, 한 번에 만든 그대로), On 공문서 쓰기로는 100점입니다(2026-11-26). 5편은 작은 표본입니다.

## 라이선스

글은 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.ko), 설정 파일(`server.json`·`.claude-plugin/`·`plugin/`)은 MIT 입니다. 「On 문서」·「On 공문서 쓰기」 이름과 로고는 이 허락에 들어가지 않습니다. 서비스의 엔진·서버 코드는 이 저장소에 없고 공개하지 않습니다. 전문은 [LICENSE](LICENSE)에 있습니다.

---

만든 사람: [napurrin](https://github.com/napurrin) — 코코에게 배우면서 만들고 고칩니다.
