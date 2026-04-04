# Contributing Guide

## 브랜치 네이밍

```
<type>/<issue-number>-<short-description>
```

| 타입 | 용도 |
|------|------|
| `feature/` | 새 기능 추가 |
| `fix/` | 버그 수정 |
| `hotfix/` | 프로덕션 긴급 수정 |
| `chore/` | 빌드, 설정, 의존성 등 기타 작업 |
| `docs/` | 문서 작업 |
| `refactor/` | 리팩토링 |
| `test/` | 테스트 추가/수정 |

**예시**
```
feature/12-add-ingress-config
fix/7-nginx-image-tag
docs/3-update-readme
```

---

## 커밋 메시지 (Conventional Commits)

```
<type>: <subject>

[body]

[footer]
```

**타입**

| 타입 | 용도 |
|------|------|
| `feat` | 새 기능 |
| `fix` | 버그 수정 |
| `docs` | 문서 변경 |
| `style` | 코드 포맷 (동작 변경 없음) |
| `refactor` | 리팩토링 |
| `test` | 테스트 추가/수정 |
| `chore` | 빌드, 설정 변경 |
| `revert` | 이전 커밋 되돌리기 |

**규칙**
- subject는 50자 이내, 명령형으로 작성 (과거형 금지)
- subject 끝에 마침표 금지
- body는 변경 이유 설명, 72자마다 줄바꿈

**예시**
```
feat: add nginx deployment manifest

Add rolling update strategy with maxSurge 1 and maxUnavailable 0
to ensure zero-downtime deployments.

Closes #12
```

---

## 이슈

- 작업 시작 전 이슈를 먼저 생성한다
- 제목은 명확하게, 무엇을/왜 해야 하는지 포함
- 이슈 없이 PR 생성 금지 (긴급 hotfix 제외)
- 이슈 완료 시 커밋/PR에 `Closes #<number>` 명시

**라벨 규칙**

| 라벨 | 용도 |
|------|------|
| `bug` | 버그 리포트 |
| `enhancement` | 기능 개선 |
| `documentation` | 문서 관련 |
| `question` | 질문/논의 |
| `good first issue` | 기여 입문용 |
| `wip` | 진행 중 |

---

## Pull Request

### PR 제목
커밋 메시지와 동일한 Conventional Commits 형식 사용
```
feat(ingress): add nginx ingress controller configuration
```

### PR 본문 템플릿
```markdown
## 변경 사항
-

## 관련 이슈
Closes #

## 테스트
- [ ] 로컬 클러스터에서 적용 확인
```

### PR 규칙
- 하나의 PR은 하나의 목적만 가진다
- PR 제목에 `[WIP]` 접두사를 붙이면 Draft PR로 간주
- 머지 전 최소 1명의 리뷰 승인 필요
- `main` 브랜치에 직접 push 금지
- CI가 실패한 상태에서 머지 금지
- 머지 방식: **Squash and Merge** 사용 (커밋 히스토리 단순화)

---

## 기본 워크플로우

```
1. 이슈 생성
2. 브랜치 생성 (feature/<issue-number>-description)
3. 작업 및 커밋
4. PR 생성 (이슈 연결)
5. 리뷰 요청
6. 승인 후 Squash and Merge
7. 브랜치 삭제

```
