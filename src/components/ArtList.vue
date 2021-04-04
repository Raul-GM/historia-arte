<template>
  <div>
    <div class="title-container">
      <h1>Historia del Arte Contemporáneo</h1>
      <span class="icon-button icon-flag" v-on:click="getRandomArt()" title="Empezar prueba"></span>
    </div>
    <article v-if="artSelected >= 0">
      <ArtCard :artList="artList" :solved="solved" :onSolveArtCard="solveArtCard" :onNextCard="onNextCard" :artSelected="artSelected"/>
    </article>
  </div>
</template>

<script>
import ArtCard from './ArtCard.vue'

export default {
  name: 'ArtistList',
  components: {
    ArtCard
  },
  props: {
    
  },
  data() {
    return {
      artSelected: -1,
      solved: false,
      artList: [
        {
          id: 1,
          artist: 'Paul Cézanne',
          name: 'La casa del ahorcado',
          style: 'Postimpresionismo',
          information: 'Su paleta se hará más luminosa, como vemos en La casa del ahorcado, mientras su pincelada cargada nos muestra ese interés escultórico que el pintor trata de transmitir a su obra. Este será el inicio de su lucha por el equilibrio entre lo visual y lo táctil de la representación pictórica.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/La_Maison_du_pendu%2C_Auvers-sur-Oise%2C_par_Paul_C%C3%A9zanne%2C_Yorck.jpg/1200px-La_Maison_du_pendu%2C_Auvers-sur-Oise%2C_par_Paul_C%C3%A9zanne%2C_Yorck.jpg'
        },
        {
          id: 2,
          artist: 'Paul Cézanne',
          name: 'Naturaleza muerta',
          style: 'Postimpresionismo',
          information: 'Si nos fijamos, por ejemplo, en esta naturaleza muerta, observamos como las frutas no descansan una encima de otra, ni sobre la mesa, sino que más bien parecen superponerse sobre un plano invisible y vertical que las acerca al espectador. Podemos observar como los unifican, planos sino no que se se superponen, un ejemplo del nuevo lenguaje pictórico sobre Naturaleza muerta (1879-1880)',
          url: 'https://64.media.tumblr.com/8e834e10e9c4d09f8aa204a8c345ef9b/tumblr_ng6fjep6Ut1qfcut3o1_1280.jpg',
        },
        {
          id: 3,
          artist: 'Paul Cézanne',
          name: 'El jarrón azul',
          style: 'Postimpresionismo',
          information: 'la pincelada cargada que veíamos en el anterior, desaparece; las formas geométricas se ven con más detalle y la simplicidad de líneas es más marcada',
          url: 'https://i.pinimg.com/originals/ac/2b/9c/ac2b9c53d0f341a81ce10eb991ebbf22.jpg',
        },
        {
          id: 4,
          artist: 'Paul Cézanne',
          name: 'Grandes bañistas',
          style: 'Postimpresionismo',
          information: 'las formas geométricas se ven con más detalle y la simplicidad de líneas es más marcada, características todas ellas acentuadas en el grupo de mujeres geometrizadas que acaban de darse un baño. Esta pintura más geométrica, de líneas simplificadas, será la que tanto llame la atención de pintores como Braque, Picasso y Derain, que serán el germen del lenguaje cubista que veremos en el siguiente tema.',
          url: 'https://64.media.tumblr.com/c76dba94884d82da365c48886e08a6f0/tumblr_na722r1QLI1qfcut3o1_1280.jpg',
        },
      ]
    }
  },
  methods: {
    getRandomArt() {
      this.artList = this.artList.map(a => ({ sort: Math.random(), id: a })).sort((a, b) => a.sort - b.sort).map(a => a.id);
      this.artSelected = 0;
    },
    onNextCard() {
      this.solved = false;
      this.artSelected++;
    },
    solveArtCard() {
      this.solved = true;
    }
  }
}
</script>

<style scoped>
.title-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>
