---
title: 반응형 웹 디자인
date: 2024-08-22 00:00:00 +09:00
categories: [CSS]
tags: [TIL, RWD, Responsive Web Design]
---

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [반응형 웹 디자인](#반응형-웹-디자인)
  - [미디어 쿼리 Media Queries](#미디어-쿼리-media-queries)
  - [반응형 레이아웃 기술](#반응형-레이아웃-기술)

<!-- /code_chunk_output -->

## 반응형 웹 디자인

반응형 웹 디자인(RWD)는 웹 페이지가 모든 다양한 화면 크기와 해상도에서 잘 렌더링 되도록 하면서도 사용성을 보장하는 웹 디자인 접근 방식입니다. 기본적으로 HTML은 반응형 혹은 유동적 (responsive, or fluid)이므로 CSS 없는 HTML만으로 브라우저는 텍스트를 뷰포트에 맞게 줄바꿈을 더하는 등 리플로우 해주기는 합니다. 그러나, 과도하게 변형되는 컴포넌트로 인해 생기는 가독성 문제와 사용자 편의를 위해 아래와 같은 방법들로 반응형 웹 디자인을 도입하는 것이 적절합니다.

### 미디어 쿼리 Media Queries

미디어 쿼리를 사용하면 장치 유형, 화면 해상도나 방향, 종횡비, 브라우저 뷰포트 너비/높이, 데이터 사용량, 투명도 등의 사용자 선호 특성에 따라 CSS를 적용할 수 있습니다.

- `@media`와 `@import` at-rules를 통해 사용할 수 있습니다.
- `media` 속성으로 특정 HTML 요소의 매체를 가리킬 수 있습니다.
- Window.matchMedia()나 MediaQueryList.addListener()의 메소드로 미디어 상태를 관찰하고 판별할 때도 같은 방식으로 사용할 수 있습니다.

미디어 쿼리는 아래의 미디어 유형/특성에 대한 논리 연산자를 이용한 표현식으로 작성됩니다.

- 미디어 유형: 미디어 쿼리가 적용되는 장치의 범주를 정의합니다.
  - all
  - print
  - screen
  - (기본적으로 all로 설정되어 only 연산자를 사용할 때를 제외하고는 선택적optional입니다.)
- 미디어 특성: 브라우저를 포함한 user agent, 출력 장치, 환경 등의 특징을 나타냅니다.
  - any-hover
  - any-pointer
  - aspect-ratio
  - color
  - display-mode
  - grid
  - height/width
  - hover
  - overflow-block
  - overflow-inline
  - pointer
  - resolution
  - scripting
  - update
  - video-dynamic-range
  - [자세한 사항은 여기에서 확인할 수 있습니다.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
- 논리 연산자: 복잡한 미디어 쿼리를 구성할 수 있게 합니다.
  - not, and, only
  - 또한, 여러 미디어 쿼리를 쉼표로 구분해 하나의 규칙으로 결합할 수 있습니다.

### 반응형 레이아웃 기술

유연한 그리드flexible grids를 사용함으로서 반응형 웹 사이트는 모든 디바이스 사이즈에 맞출 필요가 없어졌습니다.
