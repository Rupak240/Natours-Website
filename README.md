# Natours Project
## Tools and Languages used 

<img align="left" alt="Visual Studio Code" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/visual-studio-code/visual-studio-code.png" />

<img align="left" alt="HTML" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/html/html.png" />

<img align="left" alt="CSS" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/css/css.png" />

<img align="left" alt="Sass" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/sass/sass.png" />

<img align="left" alt="NPM" width="26px" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/npm/npm.png" />

<br />
---
---

### SASS FileCode :

#### 1. abstracts
#### a. _mixins_.scss
```Css
@mixin clearfix {
  &::after {
    content: "";
    display: table;
    clear: both;
  }
}

@mixin absCenter {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

// MEDIA QUERY MANAGER
/*
0 - 600px Phone
600 - 900             Tablet portrait
900 - 1200            Tablet landscape
1200 - 1800           where normal style appiles
1800 +                Big desktop

$breakpoint arguement choices
-- phone
-- tab-port
-- tab-land
-- big-desktop

ORDER: base + typography + general layout + grid > page layout > components
*/

@mixin respond($breakpoint) {
  @if $breakpoint == phone {
    @media only screen and (max-width: 37.5em) {
      // 600px
      @content;
    }
  }

  @if $breakpoint == tab-port {
    @media only screen and (max-width: 56.25em) {
      // 900px
      @content;
    }
  }

  @if $breakpoint == tab-land {
    @media only screen and (max-width: 75em) {
      // 1200px
      @content;
    }
  }

  @if $breakpoint == big-desktop {
    @media only screen and (min-width: 112.5em) {
      // 1800px
      @content;
    }
  }
}
```
#### b. _variables.scss
```Css
// COLORS
$color-primary: #55c57a;
$color-primary-light: #7ed56f;
$color-primary-dark: #28b485;

$color-secondary-light: #ffb900;
$color-secondary-dark: #ff7730;

$color-tertiary-light: #2998ff;
$color-tertiary-dark: #5643fa;

$color-grey-light-1: #f7f7f7;
$color-grey-light-2: #eee;

$color-grey-dark: #777;
$color-grey-dark-2: #999;
$color-grey-dark-3: #333;

$color-white: #fff;
$color-black: #000;

// FONT
$default-font-size: 1.6rem;

// GRID
$grid-width: 114rem;
$gutter-vertical: 8rem;
$gutter-vertical-small: 6rem;
$gutter-horizontal: 6rem;
```

