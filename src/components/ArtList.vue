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
        {
          id: 5,
          artist: 'George Seurat',
          name: 'Los bañistas de Asnières',
          style: 'Neoimpresionismo',
          information: 'Las figuras presentan ese hieratismo propio de las obras clásicas, con perfiles marcados, coloreadas por medio de pequeños puntos de color. Mantiene el gusto del color impresionista, aunque su técnica le haga perder en luminosidad.',
          url: 'https://3.bp.blogspot.com/-YLvsHFrEbqE/Vyd--3BVxeI/AAAAAAAAAxw/zGo4TGQNEV41sk6m-4vf7i5xPrKfe6pYACLcB/s1600/Georges_Seurat_004.jpg',
        },
        {
          id: 6,
          artist: 'George Seurat',
          name: 'Una tarde de domingo en la isla de la Grande Jatte',
          style: 'Neoimpresionismo',
          information: 'Esta obra le llevó varios años de trabajo. Representa una escena cotidiana de la vida parisina, en la que podemos ver de nuevo el hieratismo y la factura puntillista. Cuando se expuso a la crítica se habló de rigidez y se comparó la obra con un teatro de marionetas, ya que las figuras parecen recortadas y pegadas sobre el escenario del paisaje.',
          url: 'https://educacion.ufm.edu/wp-content/uploads/2014/01/Georges_Seurat_031.jpg',
        },
        {
          id: 7,
          artist: 'George Seurat',
          name: 'La parade',
          style: 'Neoimpresionismo',
          information: 'Seurat también fue conocido por sus pinturas sobre el circo, en las que vemos las mismas características ya mencionadas y donde podemos descubrir ese carácter de pintura egipcia que comentamos al principio, como ocurre en La Parade. En esta obra vemos la quietud y la búsqueda de estabilidad que contrasta con el tema cotidiano, de ocio y entretenimiento, un tema movido, propio de la vida moderna, pero que el pintor trata de manera rígida, como si vieran la modernidad a través de ojos egipcios.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/d/d0/Seurat_parade00.jpg',
        },
        {
          id: 8,
          artist: 'Paul Gaugin',
          name: 'Visión después del sermón: Jacob luchando con el ángel',
          style: 'Neoimpresionismo',
          information: 'Émile Bernard le enseñó a Gauguin la técnica del Cloisonné, un antiguo procedimiento de hacer esmalte en la que finas tiras de metal separan los espacios de color. Tomando ideas de esta técnica, Gauguin desarrollará una pintura de colores planos delimitados por los contornos de las figuras aplicado en las obras de esta época. En esta obra vemos también otras de las características de la obra de Gauguin, la búsqueda del primitivismo y la representación de lo visionario. Esta obra representa a las bretonas al salir de la iglesia, después de escuchar el sermón sobre la lucha de Jacob y el ángel, que es lo que vemos en la escena superior derecha. Esta escena, representada sobre un rojo que nos aleja de considerarla una escena realista, nos lleva a reconocer la imagen que estas señoritas puedan estar recreando en su cabeza después de escuchar las palabras del pastor. Lo que representa Gauguin en esta obra no es lo que podemos ver con los ojos de la carne, sino con los del espíritu, es decir, lo que las bretonas identifican con la visión.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/La_vision_apr%C3%A8s_le_sermon_%28Paul_Gauguin%29.jpg/1200px-La_vision_apr%C3%A8s_le_sermon_%28Paul_Gauguin%29.jpg',
        },
        {
          id: 9,
          artist: 'Paul Gaugin',
          name: 'El Cristo amarillo',
          style: 'Neoimpresionismo',
          information: 'muestra ese gusto por llegar a representar de manera muy sencilla, primitiva, casi torpe. Vemos unas mujeres bretonas que supuestamente están al pie del calvario y que más bien es producto de su imaginación. Es una escena transformada, aparentemente real, pero que ocurre en la mente de las mujeres.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/3/35/Gauguin_Il_Cristo_giallo.jpg',
        },
        {
          id: 10,
          artist: 'Paul Gaugin',
          name: 'Mahana no atúa',
          style: 'Neoimpresionismo',
          information: 'Esta búsqueda por volver a lo ingenuo, retornar a lo que Gauguin consideraba más puro, lo primitivo, lo no infectado por Occidente, le llevó a realizar diferentes viajes por el continente americano. Residió en Panamá y Martinica, terminando sus días en las Islas Marquesas. Durante este período representó, sobre todo, el ritual, que respondía a ese interés que tenía por buscar lo visionario. Un buen ejemplo es la obra Mahana no atúa, representación de la danza de las mujeres ante Hina, ídolo maorí. Es la representación del Día del Dios de esta comunidad primitiva.',
          url: 'https://www.artehistoria.com/sites/default/files/styles/full_horizontal/public/imagenobra/GAM00334.jpg?itok=FfPyRIpS',
        },
        {
          id: 11,
          artist: 'Paul Gaugin',
          name: 'Cabeza de muchacha',
          style: 'Neoimpresionismo',
          information: 'Paul Gauguin intentó recuperar la talla reivindicándola como la manera tradicional y primitiva de la elaboración escultórica. Tamién aprendió la técnica de la cerámica',
          url: 'https://www.museothyssen.org/sites/default/files/styles/16x9_social_share/public/imagen/obras/CTB.DEC99.36_cabeza-muchacha.jpg?h=379b870d',
        },
        {
          id: 12,
          artist: 'Paul Sérusier',
          name: 'El talismán',
          style: 'Neoimpresionismo',
          information: 'Paul Gauguin influyó en la utilización de colores puros en pintores como Van Gogh o Paul Sérusier, que motivarán la formación de los Nabis (escuela de Pont Aven). Sérusier pintó esta obra gracias a las instrucciones de Gauguin, contestando a preguntas como ¿Cómo ve usted los árboles?. Esta sería la primera obra de los Nabis. Se aprecian los colores puros y el cloisonné. Este nuevo grupo es colorista y defensor de la representación de las emociones y las experiencias al margen de la figuración. Al igual que los simbolistas, tratan de representar su percepción interior de lo visible, trascender de lo puramente físico para traspasar la barrera de lo objetivo.',
          url: 'https://3minutosdearte.com/wp-content/uploads/2017/01/S%C3%A9rusier-el-talism%C3%A1n-1888.jpg',
        },
        {
          id: 13,
          artist: 'Vincent Van Gogh',
          name: 'Los comedores de patatas',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
            'En sus primeras obras ya se podrá apreciar la intensidad que le caracterizará toda su vida. Una pincelada intensa y un ambiente todavía tenebroso. Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.',
          url: 'https://www.reprodart.com/kunst/vincent_van_gogh/The_Potato_Eaters_van_gogh.jpg',
        },
        {
          id: 14,
          artist: 'Vincent Van Gogh',
          name: 'La Arlesiana. Retrato de Mme Ginoux',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
            'Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.' +
            'De 1886 a 1888 realizó numerosos retratos tratando de crear un nuevo género realizando una depuración expresiva para dotar a los modelos. En esta obra vemos a una mujer melancólica ensimismada en sus pensamientos.',
          url: 'https://c8.alamy.com/compes/m6jw3f/l-arlesienne-madame-ginoux-con-libros-van-gogh-vincent-willem-1888-m6jw3f.jpg',
        },
        {
          id: 15,
          artist: 'Vincent Van Gogh',
          name: 'La noche estrellada',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
          'Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.' +
          'Van Gogh se va encontrando a sí mismo trabajando con esa pincelada cargada de color, movida, violenta e impusiva vista en obras como Los Girasoles o en los paisajes de campo (introduciendo la figura simbólica de la muerte en forma de segador). A través de los colores introduce elementos simbólicos como el uso del naranja para representar el color del sol y la cosecha, o el azul celeste para su Noche Estrellada, representando la imagen de la muerte como el inicio luminoso de una nueva vida después de la muerte',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbm9jaGUtZXN0cmVsbGFkYS12YW4tZ29naC5qcGciLCJyZXNpemUsNjAwLDYwMCJdfQ.30yTvpSbWId_RW0lLazENwOF6e00OTc13bMoDRyoMxI.jpg',
        },
        
        
      ]
    }
  },
  methods: {
    getRandomArt() {
      this.solved = false;
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
