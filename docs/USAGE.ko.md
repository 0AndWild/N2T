# N2T 자세한 설치 안내

<p align="center">
  <a href="USAGE.md">English</a> | <a href="USAGE.ko.md">한국어</a> | <a href="USAGE.ja.md">日本語</a> | <a href="USAGE.zh-CN.md">简体中文</a>
</p>

[소개와 사용 예시로 돌아가기](../README.ko.md)

## Skills CLI

설치 명령은 N2T를 쓸 프로젝트 폴더에서 실행하세요. 기본적으로 그 프로젝트에 설치됩니다. 여러 프로젝트에서 함께 쓰려면 아래처럼 `--global`을 붙이면 됩니다. 심볼릭 링크를 쓰기 어려운 환경에서는 `--copy`를 추가해 파일을 복사할 수 있습니다.

```sh
npx skills add 0AndWild/N2T --skill n2t --agent codex claude-code --global
```

내 컴퓨터에 있는 스킬이 목록에 잡히는지 확인하려면, N2T 저장소 폴더에서 실행하세요.

```sh
npx skills add . --list
```

`0AndWild/N2T`를 지정하면 GitHub에 올라간 파일을 가져옵니다. 내 컴퓨터에서만 고친 내용은 커밋하고 푸시하기 전까지 이 설치에 반영되지 않습니다.

## 설치한 스킬 관리하기

설치 목록은 `npx skills list`, 업데이트는 `npx skills update n2t`, 삭제는 `npx skills remove n2t`로 진행합니다. 화면에 안내가 나오면 적용할 프로젝트와 도구를 확인하세요.

아래는 Skills CLI를 쓰지 않고 직접 설치하고 싶을 때의 방법입니다.

## 직접 설치하려면

1. Codex CLI 또는 Claude Code를 설치하고 로그인합니다.
2. `skills/n2t` 폴더를 사용하는 에이전트의 Skill 디렉터리에 복사합니다.
3. 작업할 폴더에서 CLI를 실행하고 N2T에 현재 작업을 설명합니다.

N2T는 Markdown 문서로 구성되어 있어 서버를 띄우거나 빌드할 필요가 없고, Python도 필요하지 않습니다. 아래 방법으로 저장소를 받으려면 Git이 있어야 합니다. 가이드를 만들려면 Codex나 Claude Code에 로그인해야 하며, 웹 자료를 조사하려면 검색과 페이지 열기 기능을 사용할 수 있어야 합니다.

## 1. CLI 설치

이미 CLI가 있다면 다음 단계로 넘어가세요. 아래 명령은 각 제공자의 공식 설치 스크립트를 실행합니다.

### Codex CLI

Windows PowerShell:

```powershell
irm https://chatgpt.com/codex/install.ps1 | iex
```

macOS / Linux:

```sh
curl -fsSL https://chatgpt.com/codex/install.sh | sh
```

설치 후 새 터미널에서 확인하고 첫 실행 안내에 따라 로그인합니다.

```sh
codex --version
codex
```

