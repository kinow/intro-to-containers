<template>
  <div class="bsc-title">
    <div class="slidev-layout cover my-title">
      <h1 class="title">{{ props.slidesTitle }}</h1>
    </div>
    <footer>
      <div class="date">{{ props.slidesDate }}</div>
      <div class="venue">{{ props.slidesVenue }}</div>
    </footer>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  slidesTitle: {
    type: String,
  },
  slidesDate: {
    type: String,
  },
  slidesVenue: {
    type: String,
  }
})
</script>

<style>
.bsc-title > .my-title {
  background-image: url('/images/bsc-bg.jpg');
  background-size: cover;
  padding-top: 200px;
  padding-left: 400px;
}

.bsc-title > .my-title > .title {
  text-align: left;
  font-weight: bold;
  font-size: 5rem !important;
}

.bsc-title > footer {
  position: absolute;
  bottom: 0;
  padding: 0 0;
  font-weight: bold;
  display: grid;
  grid-template-columns: 33% 67%;
  min-width: 100%;
}

.bsc-title > footer > div {
  padding: 20px 0;
}

.bsc-title > footer > div.date {
  color: white;
}

.bsc-title > footer > div.venue {
  color: #004890;
  text-align: left;
  padding-left: 75px;
}

</style>
