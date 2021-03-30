<template>
  <div class="artcard">
    <img class="artcard-image" :src="artData.url" />
    <button v-on:click="onSolveArtCard()">Resolver</button>
    <div v-if="solved">
      <p>Pintor/a: {{ artData.artist }}</p>
      <p>Nombre: {{ artData.name }}</p>
      <p>Estilo: {{ artData.style }}</p>
      <p>Descripción: {{ artData.information }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ArtCard',
  props: {
    artData: {
      type: Object,
      default: () => {}
    },
    solved: {
      type: Boolean,
      default: () => false,
    },
    onSolveArtCard: {
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
  max-width: 60vw;;
}
</style>
