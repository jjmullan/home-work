# 마크다운 문법

> Authored by [**Youngjune-Choi**](https://github.com/jjmullan/home-work) (_2025. 2. 14_)<br />
> Sourced by **[CommonMark](https://spec.commonmark.org/0.31.2/)** (_version: 0.31.2_) & **[GFM](https://github.github.com/gfm/#what-is-github-flavored-markdown-)** (_version: 0.29-gfm_)

- [제목](#제목)
- [볼드](#볼드)
- [이탤릭](#이탤릭)
- [GFM 취소선](#gfm-취소선)
- [인용문](#인용문)
- [리스트(1)](#리스트1)
- [리스트(-)](#리스트-)
- [하이퍼링크](#하이퍼링크)
- [GFM 오토링크](#gfm-오토링크)
- [이미지](#이미지)
- [테이블](#테이블)
- [GFM 테이블](#gfm-테이블)
- [인라인 코드](#인라인-코드)
- [블록 코드](#블록-코드)
- [GFM 체크박스](#gfm-체크박스)
- [GFM 태그 필터](#gfm-태그-필터)
- [GFM 하이라이트 박스](#gfm-하이라이트-박스)

<br />

## 제목

# `#`를 사용하면 h1 태그를 사용할 수 있습니다.

## `##`를 사용하면 h2 태그를 사용할 수 있습니다.

### `###`를 사용하면 h3 태그를 사용할 수 있습니다.

#### `####`를 사용하면 h4 태그를 사용할 수 있습니다.

##### `#####`를 사용하면 h5 태그를 사용할 수 있습니다.

###### `######`를 사용하면 h6 태그를 사용할 수 있습니다.

&#9888; warning. <br />- #와 텍스트 사이에 띄어쓰기( )가 포함되어야 한다.<br />- #가 7개 이상인 경우, p 태그로 인식된다.<br />- 반드시 #로 문장이 시작해야 한다.

<br />

## 볼드

`**` 태그를 앞뒤로 붙이면 **강조** 할 수 있습니다.

<br />

## 이탤릭

`*` 태그를 앞뒤로 붙이면 _이탤릭체_ 를 사용할 수 있습니다.

<br />

## GFM 취소선

`~~` 를 앞뒤로 붙이면 ~~취소선~~을 사용할 수 있습니다.

<br />

## 인용문

> `>`를 사용하여 인용문을 만들 수 있습니다.

<br />

## 리스트(1)

1. `숫자.`를 앞에 붙여 ordered list를 만들 수 있습니다.

<br />

## 리스트(-)

- `-`를 앞에 붙여 unordered list를 만들 수 있습니다.

* `*`를 앞에 붙여 unordered list를 만들 수 있습니다.

<br />

## 하이퍼링크

`[대체텍스트](URL)` 형태로 작성하면 [하이퍼링크](https://bootcamp.likelion.net/)를 만들 수 있습니다.

<br />

## GFM 오토링크

www 로 시작하는 URL 을 입력하면 자동으로 링크 https://bootcamp.likelion.net/ 를 만들 수 있습니다.

<br />

## 이미지

`![이미지설명](URL)` 형태로 작성하면<br />
![멋쟁이사자처럼 로고](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS2QuItPJLx65Rb2kqBsMRU7t3BmKc8jn98lw&s)<br />
를 만들 수 있습니다.

<br />

## 테이블

- CommonMark 에는 테이블 문법이 없습니다.
- CommonMark 에서 표를 만들기 위해서는, HTML 의 `<table>` 코드를 직접 사용해야 합니다.

<br />

## GFM 테이블

- `|`를 사용하여 열을 생성할 수 있습니다.
- 생성한 열 수에 맞게 `|--|`를 작성하면 테이블 형태로 작성할 수 있습니다.
- `|--|`안에 `:`를 넣어 좌/우/중앙 정렬을 할 수 있습니다.
  - `|:--|` : 좌측 정렬
  - `|--:|` : 우측 정렬
  - `|:--:|` : 중앙 정렬

| 강의명                              |  강의정보  |  강사명  |
| ----------------------------------- | :--------: | :------: |
| 멋쟁이사자처럼 프론트엔드 스쿨 13기 |  HTML/CSS  | 김데레사 |
| 멋쟁이사자처럼 프론트엔드 스쿨 13기 | JavaScript |  정길용  |

<br />

## 인라인 코드

` `` `를 넣어 인라인 코드 형태로 포매팅이 가능합니다.

<br />

## 블록 코드

```
블록 코드 형태로 포매팅이 가능합니다.
```

<br />
이때, 시작하는 지점(```)에 해당 코드 블록이 어떤 Language 를 사용하는지 표현할 수 있습니다.

```html
<!DOCTYPE html>
```

e.g. [JavaScript, C-like, Other(python, ...), Styling(css, ...), Markup(HTML, XML, ...), Command Prompt(bash, powershell, ...), Configure/Data Files(json, ignore, ...), etc.](https://developer.mozilla.org/en-US/docs/MDN/Writing_guidelines/Howto/Markdown_in_MDN)

<br />

## GFM 체크박스

- HTML 태그의 `<input type="checkbox" />`를 대체할 수 있습니다.

<!-- Github 에서 작동 -->

- [ ] 오늘 할일 1
  - [x] 중요한 할일 1
  - [ ] 중요한 할일 2
- [x] 오늘 할일 2

<br />

## GFM 태그 필터

- Github 에서 Md 파일을 작성할 때 위험한 태그를 필터링하고, 안전한 태그만 렌더링하여 표시할 수 있다.
- 필터링 태그: `<script>`, `<style>`, `<ifframe>`, `<object>`, `<embed>` 등

<br />

## GFM 하이라이트 박스

- 첫 줄에 [!NOTE], [!WARNING], [!CALLOUT] 을 선언하여, 해당 blockquote 를 하이라이트 박스로 만들 수 있습니다.
- GFM 을 지원하는 Github 에서만 제대로 표시될 수 있습니다.

[!NOTE]
이것은 중요한 참고 사항입니다. 이 정보를 잘 기억해 두세요!

[!WARNING]
이 작업을 실행하기 전에 중요한 주의사항을 확인해야 합니다!

[!CALLOUT]
이 부분은 특별히 강조가 필요한 부분입니다. 중요합니다!

<style>  
  li:nth-child(4), li:nth-child(9), li:nth-child(12), li:nth-child(15), li:nth-child(16), li:nth-child(17) {
    color: orange;
    list-style: square;
  }
</style>
