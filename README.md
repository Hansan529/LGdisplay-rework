# LG Display Rework

# **프로젝트 정보**

> 1인 개발  
> 개발 기간: **2023.01.18 ~ 2023.03.29**

## 홈페이지 배포 주소

> 깃허브 페이지 주소 : https://Hansan529.github.io/LGdisplay-rework

## 프로젝트 소개

- 제작 해상도: 1920px x 1080px
- 반응형 웹 (1600px, 1280px, 767px)
- 라이트 / 다크모드 기능
- 서브 페이지 (PRODUCT)

[한산: @Hansan529](https://github.com/Hansan529) / 웹퍼블리셔 및 프론트엔드 스터디

## 프로젝트 목표

1. data 속성을 통해 스타일 변경이 가능하다.
2. jQuery 라이브러리를 통해서 적은 코드로 작업을 가능하게 한다.

## 사용된 언어 및 도구

### Developement

![Html5](https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![Css3](https://img.shields.io/badge/css3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![Javascript](https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=white)
![Jquery](https://img.shields.io/badge/jquery-0769AD?style=for-the-badge&logo=jquery&logoColor=white)

## 화면 구성

| 라이트 모드                                                                                     | 다크 모드                                                                                       |
| ----------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------- |
| ![img](https://github.com/Hansan529/Blog/assets/115819770/58d3ad0c-e57e-4da1-9bbc-cd44d1035f3f) | ![img](https://github.com/Hansan529/Blog/assets/115819770/8284335c-4dc0-4e4d-ae07-98eb51f40c48) |
| 태블릿 레이아웃                                                                                 | 모바일 레이아웃                                                                                 |
| ![img](https://github.com/Hansan529/Blog/assets/115819770/6f3c9490-1dfb-4844-8641-dfcc693d8dbb) | ![img](https://github.com/Hansan529/Blog/assets/115819770/43df4bae-2c84-487c-b2c5-7f930d265c05) |
| 더보기 창                                                                                       |                                                                                                 |

![img](https://github.com/Hansan529/Blog/assets/115819770/59840bd1-c0f4-4cdd-863f-2256284c861e)

<br>

## 디렉토리 구조

```zsh
├── README.md
├── fonts
│   └── font.css
├── images
├── index.html
├── product.html
├── reset.css
├── script
│   ├── common.js
│   └── script.js
└── styles
    ├── css
    │   ├── common.css
    │   ├── product.css
    │   ├── style.css
    │   └── variable.css
    └── scss
        ├── common.scss
        ├── product.scss
        ├── style.scss
        └── variable.scss
```

## 작업하면서 느낀점

작업하면서 잘못 쓰인 코드를 계속해서 작성하여 추후에는 모든 코드를 갈아엎게 되었다.  
처음 기획할 때 부터 기반을 다져놓지 않으면 나중에는 겉잡을 수 없이 일이 커질 수 있을 것 같다.

<br>

- ### data-속성 이용하기

사용자 속성을 통해서 다크모드를 구현하는데 큰 공이 있다. 기존에 CSS 변수로 라이트 모드의 색상을 지정하고, data 속성으로 변수의 값을 변경하여 적용되도록 하였다.

<br>

- ### 미디어쿼리 선언 방식

### 1. 조상에 미디어쿼리를 선언하기

자손들의 값들을 변경하면 DX(개발자 경험)이 더욱 뛰어나다,  
왜냐, 한 눈에 변화되는 코드만을 볼 수 있기 때문에 변화점에 대해 쉽게 알 수 있다.

```scss
body {
  @include respon(1600) {
    font-size: 16px;
    footer {
      gap: 15px;
    }
  }
}
```

해당 코드를 살펴보면, 스크린이 1600px 안에 포함되면  
body의 font-size가 변경되며, footer 의 gap이 15px로 변경 되는 걸 알 수 있다.

하지만 별도의 변화점을 추가하려면 경로를 일일이 추가해야하기 때문에 유지보수에서는 떨어진다.

<br>

### 2. 선언한 코드마다 미디어쿼리를 선언하기

어느 코드에서라도 미디어쿼리를 관리하기 쉽다.  
기존에 선언한 코드에 작성하는 것이기에 별도의 경로를 추가하여 작성 할 필요 없으며, 하나의 코드에 선언되는 미디어쿼리의 수를 확인할 수 있다.

```scss
header {
  .gnb-btn__wrap {
    @include respon(1280) {
      height: 20%;
    }
    @include responOrientaion(767) {
      height: 100%;
    }
  }
}
```

.gnb-btn\_\_wrap 이라는 클래스 요소가 1280px에서는 height 값이 20%, 767px일 경우 100%로 변경되는 것을
한 눈에 보기 쉽다.  
이로 인해서 값을 수정하기 쉬워 유지보수가 편리하다는 장점이 있다. 단, 미디어 쿼리를 여러번 선언하기에 코드가 길어 질 수 있다.

<br>

### 결론

나는 2번의 방식으로 작성하기로 했다. 어떠한 이유로 인해서 코드를 변경해야 하게 된다면 유지보수가 쉬운 방향이  
DX(개발자 경험)이 조금 떨어지더라도 업무적으로는 더욱 좋기에 선택했다.

만약에 1번의 예제에서 footer의 자손 중에 `ul >li >div >a >button` 으로 스타일을 변경하게 된다면 저 코드에 모든 경로를 새롭게 작성해야 한다면

과연 그게 **효율적인가?** 를 생각해보면 된다.