#### 2. base
#### a. _animation.scss
```css

@keyframes moveInLeft {
    0% {
      opacity: 0;
      transform: translateX(-10rem);
    }
  
    80% {
      transform: translateX(1rem);
    }
  
    100% {
      opacity: 1;
      transform: translate(0);
    }
  }
  
  @keyframes moveInRight {
    0% {
      opacity: 0;
      transform: translateX(10rem);
    }
  
    80% {
      transform: translateX(-1rem);
    }
  
    100% {
      opacity: 1;
      transform: translate(0);
    }
  }
  
  @keyframes moveInBottom {
    0% {
      opacity: 0;
      transform: translateY(10rem);
    }
  
    100% {
      opacity: 1;
      transform: translate(0);
    }
  }
```
#### b. _base.scss
```css
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

html {
  font-size: 62.5%; // 1rem = 10px

  // @include respond-phone {
  //   font-size: 50%;
  // }

  @include respond(big-desktop) {
    font-size: 75%; // 1rem = 12px, 12/16 = 75%
  }

  @include respond(tab-land) {
    font-size: 56.25%; // 1rem = 9px, 9/16 = 56.25%
  }

  @include respond(tab-port) {
    font-size: 50%; // 1rem = 8px, 8/16 = 50%
  }

  @include respond(phone) {
    font-size: 40%; // 1rem = 8px, 8/16 = 50%
  }

  
}

body {
  box-sizing: border-box;
  padding: 2rem;

  @include respond(tab-land) {
    padding: 0;
  }
}


::selection {
  background-color: $color-primary;
  color: $color-white;
}
```
#### c. _typography.scss
```css
body {
  font-family: "Lato", sans-serif;
  font-weight: 400;
  /* font-size: 1rem; */
  line-height: 1.7;
  color: $color-grey-dark;
}

.heading-primary {
  color: $color-white;
  text-transform: uppercase;

  backface-visibility: hidden;
  margin-bottom: 6rem;

  &--main {
    display: block;
    font-size: 6rem;
    font-weight: 400;
    letter-spacing: 3.5rem;

    animation-name: moveInLeft;
    animation-duration: 1s;
    animation-timing-function: ease-out;

    @include respond(phone) {
      letter-spacing: 2rem;
      font-size: 5.5rem;
    }

    /* animation-iteration-count: 3; */
    /* animation-delay: 3s; */
  }

  &--sub {
    display: block;
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: 1.75rem;

    animation: moveInRight 1s ease-out;

    @include respond(phone) {
      letter-spacing: 0.5rem;
    }

    /* animation-name: moveInRight;
        animation-duration: 1s;
        animation-timing-function: ease-out; */
  }
}

.heading-secondary {
  font-size: 3.5rem;
  text-transform: uppercase;
  font-weight: 700;
  display: inline-block;
  background-image: linear-gradient(
    to right,
    $color-primary-light,
    $color-primary-dark
  );
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  letter-spacing: 0.2rem;
  transition: all 0.2s;

  @include respond(tab-port) {
    font-size: 3rem;
  }

  @include respond(phone) {
    font-size: 2.5rem;
  }


  &:hover {
    transform: skewY(2deg) skewX(15deg) scale(1.1);
    text-shadow: 0.5rem 1rem 2rem rgba($color-black, 0.2);
  }
}

.heading-tertiary {
  font-size: $default-font-size;
  font-weight: 700;
  text-transform: uppercase;
}

.paragraph {
  font-size: $default-font-size;

  &:not(:last-child) {
    margin-bottom: 3rem;
  }
}
```

#### d. _utilities.scss
```css
.u-center-text {
  text-align: center !important;
}

.u-margin-bottom-small {
  margin-bottom: 1.5rem !important;
}

.u-margin-bottom-medium {
  margin-bottom: 4rem !important;

  @include respond(tab-port) {
    margin-bottom: 3rem !important;
  }
}

.u-margin-bottom-big {
  margin-bottom: 8rem !important;

  @include respond(tab-port) {
    margin-bottom: 5rem !important;
    margin-top: 2rem;
  }
}

.u-margin-top-big {
  margin-top: 8rem !important;
}

.u-margin-top-huge {
  margin-top: 10rem !important;

  @include respond(tab-port) {
    margin-top: 8rem !important;
  }
}
```

#### 3. components
#### 3.a _bg-video.scss
```css
.bg-video {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: -1;
    opacity: .15;
    overflow: hidden;

    &__content {
        height: 100%;
        width: 100%;
        object-fit: cover;
    }
}
```

#### 3.b _button.scss
```css
.btn {
  &,
  &:link,
  &:visited {
    text-transform: uppercase;
    text-decoration: none;
    padding: 1.2rem 3.5rem;
    display: inline-block;
    border-radius: 10rem;
    transition: all 0.2s;
    position: relative;
    font-size: $default-font-size;

    // Change for the <button> element
    border: none;
    cursor: pointer;
  }

  &:hover {
    transform: translateY(-0.3rem);
    box-shadow: 0 1rem 2rem rgba($color-black, 0.2);

    &::after {
      transform: scaleX(1.4) scaleY(1.6);
      opacity: 0;
    }
  }

  &:active,
  &:focus {
    outline: none;
    transform: translateY(-0.1rem);
    box-shadow: 0 0.5rem 1rem rgba($color-black, 0.2);
  }

  &--white {
    background-color: $color-white;
    color: $color-grey-dark;

    &::after {
      background-color: $color-white;
    }
  }

  &--green {
    background-color: $color-primary;
    color: $color-white;

    &::after {
      background-color: $color-primary;
    }
  }

  &::after {
    content: "";
    display: inline-block;
    height: 100%;
    width: 100%;
    border-radius: 10rem;
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    transition: all 0.4s;
  }

  &--animated {
    animation: moveInBottom 0.5s ease-out 0.75s;
    animation-fill-mode: backwards;
  }
}

.btn-text {
  &:link,
  &:visited {
    font-size: $default-font-size;
    color: $color-primary;
    display: inline-block;
    text-decoration: none;
    border-bottom: 1px solid $color-primary;
    padding: 1rem;
    transition: all 0.2s;
    border-radius: 0;
  }

  &:hover {
    background-color: $color-primary;
    color: $color-white;
    box-shadow: 0 1rem 2rem rgba($color-black, 0.15);
    transform: translateY(-0.2rem);
  }

  &:active {
    box-shadow: 0 0.5rem 1rem rgba($color-black, 0.15);
    transform: translateY(0);
  }
}
```

