<template>
  <div class="de-thankyou">
    <div class="de-thankyou-header">
      <h1>Destination<br/>Earth</h1>
    </div>
    <div class="slidev-layout cover my-title">
      <h1 class="title">Thank you</h1>
    </div>
  </div>
</template>

<style>
.de-thankyou {
  background-color: #11122A;
  display: grid;
  grid-template: 10% 90% / 100%;
  height: 90%;
  font-family: Helvetica, sans-serif;
  background-image: url('/images/de-default-bg.png');
  background-size: 100px;
  background-repeat: no-repeat;
  background-position-x: 3.5rem;
  background-position-y: bottom 1.5%;
}

.de-thankyou .slidev-layout {
  padding-top: 0.5rem !important;
}

.de-thankyou > .my-title {
  background-image: url('/images/de-thankyou.png');
  background-size: cover;
}

.de-thankyou > .my-title > .title {
  text-align: left;
  font-weight: normal;
  font-size: 5rem !important;
  align-self: center;
}

.de-thankyou-header h1 {
  font-size: 1rem !important;
  display: inline-block;
  align-self: flex-end;
  padding-left: 3.5rem;
  padding-right: 2rem;
  border-bottom: 1px solid #62BCAD;
}

.de-thankyou-header h1 {
  font-size: 1rem !important;
  display: inline-block;
  align-self: flex-end;
  padding-left: 3.5rem;
  padding-right: 2rem;
  border-bottom: 1px solid #62BCAD;
}

.de-thankyou h1, h2, h3 h4, h5, h6 {
  color: #62BCAD !important;
  text-transform: uppercase;
  font-weight: normal;
}
</style>
