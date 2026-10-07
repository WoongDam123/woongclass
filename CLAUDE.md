# LLM Wiki 스키마

이 저장소는 LLM이 관리하는 지식 위키다. 너(LLM)는 위키의 관리자이고, 사용자는 자료 큐레이터이자 질문자다.

## 폴더 규칙

- `raw/`: 원본 자료. **절대 수정·삭제하지 않는다.** 읽기만 한다.
- `wiki/`: 네가 작성하고 관리하는 영역. 모든 페이지는 마크다운이다.
  - `sources/`: 원본 자료 1개당 요약 페이지 1개
  - `concepts/`: 개념·주제
  - `entities/`: 사람·기관·교재 등 고유 대상
  - `analyses/`: 질문에 대한 답변, 비교표, 분석
  - `index.md`: 모든 페이지의 목록과 한 줄 설명
  - `log.md`: 작업 기록 (맨 아래에 추가만 한다)
  - `overview.md`: 위키 전체의 현재 요약

## 페이지 형식

- 파일명은 소문자 kebab-case: `photosynthesis.md`, `newton-laws.md`
- 페이지 간 링크는 `[[파일명]]` 형식 (확장자 없이)
- 모든 페이지 맨 위에 frontmatter:

```yaml
---
title: 페이지 제목
type: source | concept | entity | analysis
sources: [근거가 된 sources 페이지 이름들]
updated: YYYY-MM-DD
---
```

- 주장에는 근거가 된 소스 페이지를 링크한다.
- 소스끼리 내용이 충돌하면 지우지 말고 "## 상충되는 내용" 섹션에 양쪽을 모두 적는다.

## 작업 절차

### Ingest (자료 반영)
1. `raw/`의 새 자료를 읽는다.
2. 핵심 내용을 사용자와 짧게 확인한다.
3. `wiki/sources/`에 요약 페이지를 만든다.
4. 관련 `concepts/`, `entities/` 페이지를 만들거나 갱신한다 (보통 여러 페이지가 바뀐다).
5. `index.md`, `overview.md`를 갱신한다.
6. `log.md`에 기록한다.

### Query (질문 응답)
1. 먼저 `index.md`를 보고 관련 페이지를 찾는다.
2. 해당 페이지들을 읽고 링크를 달아 답한다.
3. 다시 쓸 만한 답이면 `analyses/`에 저장하고 `index.md`, `log.md`를 갱신한다.

### Lint (점검)
- 페이지 간 모순, 오래된 주장, 깨진 `[[링크]]`, 어디서도 링크되지 않은 페이지, 언급만 되고 페이지가 없는 개념을 찾는다.
- 결과와 수정 내용을 `log.md`에 기록한다.

## log.md 형식

```
## [YYYY-MM-DD] ingest | 자료 제목
- 바뀐 페이지: [[a]], [[b]]
```

작업 종류: `ingest`, `query`, `lint`, `setup`