#### 3.b _card.scss
```css
.card {
  // FUNCTIONALITY
  perspective: 150rem;
  -moz-perspective: 150rem;
  position: relative;
  height: 52rem;

  &__side {
    height: 52rem;
    transition: all 0.8s ease;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    backface-visibility: hidden;
    border-radius: 0.3rem;
    overflow: hidden;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &--front {
      background-color: $color-white;
    }

    &--back {
      transform: rotateY(180deg);

      &-1 {
        background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        );
      }

      &-2 {
        background-image: linear-gradient(
          to right bottom,
          $color-primary-light,
          $color-primary-dark
        );
      }

      &-3 {
        background-image: linear-gradient(
          to right bottom,
          $color-tertiary-light,
          $color-tertiary-dark
        );
      }
    }
  }

  &:hover &__side--front {
    transform: rotateY(-180deg);
  }

  &:hover &__side--back {
    transform: rotateY(0);
  }

  //   FRONT SIDE STYLING

  &__picture {
    background-size: cover;
    height: 23rem;
    background-blend-mode: screen;
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 85%, 0 100%);
    border-top-left-radius: 0.3rem;
    border-top-right-radius: 0.3rem;

    &--1 {
      background-image: linear-gradient(
          to right bottom,
          $color-secondary-light,
          $color-secondary-dark
        ),
        url("../img/nat-5.jpg");
    }

    &--2 {
      background-image: linear-gradient(
          to right bottom,
          $color-primary-light,
          $color-primary-dark
        ),
        url("../img/nat-6.jpg");
    }

    &--3 {
      background-image: linear-gradient(
          to right bottom,
          $color-tertiary-light,
          $color-tertiary-dark
        ),
        url("../img/nat-7.jpg");
    }
  }

  &__heading {
    font-size: 2.8rem;
    font-weight: 300;
    text-transform: uppercase;
    color: $color-white;
    position: absolute;
    text-align: right;
    top: 11rem;
    right: 2rem;
    width: 75%;
  }

  &__heading-span {
    padding: 1rem 1.5rem;
    -webkit-box-decoration-break: clone;
    box-decoration-break: clone;

    &--1 {
      background-image: linear-gradient(
        to right bottom,
        rgba($color-secondary-light, 0.85),
        rgba($color-secondary-dark, 0.85)
      );
    }

    &--2 {
      background-image: linear-gradient(
        to right bottom,
        rgba($color-primary-light, 0.85),
        rgba($color-primary-dark, 0.85)
      );
    }

    &--3 {
      background-image: linear-gradient(
        to right bottom,
        rgba($color-tertiary-light, 0.85),
        rgba($color-tertiary-dark, 0.85)
      );
    }
  }

  &__details {
    padding: 3rem;

    ul {
      list-style: none;
      width: 80%;
      margin: 0 auto;

      li {
        text-align: center;
        font-size: 1.5rem;
        padding: 1rem;

        &:not(:last-child) {
          border-bottom: 1px solid $color-grey-light-2;
        }
      }
    }
  }

  //   BACK SIDE STYLING
  &__cta {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 90%;
    text-align: center;
  }

  &__price-box {
    text-align: center;
    color: $color-white;
    margin-bottom: 8rem;
  }

  &__price-only {
    font-size: 1.4rem;
    text-transform: uppercase;
  }
  &__price-value {
    font-size: 6rem;
    font-weight: 280;
  }

  // ********************* //

  // @include respond(tab-port) {
  @media only screen and (max-width: 56.25em), only screen and (hover: none) {
    height: auto;
    border-radius: 0.3rem;
    background-color: $color-white;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);

    &__side {
      height: auto;
      position: relative;
      box-shadow: none;

      &--back {
        transform: rotateY(0);
        clip-path: polygon(0 15%, 100% 0, 100% 100%, 0 100%);
      }
    }

    &:hover &__side--front {
      transform: rotateY(0);
    }

    &__details {
      padding: 0 1rem;
    }

    //   FRONT SIDE STYLING
    &__cta {
      position: relative;
      top: 0%;
      left: 0%;
      transform: translate(0);
      width: 100%;
      padding: 7rem 4rem 4rem 4rem;
    }

    &__price-box {
      margin-bottom: 3rem;
    }

    &__price-value {
      font-size: 4rem;
      font-weight: 380;
    }
  }
}

```

