<template>
  <div><router-view /></div>
</template>

<script>
export default {};
</script>

<style lang="scss" >
@import url(https://fonts.googleapis.com/css?family=Rubik:300,regular,500,600,700,800,900,300italic,italic,500italic,600italic,700italic,800italic,900italic);

// Стили скролла

::-webkit-scrollbar {
  width: 10px; /* ширина для вертикального скролла */
  height: 10px; /* высота для горизонтального скролла */
  background-color: #0e2846;
}
::-webkit-scrollbar-thumb {
  background-color: #350452;
  border-radius: 9em;
  box-shadow: inset 1px 1px 10px #f3faf7;
}

// Обнуление стилей
* {
  padding: 0;
  margin: 0;
  border: 0;
}

*,
*:before,
*:after {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}

:focus,
:active {
  outline: none;
}
a:focus,
a:active {
  outline: none;
}

nav,
footer,
header,
aside {
  display: block;
}

html,
body {
  background-color: #0f1215;
  font-family: Rubik;
  height: 100%;
  width: 100%;
  font-size: 100%;
  line-height: 1;
  font-size: 14px;
  -ms-text-size-adjust: 100%;
  -moz-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
}

input,
button,
textarea {
  font-family: inherit;
}

input::-ms-clear {
  display: none;
}
button {
  cursor: pointer;
}
button::-moz-focus-inner {
  padding: 0;
  border: 0;
}
a,
a:visited {
  text-decoration: none;
}
a:hover {
  text-decoration: none;
}
ul li {
  list-style: none;
}
img {
  vertical-align: top;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  font-size: inherit;
  font-weight: 400;
}
</style>