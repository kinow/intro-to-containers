<template>
  <div class="de-title">
    <div class="slidev-layout my-title">
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
  display: flex;
  flex-direction: column;
}

.de-title > div {
  display: flex;
  flex-direction: row;
  flex-grow: 1;
  flex-basis: available;
}

.de-title > footer {
  display: flex;
  flex-direction: row;
  flex-grow: 0;
  flex-shrink: 1;
  flex-basis: 100px;
}

.de-title > .my-title {
  background-image: url('/images/de-title.png');
  background-size: contain;
  background-repeat: no-repeat;
  background-position-x: center;
  min-height: 90%;
}

.de-title > .my-title > .title {
  text-align: left;
  font-size: 5rem !important;
  margin: auto 0;
  width: 100%;
  text-align: right;
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