#### 3.d _composition.scss
```css
.composition {
  position: relative;

  &__photo {
    width: 55%;
    box-shadow: 0 1.5rem 4rem rgba($color-black, 0.4);
    border-radius: 0.2rem;
    position: absolute;
    z-index: 10;
    transition: all 0.2s;
    outline-offset: 2rem;

    @include respond(tab-port) {
      float: left;
      position: relative;
      width: 33.33333%;
      box-shadow: 0 1.5rem 3rem rgba($color-black, 0.2);
    }

    &--p1 {
      left: 0;
      top: -2rem;

      @include respond(tab-port) {
        top: 1rem;
        transform: scale(1.2);
      }
    }

    &--p2 {
      right: 0;
      top: 2rem;

      @include respond(tab-port) {
        top: -1rem;
        transform: scale(1.3);
        z-index: 100;
      }
    }

    &--p3 {
      left: 20%;
      top: 10rem;

      @include respond(tab-port) {
        left: 0;
        top: 1rem;
        transform: scale(1.2);
      }
    }

    &:hover {
      outline: 1.5rem solid $color-primary;
      transform: scale(1.05) translateY(-.5rem);
      box-shadow: 0 2.5rem 4rem rgba($color-black, 0.5);
      z-index: 20;
    }
  }

  &:hover &__photo:not(:hover) {
    transform: scale(0.9);
  }
}

```

#### 3.e _feature-box.scss
```css
.feature-box {
  background-color: rgba($color-white, 0.8);
  font-size: 1.5rem;
  padding: 2.5rem;
  text-align: center;
  border-radius: 0.3rem;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.15);
  transition: transform 0.3s;

  @include respond(tab-port) {
    padding: 2rem;
  }

  &__icon {
    font-size: 6rem;
    margin-bottom: 0.5rem;

    display: inline-block;
    background-image: linear-gradient(
      to right,
      $color-primary-light,
      $color-primary-dark
    );
    background-clip: text;
    -webkit-background-clip: text;
    color: transparent;

    @include respond(tab-port) {
      margin-bottom: 0;
    }
  }

  &:hover {
    transform: translateY(-1.5rem) scale(1.03);
  }
}

```

