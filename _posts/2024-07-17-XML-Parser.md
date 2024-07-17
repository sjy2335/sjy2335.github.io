---
title: XML Parser Tokenizer 학습 정리
date: 2024-07-17 00:00:00 +09:00
categories: [Dev, CS]
tags: [TIL]
---

### AST (Abstract Syntax Tree) 추상 구문 트리

- 소스 코드의 추상 구문 구조의 트리입니다.

  - 프로그램 분석 혹은 변환 시스템에서 사용된다.
  - 소스 코드의 괄호 등 세세한 정보는 제외합니다.

- 컴파일러 이론과 관련이 있습니다.

  - 컴파일러의 첫 단계 구문분석은 tokenizer, lexer, parser의 과정을 포함합니다.
  - tokenizer: 토큰 쪼갬
  - lexer: 쪼갠 토큰에 의미 부여
  - parser: 구조적으로 나타냄
  - 각각 위와 같은 역할을 합니다.

- 단계적으로 세개 과정의 결과를 살펴보면
- tokenizer
  ```
  [ "1", "[2,[3]]", "['he', 'is', 'tall']"]
  ```
- lexer
  ````[
  {type: 'number', value:"1" },
  {type: 'array', value: "[2, [3]]"},
  {type: 'array', value: "['he', 'is', 'tall']"},
  ]```
  ````
- parser

  ```{
  type: 'array',
  child: [
  {type: 'number', value:'1', child:[] },
  {type: 'array',
  child: [
  { type: 'number', value: '2', child:[] },
  { type: 'array',
  child:[ {type:'number', value:'3', child:[]}
  ]
  }]
  },
  {type: 'array',
  child:[
  { type: 'string', value: 'he', child:[] },
  { type: 'string', value: 'is', child:[] },
  { type: 'string', value: 'tall', child:[] },
  ]
  }]
  }
  ```

- 최종적으로 출력된 결과가 AST 형태입니다. 이를 토대로 이후에 compiler가 다음 작업을 수행합니다.

- 다시 한번 말하자면 순서대로
  - tokenizer -> lexer -> parser
  - 토큰화 → 토큰의 어휘 분석해 의미 부여 → 문법을 체크하며 구조적으로 나타냄
- 일반적인 토큰 종류는 다음과 같습니다.

  | 토큰이름   | 샘플                      |
  | ---------- | ------------------------- |
  | identifier | HTML, BODY                |
  | separator  | <, >, [, ], ,             |
  | operator   | +, <, =                   |
  | literal    | true, NULL, 3.14, "hello" |
  | comment    | <!코멘트는 무시>          |

- 다양한 활용 예시가 있습니다.
  - tokenizer와 lexer를 한번에 처리하는 방식도 자주 사용됩니다.
  - 상황에 따라 적절한 토큰화를 사용해야 합니다.

### DOM

- Document Object Model (문서 객체 모델)
- 웹페이지의 태그들을 JS가 활용할 수 있는 객체로 만들엊두며, 트리 구조를 띈다.


### 태그를 찾는 정규 표현식 Regex
- `/<[^>]+>|[^<]+/g` - XML 태그나 텍스트 내용을 찾습니다.
    - `<`: 문자 '<'로 시작
    - `[^>]+`: '>'를 제외한 모든 문자가 1회 이상 반복
    - `>`: 문자 '>'로 끝남
    - `|`: 또는
    - `[^<]+`: '<'를 제외한 모든 문자가 1회 이상 반복
    - `/g`: 전역 검색 (모든 일치 항목 찾기)