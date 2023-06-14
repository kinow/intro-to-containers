<template>
  <div class="de-intro">
    <div class="de-intro-header">
      <h1>Destination<br/>Earth</h1>
    </div>
    <div class="slidev-layout intro">
      <slot />
    </div>
  </div>
</template>

<style>
.de-intro {
  font-family: Helvetica, sans-serif;
  background-image: url('/images/de-default-bg.png');
  background-size: 100px;
  background-repeat: no-repeat;
  background-position-x: 3.5rem;
  background-position-y: bottom;
  display: grid;
  grid-template: 10% 90% / 100%;
  height: 90%;
}

.de-intro-header {
  grid-row: 1;
  vertical-align: bottom;
  display: flex;
  height: 100%;
}

.de-intro-header h1 {
  font-size: 1rem !important;
  display: inline-block;
  align-self: flex-end;
  padding-left: 3.5rem;
  padding-right: 2rem;
  border-bottom: 1px solid #62BCAD;
  font-family: Rajdhani Semibold, sans-serif;
  color: #62BCAD;
  font-weight: normal;
  text-transform: uppercase;
}

.de-intro .intro {
  display: flex !important;
  justify-content: flex-start;
}

.de-intro .intro h1 {
  font-size: 4em !important;
  display: block;
  margin: auto 0;
  font-family: Rajdhani Semibold, sans-serif;
  color: #62BCAD;
  text-transform: uppercase;
}
</style>