#### 3.f _form.scss
```css
.form {

    &__group:not(:last-child) {
        margin-bottom: 2rem;
    }

    &__input {
        font-size: 1.5rem;
        font-family: inherit;
        color: inherit;
        padding: 1.5rem 2rem;
        border-radius: .2rem;
        background-color: rgba($color-white, .5);
        border: none;
        border-bottom: .3rem solid transparent;
        width: 90%;
        display: block;
        transition: all .3s;

        @include respond(tab-port) {
            width: 100%;
        }

        &:focus {
            outline: none;
            box-shadow: 0 1rem 2rem rgba($color-black, .1);
            border-bottom: .3rem solid $color-primary;
        }

        &:focus:invalid {
            border-bottom: .3rem solid $color-secondary-dark;
        }

        &::-webkit-input-placeholder {
            color: $color-grey-dark-2;
        }    
    }
    

    &__label {
        font-size: 1.2rem;
        font-weight: 700;
        margin-left: 2rem;
        margin-top: .7rem;
        display: block;
        transition: all .3s;
    }

    &__input:placeholder-shown + &__label {
        opacity: 0;
        visibility: hidden;
        transform: translateY(-4rem);
    }

    &__radio-group {
        width: 49%;
        display: inline-block;

        @include respond(tab-port) {
            width: 100%;
            margin-bottom: 2rem;
        }
    }

    &__radio-input {
        display: none;
    }

    &__radio-label {
        font-size: $default-font-size;
        cursor: pointer;
        position: relative;
        padding-left: 4.5rem;
    }

    &__radio-button {
        height: 3rem;
        width: 3rem;
        border: .5rem solid $color-primary;
        border-radius: 50%;
        display: inline-block;
        position: absolute;
        left: 0;
        top: -.4rem;


        &::after {
            content: '';
            display: block;
            height: 1.3rem;
            width: 1.3rem;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: $color-primary;
            opacity: 0;
            transition: opacity .2s;
        }
    }

    &__radio-input:checked ~ &__radio-label &__radio-button::after {
        opacity: 1;
    }
}
```

#### 3.g _popup.scss
```css
.popup {
  height: 100vh;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: rgba($color-black, 0.8);
  z-index: 9999;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s;

  @supports (-webkit-backdrop-filter: blur(10px)) or
    (backdrop-filter: blur(18px)) {
    -webkit-backdrop-filter: blur(18px);
    backdrop-filter: blur(18px);
    background-color: rgba($color-black, 0.3);
  }

  &__content {
    @include absCenter;

    width: 75%;
    background-color: $color-white;
    box-shadow: 0 2rem 4rem rgba($color-black, 0.2);
    border-radius: 0.3rem;
    display: table;
    overflow: hidden;
    opacity: 0;
    transform: translate(-50%, -50%) scale(0.25);
    transition: all 0.4s 0.2s;
  }

  &__left {
    width: 33.33333%;
    display: table-cell;
  }

  &__right {
    width: 66.6666666%;
    display: table-cell;
    vertical-align: middle;
    padding: 3rem 5rem;
  }

  &__img {
    display: block;
    width: 100%;
  }

  &__text {
    font-size: 1.4rem;
    margin-bottom: 4rem;

    -moz-column-count: 2;
    column-count: 2;
    -moz-column-gap: 4rem;
    column-gap: 4rem;
    -moz-column-rule: 1px solid $color-grey-light-2;
    column-rule: 1px solid $color-grey-light-2;

    -moz-hyphens: auto;
    -ms-hyphens: auto;
    -webkit-hyphens: auto;
    hyphens: auto;
  }

  //   Open states

  &:target {
    opacity: 1;
    visibility: visible;
  }

  &:target &__content {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }

  &__closed {
    &:link,
    &:visited {
      color: $color-grey-dark;
      position: absolute;
      top: 2.5rem;
      right: 2.5rem;
      font-size: 3rem;
      text-decoration: none;
      display: inline-block;
      transition: all 0.2s;
      line-height: 1;
    }

    &:hover {
      color: $color-primary;
    }
  }
}

```

