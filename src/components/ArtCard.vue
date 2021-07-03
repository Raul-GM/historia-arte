<template>
  <div class="artcard">
    <p>
      <span
        class="icon-button icon-solve"
        v-on:click="onSolveArtCard()"
        title="Resolver"
      ></span>
      <span
        class="icon-button icon-next"
        v-on:click="onNextCard()"
        title="Siguiente Obra"
        v-if="artSelected < artList.length - 1"
      ></span>
    </p>
    <a v-if="artList[artSelected].url" :href="artList[artSelected].url" target="_blank"> <img class="artcard-image" :src="artList[artSelected].url" /></a>
    <h1 v-if="artList[artSelected].title">{{ artList[artSelected].title }}</h1>
    <p><strong>Artista</strong> {{ artList[artSelected].artist }}</p>
    <p><strong>Nombre:</strong> {{ artList[artSelected].name }}</p>
    <div v-if="solved" class="art-data">
      <p><strong>Estilo:</strong> {{ artList[artSelected].style }}</p>
      <p><strong>Descripción:</strong> {{ artList[artSelected].information }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ArtCard',
  props: {
    artList: {
      type: Array,
      default: () => [],
    },
    artSelected: {
      type: Number,
      default: () => -1,
    },
    solved: {
      type: Boolean,
      default: () => false,
    },
    onSolveArtCard: {
      type: Function,
      default: () => false,
    },
    onNextCard: {
      type: Function,
      default: () => false,
    }
  },
}
</script>

<style scoped>
.artcard {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.artcard-image {
  min-height: 60vh;
  max-height: 60vh;
  border: 4px solid #000000;
}
.art-data {
  width: 60vw;
}
.art-data p {
  margin: .5rem 0;
}
</style>