출처: [Codex CLI 설치와 시작](https://learn.chatgpt.com/docs/codex/cli), [공식 설치 스크립트 안내](https://learn.chatgpt.com/docs/config-file/environment-variables).

### Claude Code

Windows PowerShell:

```powershell
irm https://claude.ai/install.ps1 | iex
```

macOS / Linux / WSL:

```sh
curl -fsSL https://claude.ai/install.sh | bash
```

설치 후 새 터미널에서 확인하고 첫 실행 안내에 따라 로그인합니다.

```sh
claude --version
claude
```

운영체제별 요구사항과 로그인 방법은 [Claude Code 공식 설치 문서](https://code.claude.com/docs/en/setup)를 확인하세요.

## 2. N2T 설치

CLI를 종료하고 일반 터미널에서 실행합니다. 이미 저장소를 내려받았다면 해당 폴더로 이동하고 복제는 생략하세요.

```sh
git clone https://github.com/0AndWild/N2T.git
cd N2T
```

`skills/n2t` 전체를 복사해야 합니다. `SKILL.md`만 복사하면 HTML 작성 기준을 불러올 수 없습니다. 저장소를 복제하는 것만으로 Skill이 설치되지는 않습니다.

### 여러 프로젝트에서 쓰기

| 에이전트 | 설치 위치 | 대화 입력창에서 호출 |
| --- | --- | --- |
| Codex | `~/.agents/skills/n2t/` | `$n2t 현재 하려는 작업` |
| Claude Code | `~/.claude/skills/n2t/` | `/n2t 현재 하려는 작업` |

`~`는 사용자 홈 폴더입니다. 둘 다 사용한다면 각 위치에 설치합니다. 설치 위치는 [Codex Skill 문서](https://learn.chatgpt.com/docs/build-skills)와 [Claude Code Skill 문서](https://code.claude.com/docs/en/skills)를 따릅니다.

**Windows PowerShell** — 저장소 루트에서 실행합니다. 사용할 에이전트에 맞춰 `$n2tParent` 한 줄만 선택하세요.

```powershell
# Codex
$n2tParent = Join-Path $HOME '.agents/skills'
# Claude Code는 위 줄 대신 다음 줄을 사용하세요.
# $n2tParent = Join-Path $HOME '.claude/skills'

$n2tDestination = Join-Path $n2tParent 'n2t'
if (Test-Path -LiteralPath $n2tDestination) {
    throw "이미 설치된 N2T가 있습니다: $n2tDestination"
}
New-Item -ItemType Directory -Path $n2tParent -Force | Out-Null
Copy-Item -LiteralPath './skills/n2t' -Destination $n2tDestination -Recurse
Test-Path -LiteralPath (Join-Path $n2tDestination 'SKILL.md')
```

마지막 결과가 `True`이면 Skill 파일이 복사된 것입니다.

**macOS / Linux / WSL (Bash)** — 저장소 루트에서 실행합니다. 사용할 에이전트에 맞춰 `n2t_parent` 한 줄만 선택하세요.

```bash
# Codex
n2t_parent="$HOME/.agents/skills"
# Claude Code는 위 줄 대신 다음 줄을 사용하세요.
# n2t_parent="$HOME/.claude/skills"

if [ -e "$n2t_parent/n2t" ] || [ -L "$n2t_parent/n2t" ]; then
  printf '이미 설치된 N2T가 있습니다: %s\n' "$n2t_parent/n2t"
else
  mkdir -p "$n2t_parent" && cp -R ./skills/n2t "$n2t_parent/n2t"
fi
```

### 특정 프로젝트에만 설치

개인 설치 대신, **사용할 프로젝트 루트** 아래의 다음 위치로 `skills/n2t` 전체를 복사할 수도 있습니다.

| 에이전트 | 프로젝트 안의 최종 파일 위치 |
| --- | --- |
| Codex | `.agents/skills/n2t/SKILL.md` |
| Claude Code | `.claude/skills/n2t/SKILL.md` |

여러 프로젝트에서 쓸지, 한 프로젝트에서만 쓸지 정해 한 곳에 설치하세요. 같은 스킬이 여러 곳에 있으면 목록에 중복으로 나타나거나 예상과 다른 파일을 읽을 수 있습니다. Windows와 WSL은 홈 폴더가 다르니, 실제로 CLI를 실행하는 쪽에 설치해야 합니다.

## 업데이트와 문제 해결

- **업데이트:** 원본 저장소에서 `git pull --ff-only`로 변경을 받은 뒤 설치된 `n2t` 폴더를 새 `skills/n2t` 사본으로 교체하세요. 직접 수정한 설치본은 먼저 보관하세요. 복사 설치이므로 저장소를 업데이트해도 설치본은 자동으로 바뀌지 않습니다.
- **Skill이 보이지 않음:** 설치 경로 바로 아래 `n2t/SKILL.md`가 있는지 확인하고 새 CLI 세션을 시작하세요. `n2t/n2t/SKILL.md`처럼 중첩되지 않아야 합니다. Codex 대화에서 `$n2t`, Claude Code에서 `/n2t`로 호출하세요.
- **검색이 안 됨:** 사용 중인 도구가 웹 검색과 인터넷 접속을 허용하는지 확인하세요. 웹 조사가 불가능하면 N2T는 제공된 자료를 바탕으로 검증되지 않은 초안임을 표시합니다.
- **HTML 작성 기준을 찾지 못함:** `references/html-guide.md`도 함께 복사했는지 확인하세요.
- **`codex`나 `claude`가 실행되지 않음:** 터미널을 다시 열고 공식 설치 문서의 PATH 안내를 확인하세요.
- **제거:** 선택한 설치 위치의 `n2t` 폴더만 제거하면 됩니다. 이미 만든 HTML 가이드는 별도로 남습니다.
