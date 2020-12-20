<template>
  <div>
    <nuxt />
  </div>
</template>

<style lang="scss">
html {
  height: 100%;
}

body {
  height: 100%;
  background-color: #000a38d9;
  background-image: url('~assets/images/bucket-big.jpg');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
  background-repeat: no-repeat;
  font-family: 'Fira Sans', sans-serif;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  color: #0dc7cc;
}

p,
.text-light {
  color: #dfebff !important;
}

a {
  color: #dfebff;
  text-decoration: underline;

  &:hover,
  &:focus {
    color: #965496 !important;
  }
}

.font-wide {
  /* font-family: 'CHERL', sans-serif; */
  font-family: 'Lexend Zetta', sans-serif;
}

#__layout {
  background-color: #000a38d9;
}

@media (max-width: 720px) {
  .display-4 {
    font-size: 2.5rem;
  }
}

@media (max-width: 540px) {
  .display-4 {
    font-size: 2rem;
  }
}
</style>