#### 3.h _story.scss
```css
.story {
    width: 75%;
    margin: 0 auto;
    box-shadow: 0 3rem 6rem rgba($color-black, .1);
    background-color: rgba($color-white, .6);
    border-radius: .3rem;
    padding: 6rem;
    padding-left: 9rem;
    font-size: $default-font-size;
    transform: skewX(-12deg);
    overflow: hidden;

    @include respond(tab-port) {
        width: 110%;
        padding: 4rem;
        padding-left: 7rem;    
    }

    @include respond(phone) {
        transform: skewX(0);
    }


    // & > * {
    //     transform: skewX(12deg);
    // }

    &__shape {
        width: 15rem;
        height: 15rem;
        float: left;
        -webkit-shape-outside: circle(50% at 50% 50%);
        shape-outside: circle(50% at 50% 50%);
        -webkit-clip-path: circle(50% at 50% 50%);
        clip-path: circle(50% at 50% 50%);
        transform: translateX(-3rem) skewX(12deg);
        position: relative;

        @include respond(phone) {
            transform: translateX(-3rem) skewX(0);
        }    
    }

    &__img {
        height: 100%;
        transform: translateX(-4rem) scale(1.4);
        // backface-visibility: visible;
        transition: all .5s;
    }

    &__text {
        transform: skewX(12deg);

        @include respond(phone) {
            transform: skewX(0);
        }    
    }

    &__caption {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, 20%);
        color: $color-white;
        text-transform: uppercase;
        font-size: 1.7rem;
        text-align: center;
        opacity: 0;
        transition: all .5s;
        // backface-visibility: hidden;
    }

    &:hover &__caption {
        opacity: 1;
        transform: translate(-50%, -50%);
    }

    &:hover &__img {
        transform: translateX(-4rem) scale(1);
        filter: blur(.3rem) brightness(80%);
    }
}
```

#### 4. layout
#### 4.a _footer.scss
```css
.footer {

    background-color: $color-grey-dark-3;
    padding: 10rem 15rem;
    font-size: 1.4rem;
    color: $color-grey-light-1;

    @include respond(tab-port) {
        padding: 8rem 0;
      }
  

    &__logo-box {
        text-align: center;
        margin-bottom: 8rem;

        @include respond(tab-port) {
            margin-bottom: 6rem;
          }
    }

    &__logo {
        width: 15rem;
        height: auto;
    }

    &__navigation {
        border-top: 1px solid $color-grey-dark;
        padding-top: 2rem;
        display: inline-block;

        @include respond(tab-port) {
            width: 100%;
            text-align: center;
          }
    
    }

    &__list {
        list-style: none;
    }

    &__item {
        display: inline-block;

        &:not(:last-child) {
            margin-right: 1.5rem;
        }
    }

    &__link {

        &:link, &:visited {
            color: inherit;
            background-color: $color-grey-dark-3;
            text-decoration: none;
            text-transform: uppercase;
            display: inline-block;
            transition: all .2s;
        }

        &:hover, &:active {
            color: $color-primary;
            box-shadow: 0 1rem 2rem rgba($color-black, .4);
            transform: rotate(5deg) scale(1.3);
        }
    }

    &__copyright {
        border-top: 1px solid $color-grey-dark;
        padding-top: 2rem;
        width: 70%;
        float: right;

        @include respond(tab-port) {
            width: 100%;
            float: none;
          }
    }
}
```

#### 4.b _grid.scss
```css
.row {
  max-width: $grid-width;
  margin: 0 auto;

  &:not(:last-child) {
    margin-bottom: $gutter-vertical;

    @include respond(tab-port) {
      margin-bottom: $gutter-vertical-small;
    }
  }

  @include respond(tab-port) {
    max-width: 50rem;
    padding: 0 3rem;
  }

  @include clearfix;

  [class^="col-"] {
    float: left;

    &:not(:last-child) {
      margin-right: $gutter-horizontal;

      @include respond(tab-port) {
        margin-right: 0;
        margin-bottom: $gutter-vertical-small;
      }
    }

    @include respond(tab-port) {
      width: 100% !important;
    }
  }

  .col-1-of-2 {
    width: calc((100% - #{$gutter-horizontal}) / 2);
  }

  .col-1-of-3 {
    width: calc((100% - 2 * #{$gutter-horizontal}) / 3);
  }

  .col-2-of-3 {
    width: calc(2 * ((100% - 2 * #{$gutter-horizontal}) / 3) + #{$gutter-horizontal});
  }

  .col-1-of-4 {
    width: calc((100% - 3 * #{$gutter-horizontal}) / 4);
  }

  .col-2-of-4 {
    width: calc(2 * ((100% - 3 * #{$gutter-horizontal}) / 4) + #{$gutter-horizontal});
  }

  .col-3-of-4 {
    width: calc(3 * ((100% - 3 * #{$gutter-horizontal}) / 4) + 2 * #{$gutter-horizontal});
  }
}
```

