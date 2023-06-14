<template>
  <div class="de-default">
    <div class="de-default-header">
      <h1>Destination<br/>Earth</h1>
    </div>
    <div class="slidev-layout">
      <slot />
    </div>
  </div>
</template>

<style>
.de-default {
  font-family: Helvetica, sans-serif;
  background-image: url('/images/de-default-bg.png');
  background-size: 100px;
  background-repeat: no-repeat;
  background-position-x: 3.5rem;
  background-position-y: bottom 1.5%;
  display: grid;
  grid-template: 10% 90% / 100%;
  height: 90%;
}

.de-default .slidev-layout {
  padding-top: 0.5rem !important;
}

.de-default .slidev-layout .footnotes {
  margin-left: 110px !important;
}

.de-default-header {
  grid-row: 1;
  vertical-align: bottom;
  display: flex;
  height: 100%;
}

.de-default-header h1 {
  font-size: 1rem !important;
  display: inline-block;
  align-self: flex-end;
  padding-left: 3.5rem;
  padding-right: 2rem;
  border-bottom: 1px solid #62BCAD;
}

.de-default h1, h2, h3 h4, h5, h6 {
  color: #62BCAD !important;
  text-transform: uppercase;
  font-weight: normal;
}

.de-default .slidev-layout h1 {
  font-family: Rajdhani Semibold, sans-serif;
  font-size: 1.4rem !important;
  display: block;
  position: relative;
  padding: 0;
  margin: 0 0 0.5rem 0;
}

.center1 {
  min-height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  flex-direction: row;
}
.center1 > * {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
}

.center2 {
  min-height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
  flex-direction: row;
}
.center2 + * {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
}
</style>
