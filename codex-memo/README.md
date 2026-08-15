# 📝 Memo

> Git으로 공유 가능한 Overleaf-style MEMO extension for VS Code

코드의 특정 부분을 선택해 메모를 달고, 댓글로 토론하고, `git`으로 팀원과 공유하세요.
메모는 **주석 위치 옆에** 정렬되어 표시🎯

---

## ✨ 주요 기능

| 기능 | 설명 |
| --- | --- |
| 💬 **Memo & Reply** | 코드 선택 → 메모 작성, 답글로 스레드 대화 |
| 🖊️ **Highlight** | 메모에 해당하는 코드 하이라이트됨 · 동일 색상 |
| 🔍 **Search** | 메모 본문 · 원본 코드 · 파일 경로 · 작성자 · 답글까지 통합 검색 |
| 🌐 **Search Range** | 현재 파일만 / 전체 파일 검색 전환 |
| 🏷️ **Tag** | 메모·답글 본문의 `#todo` 같은 `#tag` 자동 인식 |
| 🎨 **Color** | 메모별 색상 지정으로 분류 |
| 🧹 **Filter** | `#tag` · `#color` · `#user` 기준으로 필터링 |
| ✅ **Resolve** | 메모 완료 시 체크 버튼으로 정리 |
| 📍 **Align** | 메모 카드가 주석이 달린 코드 줄에 맞춰 정렬 |
| 🔄 **Share** | `git pull` 후 메모 변경 시 sidebar·highlight 자동 새로고침 |

---

## 📦 Install

### Method 1: Build from Source

**Dependency:** VS Code · Node.js · npm

```sh
cd codex-memo
npm install
npm run compile
npx --yes @vscode/vsce package --no-dependencies
code --install-extension codex-memo-0.2.0.vsix --force
```

설치 후 VS Code에서 `Developer: Reload Window` 를 실행 🔁

**Test:** VS Code 확장(Extensions) 탭에서 **`memo`** 를 검색하면 나옴

---

## 🚀 Usage

### 메모 작성
- 📌 에디터에서 텍스트 선택 → `Alt+M` 또는 우클릭 → **`Add Memo`**
- 🏷️ 작성 중 `Comment` · `Replace` · `Delete` 타입 선택
- ⌨️ 메모 입력 후 `Enter` 로 저장 · `Esc` 로 취소

### 메모 관리
- 💬 메모 하단 답글 박스로 댓글 추가
- 🖱️ 메모 카드 클릭 → 해당 코드 위치로 점프
- 📖 에디터 제목 표시줄의 **Open Memos Beside** 또는 명령 팔레트로 README 미리보기처럼 별도 메모 패널 열기
- ⋯ 점 세 개 메뉴로 **Edit · Delete**
- ⋯ 메뉴에서 저장된 메모의 **Comment · Replace · Delete** 타입 변경
- ⋯ 상태 메뉴에서 **Mark Open · Mark In Progress · Mark Resolved** 선택
- ⋯ 메뉴의 **Copy Context** 로 파일 경로, 선택 코드, 메모, 답글을 클립보드에 복사
- 🎨 팔레트 버튼으로 메모 색상 변경
- ✅ 체크 버튼: 루트 메모를 `resolved` 상태로 보존하고 다시 열 수 있음 · 답글은 해당 답글만 삭제
- ⚓ 앵커가 stale이면 현재 에디터에서 코드를 선택한 뒤 **Re-anchor** 로 위치 갱신

### 검색 & 필터
- 🔍 상단 검색창으로 통합 검색
- 🌐 검색창 옆 범위 아이콘으로 현재 파일 ↔ 전체 파일 전환
- 🧹 필터 아이콘으로 `#tag` · `#color` · `#user` 필터링
- ➕ #?? 작성시 자동으로 `#tag` 에 추가됨

### 표시 규칙
- 👀 현재 에디터와 범위가 교차하는 메모를 사이드바에 표시
- 🪜 카드가 겹치면 아래쪽 카드가 밀려나 모두 읽을 수 있게 배치
- ✏️ `Replace`는 밑줄, `Delete`는 취소선으로 원문에 표시

---

## 🤝 Share with Collaborators

메모는 git 저장소 루트에 저장:

```text
.codex-memos/memos.json
```

> `.codex-memos/memos.json`은 협업을 위해 의도적으로 저장소에 커밋하는 파일입니다. 해결된 메모도 `status: "resolved"`로 기록되어 이력이 보존됩니다. 원자적 저장 중 생성되는 임시 파일만 ignore됩니다.

각 메모는 `kind: "comment" | "replace" | "delete"`를 가질 수 있습니다. 기존 `kind`가 없는 메모는 `comment`로 읽습니다. `replace`와 `delete`는 원문을 자동으로 수정하지 않고, 선택된 원문과 메모 본문을 검토 제안으로 공유합니다.

```sh
git add .codex-memos/memos.json codex-memo .gitignore
git commit -m "Add shared memo extension"
git push
```

1. extension 설치
2. `git pull` 후, VS Code re-load (`Developer: Reload Window`)
3. `.codex-memos/memos.json` 이 바뀌면 MEMO sidebar, beside panel, highlight가 **자동으로 새로고침**🔄

---

## 🎚️ setting.json:

```json
{
  "codexMemo.alignment.topOffsetPx": -20,
  "codexMemo.alignment.lineHeightPx": 0,
  "codexMemo.alignment.lineScale": 1,
  "codexMemo.alignment.cardAnchorOffsetPx": 0
}
```

| 설정 | 역할 |
| --- | --- |
| `topOffsetPx` | 모든 카드를 위/아래로 이동 (카드가 너무 아래면 음수) |
| `lineHeightPx` | 줄 높이 직접 지정 (`0`이면 자동 추정) |
| `lineScale` | 세로 간격 배율 (아래쪽 카드가 더 많이 어긋날 때 조정) |
| `cardAnchorOffsetPx` | 기준선 대비 카드 위치 보정 |

* `codexMemo.authorName`은 선택적 표시 이름입니다. 비워 두면 새 메모는 `Anonymous`로 저장되며 git 사용자명이나 OS 사용자명을 자동으로 읽지 않습니다.

---

## 🛠️ Development

```sh
npm install
npm run compile
```

---

## 🐞 Issue

1. ⚠️ 코드 위치와 메모 보드 위치 사이에 오차가 발생하며, `topOffsetPx` 로도 완전히 조정되지 않는 경우가 있습니다.
