# 2월 3주차 회고

## 과제

### 1. 어떻게 마크업할까?

[Atomic Design](https://atomicdesign.bradfrost.com/chapter-2/)의 단계를 차용하여, 다음의 형태로 설계하였다.

1. 원소 atom : 'group' 요소, 'indicator' 요소
2. 분자 molecules : 'avatar' 요소
3. 유기체 organisms : 'layout' 요소
4. 템플릿 Templates : 'Avatars' 레이어


### 2-1. 원소 atoms 단계 - group

- #hash : da29b94

가장 먼저, 원소에 해당하는 요소인 'group'과 'indicator'를 완성시킨다.

'group' 에는 71.11px * 71.11px 의 프로필 이미지와, 64px * 64xp 의 마스킹된 영역이 포함된다. 이에, 나는 다음과 같이 코드를 작성했다.

```html
<picture class="avatar__img">
    <img src="images/face1.jpg" alt="여성 얼굴 - 1" width="71.111px" height="71.111px" loading="lazy" />
  </picture>
```

```css
.avatar__img {
  width: 64px; height: 64px;

  display: flex;
  justify-content: center;
  align-items: center;
  
  /* dev 모드를 확인해보니, mask 영역에 1px 의 border 가 있는 것을 확인했다. */
  /* 하지만 이게 의미가 있는 건지는 모르겠다. */
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 50%;
}
```

- #hash : 15c1263

하지만, border-radius 값이 적용이 되지 않았다. 왜 그럴까? containter 영역보다 img 영역이 더 큰데, 부모 요소의 영역을 넘어가는 것을 숨기는 속성이 있을 수 있겠다 생각했다. mdn 에서 [overflow](https://developer.mozilla.org/ko/docs/Web/CSS/overflow) 라는 유용해보이는 속성이 있었고, 바로 적용해보았다. 그 결과, 내가 원하는 대로 border-radius 가 정상적으로 처리가 되었다. clip 값을 사용하면 어떠한 스크롤도 불가능하다는 점에서, overflow: clip 속성을 선택했다.

💡 알게된 점

normal flow 에서 부모 요소의 영역이 자식 요소의 영억보다 클 경우, overflow: hidden 또는 overflow: clip 을 사용하여 숨김 수 있다. 

```css
.avatar__img {
  width: 64px; height: 64px;

  display: flex;
  justify-content: center;
  align-items: center;
  
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 50%;
  overflow:hidden;
}
```


### 2-2. 원소 atoms 단계 - indicator

- #hash : ebd9541

우선, indicator 항목이 사용자와 상호작용하는 요소일까, 아니면 디자인적으로 꾸며주는 용도일까를 우선적으로 생각했다. 하지만 이미지를 바탕으로 어떠한 정해진 패턴이 있다고 판단이 되지 않았고, 데이터로 확인할 수 있는 구분되는 속성이 있을 것이라고 판단했다.

처음에는 가상 요소 선택자를 사용하여 상호작용할 수 없는 디자인 요소로 적용해야 겠다고 생각했다. 그러다, '사용자가 해당 프로필에 대한 선호도를 나타내는 상호작용 요소일 수 있겠다'는 생각에, 해당 요소를 input 요소의 checkbox 속성을 사용해보기로 했다.

하지만, input 의 checkbox 요소가 picture 가 아닌 img 의 위치에서 absolute 를 가지면 된다고 판단했고, 이를 위해 html 코드의 수정이 불가피했다. 따라서, picture 은 추후 img 소스를 source 속성을 사용하여 관리하기 위한 용도로만 남겨두고, picture 를 form 요소로 감싼 뒤 picture 클래스를 이전하여 사용하기로 했다. 그 결과, 내가 원하는 대로 input 의 checkbox 요소가 avatar__img 에 할당한 64*64 사이즈를 기준으로 absolute 가 적용되었다.

checkbox 를 CSS 로 형태를 변경시키는 방법을 개인적으로 적용해보았으나, 방법을 찾기 쉽지 않았다. 이에, 포털사이트 검색을 통해 [appearance 속성과 가상 클래스 선택자인 :hover 를 사용한 외부 소스](https://gurtn.tistory.com/106)를 찾게 되었고, 정상 적용된 것을 볼 수 있었다.

```html
<form class="avatar__img">
    <picture class="avatar__img clip">
      <img src="images/face1.jpg" alt="여성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
    </picture>
    <div>
      <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
      <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-01" />
    </div>
</form>
```

```css
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  white-space: nowrap;
  border: 0;
}

.avatar__img {
  width: 64px;
  height: 64px;

  display: flex;
  justify-content: center;
  align-items: center;

  border-radius: 50px;

  position: relative;
}

.avatar__img.clip {
  border: 1px solid #fff;
  overflow: clip;
}

.avatar__check {
  margin: 0;
  
  position: absolute;
  right: 0;
  bottom: 0;

  /* input 요소의 checkbox 속성을 둥글게 만드는 외부 소스 인용 */
  width: 17.18px;
  height: 17.18px;
  border-radius: 50%;
  border: 1px solid #fff;
  background-color: #dbdbdb;
  appearance: none;

  &:checked {
    border: 1px solid #fff;
    background: #4CFE88;
  }
}
```

### 3. 분자 molecules 단계 - avatar

- #hash : 6aec9a8

원소 단계인 group(picture.avatar__img clip) 과 indicator(div)가 완성되었다. 두 요소를 하나의 그룹으로 묶어 분자 단계 요소를 만든다.

사용자의 프로필 선호도에 따른 checkbox 항목을 만드는 것으로 설계했기 때문에, 8개의 요소는 form 태그로 묶여서 사용하는 것이 좋겠다고 판단했다. 이에, 기존에 사용했던 form 태그를 div 로 변경, 동일한 형태의 8개의 div 를 만들고 하나의 form 태그로 묶어 사용했다.

각각의 항목에 대해 img 의 src 를 수정하였고, 성별에 따라 alt 속성을 수정하였다. `input[type="checkbox]` 요소에 name="avatar__check" 속성을 공통적으로 넣어 하나의 체크박스 형태로 묶었고, value 값을 checked-01 ~ checked-08 로 수정하였다.

```html
  <form>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face1.jpg" alt="여성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-01" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face2.jpg" alt="여성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-02" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face3.jpg" alt="여성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-03" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face4.jpg" alt="여성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-04" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face5.jpg" alt="남성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-05" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face6.jpg" alt="남성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-06" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face7.jpg" alt="남성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-07" />
      </div>
    </div>
    <div class="avatar__img">
      <picture class="avatar__img clip">
        <img src="images/face8.jpg" alt="남성 얼굴" width="71.111px" height="71.111px" loading="lazy" />
      </picture>
      <div>
        <label for="avatar__check" class="sr-only">마음에 드는 프로필을 선택해 주세요</span></label>
        <input class="avatar__check" id="avatar__check" name="avatar__check" type="checkbox" value="checked-08" />
      </div>
    </div>
  </form>
```

### 4. 조직체 organism 단계 - layout

- #hash : 

8개의 분자를 감싼 form 요소의 display 속성을 변경하여, 블록 형태에서 flex 형태로 변경하였다. flex 의 여러 속성을 사용하여 위치를 조정하였다.

width 와 padding 값을 넣었을 때, 콘텐츠 박스 영역이 적용했던 width 값보다 작아지는 것을 보고, box-sizing: border-box 로 수정 적용하였다.

![결과물](/src/avatars/images/organism:layout:01.png)

### 5. 템플릿 template 단계 - Avatar 레이어

- #hash : 5e2cd8c

최종 완성된 조직체 단계의 layout 을 정렬하기 위해 main 요소로 감쌌다. 그 다음, body 와 main 의 width, height 를 각각 100vw, 100vh 로 설정하여 화면 전체에 꽉 차도록 변경했다. main 의 display 를 flex 로 변경하고, justify-content 와 align-items 를 사용하여 가운데, 중앙 정렬하여 마무리한다.

![결과물](/src/avatars/images/template:Avatar:01.png)

- #hash : 

Notion 에서 언급된 상자 내부 여백 100px 을 수정 적용하였다. 이때, 기존에 설정했던 box-sizing 이 border-box 을 삭제하여 콘텐츠 영역의 그리드를 보존하였다.

![결과물](/src/avatars/images/template:Avatar:02.png)

### 6. 과제를 하면서 알게 된 점

첫째, 디자이너와 소통하지 않으면, 해당 인터페이스를 보았을 때 어떤 기능을 위해 만들었는 지 알 수 없을 것 같다.

figma draft 만으로 어떤 목적으로 만들었는지 이해할 수 없었다. 디자이너는 개발자를 위한 코멘트 또는 디자인 의도를 별도로 기재해줄 필요가 있고, 개발자는 이해가 안되는 부분이 있으면 바로바로 이야기를 해줘야 할 것 같다.

둘째, 개발자마다 코드를 작성하는 것이 모두 다를 수 밖에 없을 것 같다. 나는 상호작용을 목적으로 하는 페이지라고 생각하여 form 과 input 요소를 중점적으로 코드를 작성했다. 만약, 사용자가 팔로우하고 있는 사람을 보여주는 결과물 중심의 페이지라면, 내가 만든 상호작용 코드가 아니라 정적인 페이지가 구성되어야 할 것이다.

class 명을 지정하는 것부터 어려움을 겪었다. 나는 [BEM 방식](https://bem-cheat-sheet.9elements.com/)을 차용하여 class 명을 사용하였고, 학습했던 내용 중 css 중첩을 활용하여 파일을 작성하였다.

결국, 협업을 위해서는 공통의 규칙과 소통이 필수적일 것이라고 생각했다.

<br />

## 학습

이번 주에는 확실히 1-2주차에 비해 난이도가 높았다. 특히, HTML 마크업 요소들에 대해 심도 있는 학습을 할 수 있어서 의미있었다.

**마크업**에서 왜 이 코드를 사용했고, 이 코드를 나중에 누군가 유지보수를 위해 바라보았을 때, 조금더 시맨틱한 관점에서 필요한 코드를 적절하게 사용할 수 있어야 하겠다고 생각했다. 웹 브라우저의 '기본'적인 코드이지만, '기본'이 되지 않은 코드는 발전할 수 없다고 생각된다.

웹 접근성에 대해 조금 더 생각해보기로 했다. 개발자 도구에서 스크린 리더로 어떻게 읽히는지, 왜 alt 속성과 sr-only, aria-label 등을 고려해야 하는지 더 이해할 필요가 있겠다.

**CSS 코드**는 다행이도 이전에 예습했던 내용 덕분에 이해가 어렵지 않았다. 하지만, position 속성은 이전에 정확하게 이해하지 못했던 내용인데, 이번에 학습하고 직접 실습해보면서 이제는 완벽(?)하게 이해할 수 있게 되었다.

CSS 코드의 중첩 구조에 대해 처음 알게 되었다. 처음 알게된 SASS 도 꽤나 매력적으로 느껴졌다. CSS 과정 이후에 SASS 도 조금 더 학습할 필요가 있겠다.

**회고 시간**은 정말 유용했다. 이전 주까지 회고 시간에 개인 회고만 진행했는데, 이번에는 리더를 필두로 다양한 의견을 주고 받았고, 회고 방식을 지정할 때 여러 방식의 토론을 통해 합의된 방식을 결정하고, 진행해봤다. 여전히 시간은 부족했지만, 경험의 공유적인 면에서 굉장히 긍정적이었다.