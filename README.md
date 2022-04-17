<div align="center">
<img src="https://elzero.org/wp-content/themes/elzero/imgs/logo.png" alt='source' width="200"/>

# Elzero Web School

[SASS Course](https://www.youtube.com/playlist?list=PLDoPjvoNmBAzlpyFHOaB3b-eubmF0TAV2)
</div>

# 02 sass compiler

- [Sass Meister](https://www.sassmeister.com/)
- [Codepen](https://codepen.io/trending)
- [Live SASS Compiler](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass)
- [PrePros](https://prepros.io/)
- [Koala](http://koala-app.com/)

There are two file extension fro sass files `.sass` and `.scss` the `.scss` is most like `.css` as it have semicolon `;`

---

# 03

- `@import` will be depreacated in new version in sass so use `@use`
- `_filename.scss` when put undersocer `_` before file name that mean it wom't be compiled but it used only to be include and u can call it with out `_` for example

```//file name
_global-rules.scss

// importing into main.scss
@use "./a/b/global-config.scss"
```

- Anything u will include into `main.scss` u should do the previous method but if u want the file alone don't do it.

---

# 04 Variables

- css var `vs` scss var
  <br>
- `css var`
  -- when u use it the `var name` will be refrenced but when using
  -- created int root with two dash prefix `--`
  <br>
- `scss var`
  -- the `value` will be refrenced
  -- created in any thing by dollar sign `$`
  <br>
- to change global var u can use `!global` for example
- u can create file for var names to use it u must import file in file u want `@use "./var/var-names"` but with this u can't use ur var to fix that there are two ways
  --`@use "./var/var-names" as *` it will show everything or `$var01`
  --`@use "./var/var-names"` it will show everything or and use var like that `var-names.$var01`
  <br>
- $max-mobile : "max-width: 767px"

---

# 05 Nesting & Parent Element

```
.parent {
  font-weight: bold;
  .child {
    font-size: 20px;
    .grand-child {
      font-size: 15px;
    }
  }
}
```

Equivelant

```
.parent {
  font-weight: bold;
}

.parent .child {
    font-size: 20px;
    .grand-child {
      font-size: 15px;
    }
}

.parent .child .grand-child {
      font-size: 15px;
}
```

U can use all operator from css as selector

```
.parent {
  > .child {
    font-size: 20px;
  }
  .test {
    font-weight: bold;
  }
  + p {
    font-size: 15px;
  }
}
```

U can use and operator `&` to refrance parent as in the code below and it called `parent`

```
.box {
  .title {
    font-size: 10px;
  }
  .description {
    font-size: 8px;
  }
  &.red {
    color: red;
  }
  &.green {
    color: green;
  }
  &:hover {
    background-color: #eee;
  }
  &:hover .title {
    font-weight: bold;
  }
  :not(&) {
    font-weight: normal;
  }
  [dir="rtl"] & {
    direction: rtl;
  }
}
```

# 06 Property Declarations And Placeholder

- Property Declarations

  ```
  .box {
    font-size: 20px;
    font: {
      size: 15px;
      weight: bold;
    }
    padding: 10px;
    margin: auto {
      top: 10px;
      bottom: 15px;
    }
  }
  ```

  <br>

- U can extend properties like oreder isnot required

  ```

  .main-box {
  background-color: white;
  padding: 15px;
  border: 1px solid #ccc;
  }

  .ads {
  @extend .main-box;
  font-size: 20px;
  color: red;
  }

  .article {
  font-size: 22px;
  @extend .main-box;
  color: green;
  }

  ```

  U can achieve pervouis with css grouping

<br>

- With pervouis method the declation u used should be used in your website but what if u want this as only as code organization and u won't use it in your website here come consept of `placeholder`

  ```
  %main-box {
    background-color: white;
    padding: 15px;
    border: 1px solid #ccc;
  }

  .ads {
    @extend %main-box;
    font-size: 20px;
    color: red;
  }

  .article {
    font-size: 22px;
    @extend %main-box;
    color: green;
  }
  ```

---

# 07 - Control Flow

```
// Control Flow => If And Else

$theme: "dark";

.page {
  @if $theme == "light" {
    background-color: white;
    color: #444;
  } @else {
    background-color: #444;
    color: white;
  }
}
```

- There is a thing like Ternanry operator and it's like
  `if(condition, [do if true], [do if false])`

- if compiler find `null` the line won't be compiled or it will be erased

```
$rounded: false;

.box {
  @extend %main-box;
  border-radius: if($rounded, 6px, null);
}
```

---

# 08

- `@error` u can use it to throw error
- Interpolation `#{var}` u can use it to call variables

---

# 09 - Interpolation

- `unique-id()` U can use this function to generate unique id

- In interpolation u can call variableds and funcions

```
$company: "falcon";
$position: "right";

.ad-#{$company}-#{unique-id()} {
  font-size: 20px;
  background-image: url("imgs/#{$company}.png");
  #{$position}: 0;
}
.ad-#{unique-id()} {
  font-weight: bold;
}
```

---

# 10 Comments

- There are diffrent type of comment and visibilty

  ```
  // Comments

  // This Comment Will Not Show In CSS File

  /* This Comment Will Show In CSS File But Not In Compressed Mode */

  /*! This Comment Will Show In CSS File And In Compressed Mode */
  ```

- U can type comment anywhere

  ```

  .box /* Multiple
  Lines
  Comment */ {
    font-size: 20px; // Inline Comment
  }

  /* This Comment Contains Interpolation => #{$company} */
  ```

- Documentation

  ```
  /// Function To Do Bla Bla Bla
  ///
  /// @param {num}
  /// The Number To Deal With
  /// @return {int}
  ```

---

# 11 - Mixin And Include

- Mixin used like function in js u can define it and use it anywhere `at this point placeholder can do the job`
- U have the ability to pass parameters to it `Here Mixin shows it potentials`

```
ul.links {
  @include list-reset;
}

.circle-100 {
  @include circle(100px);
  background-color: red;
  color: white;
}

.circle-200 {
  @include circle(200px);
  background-color: red;
  color: white;
}

.center-circle {
  @include circle(400px);
  @include centering;
}
```

- When project become bigger and u have much Mixin it's recommended to define a seperated folder for example`sass/helpers/_mixins.scss` and collect all mixin in it.
- Don't forget to use documentaion to define param and return
- Note `_` underscoer used as this file won't be compailed and it will only used to be imported

- Some mixin library from Github
  -- [7ninjas/scss-mixins](https://github.com/7ninjas/scss-mixins)
  -- [wagerfield/cssmixins](https://github.com/wagerfield/cssmixins)

---

# 12 - Loop – For

`to` dosn't include end
`through` include end

```
@for $i from 1 through 10 {
}

@for $i from 1 to 10 {
  .class-#{$i} {
    font-size: #{$i + 10px};
  }
}
```

```
$dimensions: 0;

@for $i from 1 through 10 {
  .circle-#{100 + $dimensions} {
    width: $dimensions + 100px;
    height: $dimensions + 100px;
    border-radius: 50%;
  }
  $dimensions: $dimensions + 100;
}
```

---

# 13 - Loop - Each And Maps

- Each

  ```
  $themes: red, green, blue, orange;

  @each $theme in $themes {
    .#{$theme}-theme {
      .product {
        background-color: white;
        border-bottom: 2px solid $theme;
        .title {
          color: $theme;
          font-weight: bold;
        }
      }
    }
  }
  ```

- Map

  ```
  $socials: (
    "facebook": blue,
    "youtube": red,
    "github": black,
    "twitter": indianred,
  );

  @each $name, $color in $socials {
    .#{$name} {
      background-color: $color;
      color: white;
      &::before {
        content: $name;
      }
    }
  }
  ```

- Desctruction concept

  ```

  $classes: "one" 20px red, "two" 15px green, "three" 22px blue;

  @each $class, $font, $color in $classes {
    .#{$class} {
      font-size: $font;
      background-color: $color;
      color: white;
      padding: $font / 2;
    }
  }
  ```

---

# 14 - Loop - While

Don't forget to implement condition otherwise there will be an infinte loop

```
$start: 1;

@while $start <= 10 {
  .width-#{$start * 100} {
    width: $start * 100px;
    height: ($start * 100px) / 2;
  }
  $start: $start + 1;
}
```

---

# 15 - Create Bootstrap Grid System

- `percentage($i / $grid_cols)` built in function to cal percentage

```
// Create Grid System

$grid_cols: 12;

@for $i from 1 through $grid_cols {
  .col-#{$i} {
    width: percentage($i / $grid_cols);
  }
}
```

---

# 16 - Function

- When project become bigger and u have much functions it's recommended to define a seperated folder for example`sass/helpers/_functions.scss` and collect all functions in it.
- Don't forget to use documentaion to define param and return
- Note `_` underscoer used as this file won't be compailed and it will only used to be imported

- If U have function with non defined number of parameters u can use `varName...` and access it with `each`

```
/// Function To Get Element Height
///
/// @param {size}
/// Element Width
/// @return {int}
/// Return Element Height => Width / 2

@function half($size) {
  @return $size / 2;
}

@function calculate($sizes...) {
  $total: 0;
  @each $size in $sizes {
    $total: $total + $size;
  }
  @return $total;
}
```

---

# 17 - Practice Mixin With Content

U can use `@content` with `@mixin` to allow write content when mixin called

```
@mixin keyF($anim-name) {
  @-webkit-keyframes #{$anim-name} {
    @content;
  }
  @keyframes #{$anim-name} {
    @content;
  }
}
```

```
@include keyF(fade-in) {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
@include keyF(go-up) {
  from {
    bottom: 0;
  }
  to {
    bottom: 100px;
  }
}
```

---

# 18 - Practice Create Media Queries Mixin

```
// If Condition + Mixin + Content

.media {
  @include breakpoints(mobile) {
    font-size: 15px;
  }
  @include breakpoints(small) {
    font-size: 18px;
  }
  @include breakpoints(medium) {
    font-size: 20px;
  }
  @include breakpoints(large) {
    font-size: 22px;
  }
}
```

```
@mixin breakpoints($point) {
  @if $point == mobile {
    @media (max-width: 767px) {
      @content;
    }
  } @else if $point == small {
    @media (min-width: 768px) and (max-width: 991px) {
      @content;
    }
  } @else if $point == medium {
    @media (min-width: 992px) and (max-width: 1199px) {
      @content;
    }
  } @else if $point == large {
    @media (min-width: 1200px) {
      @content;
    }
  }
}
```

---

# 19 - The End And How To Master SASS

- [7ninjas](https://github.com/7ninjas/scss-mixins)
- [drublic](https://github.com/drublic/Sass-Mixins)
- [yannickcr](https://github.com/yannickcr/Sass-mixins)
- [huanz](https://github.com/huanz/mixins)

## Practise
