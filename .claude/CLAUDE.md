# GitHub 프로젝트 초기 세팅

## 새 레포지토리 생성 시 자동 실행

레포지토리 생성 직후 또는 "초기 세팅" 요청 시 다음 레이블들을 자동으로 생성:
```bash
gh label create "area: frontend" --description "프론트엔드 개발 영역" --color "0366d6" --force && \
gh label create "area: backend" --description "백엔드 개발 영역" --color "1d76db" --force && \
gh label create "easy" --description "쉬운 난이도" --color "0e8a16" --force && \
gh label create "medium" --description "중간 난이도" --color "fbca04" --force && \
gh label create "hard" --description "어려운 난이도" --color "d73a4a" --force && \
gh label create "type: feature" --description "새로운 기능" --color "a2eeef" --force && \
gh label create "type: fix" --description "버그 수정" --color "d73a4a" --force && \
gh label create "type: docs" --description "문서 작업" --color "0075ca" --force && \
gh label create "type: test" --description "테스트 관련" --color "fef2c0" --force && \
gh label create "type: refactor" --description "리팩토링" --color "fbca04" --force && \
gh label create "type: style" --description "코드 스타일 변경" --color "f9d0c4" --force
```

## 레이블 정책
- **개발영역**: area: frontend, area: backend
- **난이도**: easy, medium, hard
- **작업유형**: type: feature, fix, docs, test, refactor, style

## 자동 실행 트리거
- 새 git 레포지토리 감지
- "초기 세팅", "setup", "레이블 생성" 키워드
```

### 2. 글로벌 설정 - Claude.ai 메모리

Claude Code는 별도의 글로벌 설정 파일이 없으므로, **Claude.ai에서 메모리로 저장**하는 것이 맞습니다.

Claude.ai 대화창에서:
```
"내가 GitHub 프로젝트를 시작할 때마다 다음을 기억해줘:

1. 프로젝트 루트에 CLAUDE.md 파일이 있으면 그 규칙을 따름
2. 새 레포지토리 생성 시 표준 레이블 세트 자동 생성:
    - area: frontend (#0366d6), backend (#1d76db)
    - easy (#0e8a16), medium (#fbca04), hard (#d73a4a)
    - type: feature (#a2eeef), fix (#d73a4a), docs (#0075ca),
      test (#fef2c0), refactor (#fbca04), style (#f9d0c4)
3. gh CLI 명령어 사용, --force 옵션으로 덮어쓰기
4. 백엔드 개발자라 emoji는 자제"
```

## 실제 동작 방식
```
프로젝트/CLAUDE.md
↓
Claude Code가 자동 인식
↓
컨텍스트로 활용하여 작업 수행
