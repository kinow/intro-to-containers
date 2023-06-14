<template>
  <div class="de-title">
    <div class="slidev-layout cover my-title">
      <div class="title">
        <h1>Destination<br/>Earth</h1>
        <h2>{{ props.slidesTitle }}</h2>
        <p class="author">{{ props.slidesAuthor }}</p>
      </div>
    </div>
    <footer><p>&nbsp;</p></footer>
  </div>
</template>

<script setup lang="ts">
const props = defineProps({
  slidesTitle: {
    type: String,
  },
  slidesAuthor: {
    type: String,
  }
})
</script>

<style>
.de-title {
  max-height: 97.5%;
}

.de-title > .my-title {
  background-image: url('/images/de-title.png');
  background-size: contain;
  background-repeat: no-repeat;
  max-height: 90%;
  left: 5%;
  position: relative;
  display: grid;
  grid-template: 90% 10% / 50% 50%;
}

.de-title > .my-title > .title {
  text-align: left;
  font-weight: bold;
  font-size: 5rem !important;
  grid-row: 1;
  grid-column: 2;
  align-items: center;
  align-content: center;
  margin: auto 0;
}

.de-title > .my-title > .title > h1 {
  font-size: 3rem;
  text-transform: uppercase;
  color: #62BCAD;
  font-family: 'Rajdhani Medium', sans-serif;
  line-height: 1em;
  font-weight: normal;
}

.de-title > .my-title > .title > h2 {
  font-size: 3rem;
  text-transform: uppercase;
  color: #808080;
  font-family: 'Rajdhani Semibold', sans-serif;
  line-height: 1em;
  font-weight: normal;
}

.de-title > .my-title > .title > p.author {
  color: #A8A8A8;
  font-size: 2rem;
  font-weight: normal;
  font-family: Helvetica, sans-serif;
  line-height: 1em;
  margin-top: 5rem;
}

.de-title > footer {
  width: 100%;
  height: 100%;
  vertical-align: top;
  alignment-baseline: top;
}

.de-title > footer > p {
  background-image: url('/images/de-title-footer.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position: top center;
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100%;
}
</style>
