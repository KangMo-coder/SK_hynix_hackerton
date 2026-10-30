# AI Hackathon Playbook

Codex 작업 지침, 상황별 프롬프트, 데이터 분석 절차, 점검표를 모아 둔 개인용 공개 플레이북입니다. 특정 과제의 정답이나 데이터, 코드는 포함하지 않습니다.

> **우선순위:** 대회 운영 규정·과제별 지시 > 제공 환경의 지침 > 이 저장소. 충돌하면 상위 규칙을 따르고, 불명확하면 우회하지 말고 운영 채널(문제 신고)로 확인합니다.

## 구성

| 경로 | 용도 |
|---|---|
| `AGENTS.md` | Codex 작업 규칙. 작업공간 **루트**에 있어야 Codex가 자동으로 읽음 |
| `PROMPTS.md` | 시작 세팅부터 제출까지 단계별 복사용 프롬프트 (시험 중 메인으로 사용) |
| `prompts/` | 데이터 진단·문서 탐색·분석 설계·검증 등 상세 절차. Codex에게 `@playbook/prompts/...`로 지정해 사용 |
| `checklists/` | 데이터 품질, 보안, 제출 전 점검표 |
| `templates/` | 판단 기록, 분석 로그, 근거표, 보고서 틀 (과제가 양식을 지정하지 않을 때만) |

## 시험 환경에서 가져오기

공개 저장소 Git Clone은 대회 안내에서 허용됩니다. Push는 불가합니다.

```bash
git clone --depth 1 https://github.com/KangMo-coder/SK_hynix_hackerton.git ./playbook
git rev-parse --is-inside-work-tree 2>/dev/null || git init
EXC="$(git rev-parse --git-path info/exclude)"; mkdir -p "$(dirname "$EXC")"
grep -qxF 'playbook/' "$EXC" 2>/dev/null || printf '\nplaybook/\n' >> "$EXC"
```

- `playbook/`은 git에서 제외해 작업 기록(git log·diff)에 섞이지 않게 합니다.
- 작업공간 루트에 `AGENTS.md`가 **없으면** `./playbook/AGENTS.md`를 루트로 복사합니다. Codex는 저장소 루트부터 현재 작업 디렉터리까지의 경로에서 지침 파일을 읽습니다. 따라서 작업공간 루트에서 실행할 때 하위 폴더 `playbook/AGENTS.md`는 루트 지침으로 자동 적용되지 않습니다.
- 작업공간에 기존 `AGENTS.md`가 있으면 덮어쓰지 않습니다. `PROMPTS.md` 1-c에 따라 기존 지침을 우선하고 플레이북은 보조 참고로 사용합니다.
- 초기 세팅에서 `git add -A`로 작업공간 전체를 commit하지 않습니다. 검증된 기능마다 필요한 파일만 명시적으로 stage하고 diff를 확인한 뒤 로컬 commit합니다. Git Push는 하지 않습니다.
- 이후 순서는 `PROMPTS.md`를 따릅니다.

## 기본 흐름

1. 과제 파악 → 업무 담당자(메신저)에게 요구사항 확인
2. 답변을 반영해 `PLAN.md` 작성
3. end-to-end MVP → 기능 단위 추가, 기능마다 검증 후 관련 코드·문서만 로컬 commit (원본 데이터·대외비 파일은 stage/commit하지 않음)
4. 판단은 `DECISIONS.md`에 기록
5. 리뷰 → README → 이해도 점검 → 제출
6. 후속 서술형은 AI 없이 직접 작성

## 사용 원칙

- 이 저장소에는 범용 방법론과 프롬프트만 둡니다. 시험 문제, 제공 파일, 데이터, 결과물은 추가하지 않습니다.
- 템플릿과 절차는 필요한 부분만 이해해 활용하며, 결과물을 통째로 대체하지 않습니다.
- AI가 제안한 분석·코드·설명은 검증 전까지 가설로 취급합니다.
- 이 저장소는 2차 예선 결과 통지 전까지 공개 상태로 유지하고, 시험 이후 수정하지 않습니다.