#### 4.c _header.scss
```css
.header {
  height: 95vh;
  background-image: linear-gradient(
      to right bottom,
      rgba($color-primary-light, 0.8),
      rgba($color-primary-dark, 0.8)
    ),
    url("../img/hero-small.jpg");
  background-size: cover;
  background-position: top;
  position: relative;

  -webkit-clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
  clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);

  // @supports (clip-path: polygon(0, 0)) or (-webkit-clip-path: polygon(0, 0)) {
  //   -webkit-clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
  //   clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%);
  //   height: 95vh;
  // }

  @media only screen and (min-resolution: 192dpi) and (min-width: 37.5em),
    only screen and (-webkit-min-device-pixel-ratio: 2) and (min-width: 37.5em),
    only screen and (min-width: 125em) {
    background-image: linear-gradient(
        to right bottom,
        rgba($color-primary-light, 0.8),
        rgba($color-primary-dark, 0.8)
      ),
      url("../img/hero.jpg");
  }

  @include respond(phone) {
    -webkit-clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
    clip-path: polygon(0 0, 100% 0, 100% 85vh, 0 100%);
  }

  &__logo-box {
    position: absolute;
    top: 4rem;
    left: 4rem;
  }

  &__logo {
    height: 3.5rem;
  }

  &__text-box {
    position: absolute;
    top: 43%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
  }
}

```

#### 4.d _navigation.scss
```css
.navigation {
  &__checkbox {
    display: none;
  }

  &__button {
    background-color: $color-white;
    height: 7rem;
    width: 7rem;
    position: fixed;
    top: 6rem;
    right: 6rem;
    border-radius: 50%;
    z-index: 2000;
    box-shadow: 0 1rem 3rem rgba($color-black, 0.1);
    text-align: center;
    cursor: pointer;

    @include respond(tab-port) {
      top: 4rem;
      right: 4rem;  
    }

    @include respond(phone) {
      top: 3rem;
      right: 3rem;  
    }

  }

  &__background {
    height: 6rem;
    width: 6rem;
    border-radius: 50%;
    position: fixed;
    top: 6.5rem;
    right: 6.5rem;
    background-image: radial-gradient(
      $color-primary-light,
      $color-primary-dark
    );
    z-index: 1000;
    transition: transform 0.8s cubic-bezier(.91,-0.02,.14,.96);

    @include respond(tab-port) {
      top: 4.5rem;
      right: 4.5rem;  
    }

    @include respond(phone) {
      top: 3.5rem;
      right: 3.5rem;  
    }

  }

  &__nav {
    height: 100vh;
    position: fixed;
    top: 0;
    left: 0;
    z-index: 1500;
    opacity: 0;
    width: 0;
    transition: all 0.8s cubic-bezier(.91,-0.02,.07,1.23);
  }

  &__list {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    list-style: none;
    text-align: center;
    width: 100%;
  }

  &__item {
    margin: 1rem;
  }

  &__link {
    &:link,
    &:visited {
      display: inline-block;
      font-size: 2.5rem;
      font-weight: 380;
      padding: 1rem 2rem;
      color: $color-white;
      text-decoration: none;
      text-transform: uppercase;
      background-image: linear-gradient(
        120deg,
        transparent 0%,
        transparent 50%,
        $color-white 50%
      );
      background-size: 220%;
      transition: all 0.4s;

      span {
        margin-right: 1.5rem;
        display: inline-block;
      }
    }

    &:hover,
    &:active {
      background-position: 100%;
      color: $color-primary;
      transform: translateX(1rem);
    }
  }

  //   FUNCTIONALITY

  &__checkbox:checked ~ &__background {
    transform: scale(80);
  }

  &__checkbox:checked ~ &__nav {
    opacity: 1;
    width: 100%;
  }

  // ICON
  &__icon {
    position: relative;
    margin-top: 3.5rem;

    &,
    &::before,
    &::after {
      width: 3rem;
      height: 3px;
      background-color: $color-grey-dark-3;
      display: inline-block;
    }

    &::before,
    &::after {
      content: "";
      position: absolute;
      left: 0;
      transition: all 0.2s;
    }

    &::before {
      top: -0.8rem;
    }

    &::after {
      top: 0.8rem;
    }
  }

  &__button:hover &__icon::before {
    top: -1rem;
  }

  &__button:hover &__icon::after {
    top: 1rem;
  }

  &__checkbox:checked + &__button &__icon {
    background-color: transparent;
  }

  &__checkbox:checked + &__button &__icon::before {
    top: 0;
    transform: rotate(135deg);
  }
  &__checkbox:checked + &__button &__icon::after {
    top: 0;
    transform: rotate(-135deg);
  }
}
```

