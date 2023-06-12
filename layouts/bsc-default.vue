<template>
  <div class="bsc-default">
    <div class="slidev-layout">
      <slot />
    </div>
  </div>
</template>

<style>
.bsc-default {
  background-image: url('/images/bsc-bg2.jpg');
  background-size: cover;
}

.bsc-default h1 {
  font-size: 2rem;
  display: block;
}

.center {
  min-height: 100%;
  display: flex;
  flex-wrap: wrap;
  align-content: center;
}
.center + * {
  display: flex;
  flex-direction: column;
  flex-basis: 100%;
}
</style>
