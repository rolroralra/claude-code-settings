---
allowed-tools: Bash(gh)
description: GitHub 레포지토리에 표준 레이블 세트를 자동으로 생성합니다.
---

# GitHub 레이블 초기 세팅

이 커맨드는 새로운 GitHub 레포지토리에 표준화된 레이블 세트를 자동으로 생성합니다. 개발 영역, 난이도, 작업 유형별로 분류된 레이블을 일관되게 적용하여 프로젝트 관리를 효율화합니다.

---

## Prompt Instruction

현재 GitHub 레포지토리에 표준 레이블 세트를 생성해줘. 다음 스크립트를 실행해서 레이블을 자동으로 추가해줘:
```bash
#!/bin/bash

set -e  # 에러 발생 시 중단

# GitHub CLI 설치 확인
if ! command -v gh &> /dev/null; then
    echo "❌ GitHub CLI(gh)가 설치되어 있지 않습니다."
    echo "설치: https://cli.github.com/"
    exit 1
fi

# Git 레포지토리 확인
if ! git rev-parse --git-dir > /dev/null 2>&1; then
    echo "❌ 현재 디렉토리가 git 레포지토리가 아닙니다."
    exit 1
fi

# GitHub 인증 확인
if ! gh auth status &> /dev/null; then
    echo "❌ GitHub CLI가 인증되지 않았습니다."
    echo "인증: gh auth login"
    exit 1
fi

echo "🏷️  GitHub 레이블 생성 중..."

labels=(
  "area: frontend|프론트엔드 개발 영역|0366d6"
  "area: backend|백엔드 개발 영역|1d76db"
  "easy|쉬운 난이도|0e8a16"
  "medium|중간 난이도|fbca04"
  "hard|어려운 난이도|d73a4a"
  "type: feature|새로운 기능|a2eeef"
  "type: fix|버그 수정|d73a4a"
  "type: docs|문서 작업|0075ca"
  "type: test|테스트 관련|fef2c0"
  "type: refactor|리팩토링|fbca04"
  "type: style|코드 스타일 변경|f9d0c4"
)

success_count=0
fail_count=0

for label in "${labels[@]}"; do
  IFS='|' read -r name description color <<< "$label"
  if gh label create "$name" --description "$description" --color "$color" --force 2>/dev/null; then
    echo "  ✓ $name"
    ((success_count++))
  else
    echo "  ✗ $name (실패)"
    ((fail_count++))
  fi
done

echo ""
echo "✅ 레이블 생성 완료! (성공: $success_count, 실패: $fail_count)"
```

실행 전 GitHub CLI가 인증되어 있는지 확인하고, 현재 디렉토리가 git 레포지토리인지 체크해줘.