#### 5. pages
#### 5.a _home.scss
```css
.section-about {
  background-color: $color-grey-light-1;
  padding: 25rem 0;
  margin-top: -20vh;

  @include respond(tab-port) {
    padding: 20rem 0;
  }
}

.section-features {
  padding: 20rem 0;
  background-image: linear-gradient(
      to right bottom,
      rgba($color-primary-light, 0.8),
      rgba($color-primary-dark, 0.8)
    ),
    url("../img/nat-4.jpg");
  background-size: cover;

  transform: skewY(-7deg);
  margin-top: -10rem;

  & > * {
    transform: skewY(7deg);
  }

  @include respond(tab-port) {
    padding: 10rem 0;
  }
}

.section-tours {
  background-color: $color-grey-light-1;
  padding: 25rem 4rem 15rem 4rem;
  margin-top: -10rem;

  @include respond(tab-port) {
    padding: 20rem 0 10rem 0;
  }
}

.section-stories {
  position: relative;
  padding: 15rem 0;
}

.section-book {
  padding: 15rem 0;
  background-image: linear-gradient(
    to right bottom,
    $color-primary-light,
    $color-primary-dark
  );

  @include respond(tab-port) {
    padding: 10rem 0;
  }
}

.book {
  background-image: linear-gradient(
      105deg,
      rgba($color-white, 0.9) 0%,
      rgba($color-white, 0.9) 50%,
      transparent 50%
    ),
    url("../img/nat-10.jpg");
  background-size: cover;
  border-radius: 0.3rem;
  box-shadow: 0 1.5rem 4rem rgba($color-black, 0.2);

  @include respond(tab-land) {
    background-image: linear-gradient(
        105deg,
        rgba($color-white, 0.9) 0%,
        rgba($color-white, 0.9) 60%,
        transparent 60%
      ),
      url("../img/nat-10.jpg");
      background-size: cover;
  }

  @include respond(tab-port) {
    background-image: linear-gradient(
      to right,
      rgba($color-white, 0.9) 0%,
      rgba($color-white, 0.9) 100%,
    ),
    url("../img/nat-10.jpg");
  }

  &__form {
    width: 50%;
    padding: 6rem;

    @include respond(tab-land) {
      width: 60%;
    }

    @include respond(tab-port) {
      width: 100%;
    }
  }
}
```

## main.scss
```css
@import "abstracts/functions";
@import "abstracts/mixins";
@import "abstracts/variables";

@import "base/animation";
@import "base/base";
@import "base/typography";
@import "base/utilities";

@import "components/button";
@import "components/composition";
@import "components/feature-box";
@import "components/card";
@import "components/story";
@import "components/bg-video";
@import "components/form";
@import "components/popup";

@import "layout/grid";
@import "layout/header";
@import "layout/footer";
@import "layout/navigation";

@import "pages/home";
```