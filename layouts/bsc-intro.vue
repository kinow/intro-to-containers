<template>
  <div class="bsc-intro">
    <div class="slidev-layout intro">
      <slot />
    </div>
  </div>
</template>

<style>
.bsc-intro {
  background-image: url('/images/bsc-bg2.jpg');
  background-size: cover;
  height: 100%;
}

.bsc-intro .intro {
  display: flex !important;
  justify-content: flex-start;
  height: 100%;
}

.bsc-intro .intro h1 {
  font-size: 6em !important;
  display: block;
  margin: auto 0;
}
</style>
