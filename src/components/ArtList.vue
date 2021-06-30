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
          name: 'La casa del ahorcado (1872-1873)',
          style: 'Postimpresionismo',
          information: 'Su paleta se hará más luminosa, como vemos en La casa del ahorcado, mientras su pincelada cargada nos muestra ese interés escultórico que el pintor trata de transmitir a su obra. Este será el inicio de su lucha por el equilibrio entre lo visual y lo táctil de la representación pictórica.\n' +
            'Su composición tiende al equilibrio donde las horizontales y verticales marcan los ejes de la obra. Aquí se aprecia como los dos troncos de los árboles marcan una línea vertical que corta la diagonal que genera el camino de tierra. Así estructura el espacio del lienzo.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/La_Maison_du_pendu%2C_Auvers-sur-Oise%2C_par_Paul_C%C3%A9zanne%2C_Yorck.jpg/1200px-La_Maison_du_pendu%2C_Auvers-sur-Oise%2C_par_Paul_C%C3%A9zanne%2C_Yorck.jpg'
        },
        {
          id: 2,
          artist: 'Paul Cézanne',
          name: 'Naturaleza muerta (1879-1880)',
          style: 'Postimpresionismo',
          information: 'Se nota la marca pesadade sus pinceladas paralelas. Si nos fijamos, por ejemplo, en esta naturaleza muerta, observamos como las frutas no descansan una encima de otra, ni sobre la mesa, sino que más bien parecen superponerse sobre un plano invisible y vertical que las acerca al espectador. Podemos observar como los unifican, planos sino no que se se superponen, un ejemplo del nuevo lenguaje pictórico sobre Naturaleza muerta. Cezanne trabaja con la forma y se aleja del sentimiento. Se centra más en la composición y el dibujo y no tanto en la mancha de color, dando importancia al volumen, contorno y forma.',
          url: 'https://64.media.tumblr.com/8e834e10e9c4d09f8aa204a8c345ef9b/tumblr_ng6fjep6Ut1qfcut3o1_1280.jpg',
        },
        {
          id: 3,
          artist: 'Paul Cézanne',
          name: 'El jarrón azul (1889-1890)',
          style: 'Postimpresionismo',
          information: 'la pincelada cargada que veíamos en el anterior, desaparece; las formas geométricas se ven con más detalle y la simplicidad de líneas es más marcada',
          url: 'https://i.pinimg.com/originals/ac/2b/9c/ac2b9c53d0f341a81ce10eb991ebbf22.jpg',
        },
        {
          id: 4,
          artist: 'Paul Cézanne',
          name: 'Grandes bañistas (1906)',
          style: 'Postimpresionismo',
          information: 'las formas geométricas se ven con más detalle y la simplicidad de líneas es más marcada, características todas ellas acentuadas en el grupo de mujeres geometrizadas que acaban de darse un baño. Esta pintura más geométrica, de líneas simplificadas, será la que tanto llame la atención de pintores como Braque, Picasso y Derain, que serán el germen del lenguaje cubista que veremos en el siguiente tema.',
          url: 'https://64.media.tumblr.com/c76dba94884d82da365c48886e08a6f0/tumblr_na722r1QLI1qfcut3o1_1280.jpg',
        },
        {
          id: 5,
          artist: 'George Seurat',
          name: 'Los bañistas de Asnières (1883-1884)',
          style: 'Neoimpresionismo',
          information: 'Las figuras presentan ese hieratismo propio de las obras clásicas, con perfiles marcados, coloreadas por medio de pequeños puntos de color. Mantiene el gusto del color impresionista, aunque su técnica le haga perder en luminosidad.',
          url: 'https://3.bp.blogspot.com/-YLvsHFrEbqE/Vyd--3BVxeI/AAAAAAAAAxw/zGo4TGQNEV41sk6m-4vf7i5xPrKfe6pYACLcB/s1600/Georges_Seurat_004.jpg',
        },
        {
          id: 6,
          artist: 'George Seurat',
          name: 'Una tarde de domingo en la isla de la Grande Jatte (1884-1886)',
          style: 'Neoimpresionismo',
          information: 'Esta obra le llevó varios años de trabajo. Representa una escena cotidiana de la vida parisina, en la que podemos ver de nuevo el hieratismo y la factura puntillista. Cuando se expuso a la crítica se habló de rigidez y se comparó la obra con un teatro de marionetas, ya que las figuras parecen recortadas y pegadas sobre el escenario del paisaje.',
          url: 'https://educacion.ufm.edu/wp-content/uploads/2014/01/Georges_Seurat_031.jpg',
        },
        {
          id: 7,
          artist: 'George Seurat',
          name: 'La parade (1889)',
          style: 'Neoimpresionismo',
          information: 'Seurat también fue conocido por sus pinturas sobre el circo, en las que vemos las mismas características ya mencionadas y donde podemos descubrir ese carácter de pintura egipcia que comentamos al principio, como ocurre en La Parade. En esta obra vemos la quietud y la búsqueda de estabilidad que contrasta con el tema cotidiano, de ocio y entretenimiento, un tema movido, propio de la vida moderna, pero que el pintor trata de manera rígida, como si vieran la modernidad a través de ojos egipcios.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/d/d0/Seurat_parade00.jpg',
        },
        {
          id: 8,
          artist: 'Paul Gaugin',
          name: 'Visión después del sermón: Jacob luchando con el ángel (1888)',
          style: 'Neoimpresionismo',
          information: 'Émile Bernard le enseñó a Gauguin la técnica del Cloisonné, un antiguo procedimiento de hacer esmalte en la que finas tiras de metal separan los espacios de color. Tomando ideas de esta técnica, Gauguin desarrollará una pintura de colores planos delimitados por los contornos de las figuras aplicado en las obras de esta época. En esta obra vemos también otras de las características de la obra de Gauguin, la búsqueda del primitivismo y la representación de lo visionario. Esta obra representa a las bretonas al salir de la iglesia, después de escuchar el sermón sobre la lucha de Jacob y el ángel, que es lo que vemos en la escena superior derecha. Esta escena, representada sobre un rojo que nos aleja de considerarla una escena realista, nos lleva a reconocer la imagen que estas señoritas puedan estar recreando en su cabeza después de escuchar las palabras del pastor. Lo que representa Gauguin en esta obra no es lo que podemos ver con los ojos de la carne, sino con los del espíritu, es decir, lo que las bretonas identifican con la visión.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/5/56/La_vision_apr%C3%A8s_le_sermon_%28Paul_Gauguin%29.jpg/1200px-La_vision_apr%C3%A8s_le_sermon_%28Paul_Gauguin%29.jpg',
        },
        {
          id: 9,
          artist: 'Paul Gaugin',
          name: 'El Cristo amarillo (1889)',
          style: 'Neoimpresionismo',
          information: 'muestra ese gusto por llegar a representar de manera muy sencilla, primitiva, casi torpe. Vemos unas mujeres bretonas que supuestamente están al pie del calvario y que más bien es producto de su imaginación. Es una escena transformada, aparentemente real, pero que ocurre en la mente de las mujeres.',
          url: 'https://upload.wikimedia.org/wikipedia/commons/3/35/Gauguin_Il_Cristo_giallo.jpg',
        },
        {
          id: 10,
          artist: 'Paul Gaugin',
          name: 'Mahana no atúa (1894)',
          style: 'Neoimpresionismo',
          information: 'Esta búsqueda por volver a lo ingenuo, retornar a lo que Gauguin consideraba más puro, lo primitivo, lo no infectado por Occidente, le llevó a realizar diferentes viajes por el continente americano. Residió en Panamá y Martinica, terminando sus días en las Islas Marquesas. Durante este período representó, sobre todo, el ritual, que respondía a ese interés que tenía por buscar lo visionario. Un buen ejemplo es la obra Mahana no atúa, representación de la danza de las mujeres ante Hina, ídolo maorí. Es la representación del Día del Dios de esta comunidad primitiva.',
          url: 'https://www.artehistoria.com/sites/default/files/styles/full_horizontal/public/imagenobra/GAM00334.jpg?itok=FfPyRIpS',
        },
        {
          id: 11,
          artist: 'Paul Gaugin',
          name: 'Cabeza de muchacha (1893-1894)',
          style: 'Neoimpresionismo',
          information: 'Paul Gauguin intentó recuperar la talla reivindicándola como la manera tradicional y primitiva de la elaboración escultórica. Tamién aprendió la técnica de la cerámica',
          url: 'https://www.museothyssen.org/sites/default/files/styles/16x9_social_share/public/imagen/obras/CTB.DEC99.36_cabeza-muchacha.jpg?h=379b870d',
        },
        {
          id: 12,
          artist: 'Paul Sérusier',
          name: 'El talismán (1888)',
          style: 'Neoimpresionismo',
          information: 'Paul Gauguin influyó en la utilización de colores puros en pintores como Van Gogh o Paul Sérusier, que motivarán la formación de los Nabis (escuela de Pont Aven). Sérusier pintó esta obra gracias a las instrucciones de Gauguin, contestando a preguntas como ¿Cómo ve usted los árboles?. Esta sería la primera obra de los Nabis. Se aprecian los colores puros y el cloisonné. Este nuevo grupo es colorista y defensor de la representación de las emociones y las experiencias al margen de la figuración. Al igual que los simbolistas, tratan de representar su percepción interior de lo visible, trascender de lo puramente físico para traspasar la barrera de lo objetivo.',
          url: 'https://3minutosdearte.com/wp-content/uploads/2017/01/S%C3%A9rusier-el-talism%C3%A1n-1888.jpg',
        },
        {
          id: 13,
          artist: 'Vincent Van Gogh',
          name: 'Los comedores de patatas (1885)',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
            'En sus primeras obras ya se podrá apreciar la intensidad que le caracterizará toda su vida. Una pincelada intensa y un ambiente todavía tenebroso. Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.',
          url: 'https://www.reprodart.com/kunst/vincent_van_gogh/The_Potato_Eaters_van_gogh.jpg',
        },
        {
          id: 14,
          artist: 'Vincent Van Gogh',
          name: 'La Arlesiana. Retrato de Mme Ginoux (1888)',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
            'Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.' +
            'De 1886 a 1888 realizó numerosos retratos tratando de crear un nuevo género realizando una depuración expresiva para dotar a los modelos. En esta obra vemos a una mujer melancólica ensimismada en sus pensamientos.',
          url: 'https://c8.alamy.com/compes/m6jw3f/l-arlesienne-madame-ginoux-con-libros-van-gogh-vincent-willem-1888-m6jw3f.jpg',
        },
        {
          id: 15,
          artist: 'Vincent Van Gogh',
          name: 'La noche estrellada (1889)',
          style: 'Neoimpresionismo',
          information: 'Van Gogh no comenzaría a pintar hasta finales del XIX. Fue representante del Postimpresionismo. Su intensa labor pictórica fue debida al apoyo a su hermano Theo y a la mujer de este, Johanna. Se instaló en Bélgica debido a su afán misionero como predicador' + 
          'Su pincelada larga nos recuerda a Cézanne, diferenciándose por la vivacidad con la que la aplica. Vincent pintaba deprisa y aplicando colores puros (recuerdo de la influencia de Gaugin, creando de auras de luz sutles y aplicando pinceladas de forma dinámica. Dibujaba con el color más que con las líneas.' +
          'Van Gogh se va encontrando a sí mismo trabajando con esa pincelada cargada de color, movida, violenta e impusiva vista en obras como Los Girasoles o en los paisajes de campo (introduciendo la figura simbólica de la muerte en forma de segador). A través de los colores introduce elementos simbólicos como el uso del naranja para representar el color del sol y la cosecha, o el azul celeste para su Noche Estrellada, representando la imagen de la muerte como el inicio luminoso de una nueva vida después de la muerte',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbm9jaGUtZXN0cmVsbGFkYS12YW4tZ29naC5qcGciLCJyZXNpemUsNjAwLDYwMCJdfQ.30yTvpSbWId_RW0lLazENwOF6e00OTc13bMoDRyoMxI.jpg',
        },
        {
          id: 16,
          artist: 'Gustave Moreau',
          name: 'La aparición (1876)',
          style: 'Simbolismo',
          information: 'Hacia finales del XIX surge un nuevo grupo revolucionario. Los simbolistas. Su origen radica en la literatura y toma como precursores a Puvis de Chavannes y a Gustave Moreau.  Obras decorativas (fiel al movimiento del Simbolismo). Se rescata la pintura mural con aire misticista'+
            'Gustave Moreau recrea ambientes exóticos y llenos de dramatismo. De fuerte inspiración de temática mitológica y religiosa.' +
            'En esta escena vemos a Salomé con la cabeza de Juan Bautista elevándose de forma misteriosa. Este tipo de obras inspirarán al grupo de los surrealistas' + 
            'Los simbolistas se preocupan por presentar las escenas tradicionales desde un punto de vista subjetivo, intentando representar el inconsciente. Esto responde a la idea principal del Manifiesto Simbolista de Jean Moréas que dice que no se deben fijar las ideas, sino simbolizarlas hasta tal punto que lleguen al espectador por líneas ocultas que emoconalmente te llevan a la idea original',
          url: 'https://tuiteartees.files.wordpress.com/2014/10/la-aparicion-de-gustave-moreau.jpg?w=736',
        },
        {
          id: 17,
          artist: 'Odilon Redon',
          name: 'Ojos cerrados (1890)',
          style: 'Simbolismo',
          information: 'Hacia finales del XIX surge un nuevo grupo revolucionario. Los simbolistas. Su origen radica en la literatura y toma como precursores a Puvis de Chavannes y a Gustave Moreau.  Obras decorativas (fiel al movimiento del Simbolismo). Se rescata la pintura mural con aire misticista'+
            'Los simbolistas se preocupan por presentar las escenas tradicionales desde un punto de vista subjetivo, intentando representar el inconsciente. Esto responde a la idea principal del Manifiesto Simbolista de Jean Moréas que dice que no se deben fijar las ideas, sino simbolizarlas hasta tal punto que lleguen al espectador por líneas ocultas que emoconalmente te llevan a la idea original' +
            'Las primeras obras de Odilon Redon fueron grabados, pudiéndose ver ya un gusto por lo misterioso. Al igual que Moreau se vio atraído por temas religiosos y mitológicos. A través de ellos trató de superar la apariencia física de lo representado, dando a su obra un aire inquietante.',
          url: 'https://64.media.tumblr.com/960c67ae4e6787e23935b07725619d68/tumblr_nhwql1l0BS1qfcut3o1_1280.jpg',
        },
        {
          id: 18,
          artist: 'Edvard Munch',
          name: 'El grito (1893)',
          style: 'Simbolismo/Expresionismo',
          information: 'Hacia finales del XIX surge un nuevo grupo revolucionario. Los simbolistas. Su origen radica en la literatura y toma como precursores a Puvis de Chavannes y a Gustave Moreau.  Obras decorativas (fiel al movimiento del Simbolismo). Se rescata la pintura mural con aire misticista'+
            'Edvard Munch representa un ejemplo de una obra unida a las experiencias de una vida. A los cunco años su madre muere de tuberculosis. Unos años después su hermana. Esto le llevo a desarrollar una obsesión por la muerte. En un viaje a París conoció las obras impresionistas empezando a desarrollar su pintura bajo esos cánones. Poco después, siguiendo los pasos de Gauguin, empezó a aplicar colores puros de manera libre siguiendo el interés del grupo simbolista, aplicando el color de forma simbólica, no naturalista.' +
            'En el grito se observa la fuerza expresiva a tavés de la estridencia de sus colores la sinuosidad de la línea. Representa la angustia, la tensión, el pánico de un hombre que a pesar de tener compañía se siente solo. Esa soledad y angustia que se ve en sus hombras son un reflejo a los sentimientos de propio Munch a lo largo de su vida. <= Esto nos adentra al Expresionismo',
          url: 'https://cdn.martiarte.com/1152-superlarge_default/el-grito-edvard-munch.jpg',
        },
        {
          id: 19,
          artist: 'Henri Matisse',
          name: 'Lujo, calma y voluptuosidad (1904-1905)',
          style: 'Fauvismo',
          information: 'El Fauvismo surgió de una explosición de principios del XX definida como Cage aux fauves (Caja de fieras).' +
            'Matisse se inició en el Neoimpresionismo siguiendo la obra de Seurat y su puntillismo, como se puede apreciar en esta obra. A diferencia de Seurat, las pretensiones puntillistas no eran las de representar la realidad, si no más bien simbólicas. En esta obra se aprecia, tal y como en la obra de Gauguin, cómo transmite las figuras femeninas como sacadas de la imaginación de un niño',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbWF0aXNzZS1sdXhlLmpwZyIsInJlc2l6ZSw4MDAiXX0.GPbsyuzR-hoEWZi1kcvRBZ2ZYIJ7ntdXlVrcBwiUYdU.jpg',
        },
        {
          id: 20,
          artist: 'Henri Matisse',
          name: 'La alegría de vivir (1905-1906)',
          style: 'Fauvismo',
          information: 'El Fauvismo surgió de una explosición de principios del XX definida como Cage aux fauves (Caja de fieras).' +
            'Tas sus comienzos puntillistas, Matisse presenta una evolución hacia el uso de manchas de color uniformes y el enfrentamiento de colores puros. Se formaliza el Fauvismo, fuertemente influenciado por la obra de Gauguin. Se caracterizaban por extender el color en grandes áreas dotando a la superficie de un caracter plano, pero usando grandes cantidades de color que producían un intenso deslumbramiento. Tratan de expresar sensaciones a través del color'+
            'La gran obra de MAtisse en este período es la Alegría de vivir. Una pintura de tono arcaico que representa una situación idílica. El cuadro recuerda a Gauguin y el clasicismo representativo de Cezanne. ',
          url: 'https://educacion.ufm.edu/wp-content/uploads/2017/02/Matisse-la-alegria-de-vivir.jpg',
        },
        {
          id: 21,
          artist: 'Henri Matisse',
          name: 'Armonía en rojo (1908)',
          style: 'Fauvismo',
          information: 'El Fauvismo surgió de una explosición de principios del XX definida como Cage aux fauves (Caja de fieras).' +
            'Tas sus comienzos puntillistas, Matisse presenta una evolución hacia el uso de manchas de color uniformes y el enfrentamiento de colores puros. Se formaliza el Fauvismo, fuertemente influenciado por la obra de Gauguin. Se caracterizaban por extender el color en grandes áreas dotando a la superficie de un caracter plano, pero usando grandes cantidades de color que producían un intenso deslumbramiento. Tratan de expresar sensaciones a través del color'+
            'En Armonía en rojo, se aprecia la evolución de la obra de Matisse hacia el uso del color de manera individual, de tal forma que un solo color predomine en el lienzo y cobre protagonismo. Esto dará una sensación de aplanamiento mucho mayor',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvNDgxMTE4ODc5MV83ZmJjMWJmOTExX28uanBnIiwicmVzaXplLDgwMCJdfQ.wsIDChkLYDPJGBPEjLfBWanDDBhwZL7K963bkRDkPuI.jpg',
        },
        {
          id: 22,
          artist: 'Henri Matisse',
          name: 'La danza (1909-1910)',
          style: 'Fauvismo',
          information: 'El Fauvismo surgió de una explosición de principios del XX definida como Cage aux fauves (Caja de fieras).' +
            'Tas sus comienzos puntillistas, Matisse presenta una evolución hacia el uso de manchas de color uniformes y el enfrentamiento de colores puros. Se formaliza el Fauvismo, fuertemente influenciado por la obra de Gauguin. Se caracterizaban por extender el color en grandes áreas dotando a la superficie de un caracter plano, pero usando grandes cantidades de color que producían un intenso deslumbramiento. Tratan de expresar sensaciones a través del color'+
            'El uso del color de Matisse evolucionó hasta el uso del mismo de manera individual, donde un color uniforme predominaba en la obra dándole una sensación mayor de aplanamiento. Para Matisse, la intensidad del color aumentaba en relación a la superficie coloreada, como vemos en esta obra. Esta obra representa a unas personas danzando sobre una colina verde de pinos bajo un cielo azul. Al usar estos colores, tuvo que usar bermellón para las figuras y así dotar a la obra de luz',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbWF0aXNzZS1kYW5jZS0xOTEwLmpwZyIsInJlc2l6ZSw4MDAiXX0.algQupJ4DIvcEXEX844h0yLi3sRIa_Sf9x5Zcjj8ei0.jpg',
        },
        {
          id: 23,
          artist: 'Pablo Picasso',
          name: 'Retrato de Gertrude Stein (1906)',
          style: '-',
          information: 'Los inicios de Pablo Picasso en el cubismo se empiezan a apreciar cuando su obra se vuelve escultórica.'+
            'Con el Retrato de Gertrude Stein, podemos reparar en el rostro de la modelo con cierta reminiscencia a una escultura. Más concretamente con la escultura íbera. Más tarde recibiría influencias también de las máscaras africanas',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvZ2VydHJ1ZGUtc3RlaW4tcGljYXNzby5qcGciLCJyZXNpemUsODAwIl19.E4gAOtJaMQsByyxhjrH9WUtVzh51K4aQUIUzng7J6f8.jpg',
        },
        {
          id: 24,
          artist: 'Pablo Picasso',
          name: 'Las señoritas de Aviñón (1907)',
          style: 'Proto-cubista',
          information: 'Esta obra de Picasso está considerada como la obra puente que le lleva al cubismo. En ella rompe claramente con la representación figurativa y opta por el uso del color de forma aleatoria.'+
            'Se observa un primitivismo sobre todo en tres de las figuras, cuyos rostros se asemejan a las máscaras Africanas. Se tratan de 5 mujeres prostitutas que devuelven la mirada al espectador y representa la fatalidad de la sexualidad femenina de la época. En realidad se trata de un recuerdo a un amigo que se quitó la vida por amor.',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbGVzLWRlbW9pc2VsbGVzLWQtYXZpZ25vbi5qcGciLCJyZXNpemUsNjAwLDYwMCJdfQ.jWC7c1SO5imjPpVjR7v_FsHA4w0jp2eix9Hf5_mkXJo.jpg',
        },
        {
          id: 25,
          artist: '-',
          name: '',
          style: 'Cubismo',
          information: 'Cezanne sería el primer pintor interesado en adentrarse en una nueva visión de la pintura donde la geometría sería la nueva gramática de este lenguaje. En una exposición que se realizó en París'+
            'sobre su obra donde se veía el uso de los volúmenes, donde asistió Pablo Picasso. Su pincelada geométrica y su alejamiento de la perspectiva renacentista sembraron en Picasso una semilla del Cubismo.' +
            'Los iniciadores de este movimiento fueron Pablo Picasso y George Braque, desarrollando un nuevo lenguaje pictórico alejado de la perspectiva canónica y usando unas composiciones en las que ' +
            'la yuxtaposición de planos y líneas cambian la forma de mirar del espectador. Ante estos cuadros, el espectador debe reconstruir las imágenes. La perspectiva múltiple rompe la apariencia tradicional' +
            'de los objetos, ahora representados descompuestos desde todos sus puntos de vista en el mismo lienzo. Con ello se realiza una ruptura del espacio tridimensonal de la pintura, haciendo desaparecer' +
            'la relación formal con los modelos pintados. También se realiza un alejamiento del color y la luz, dando protagonismo a los planos y las líneas.\n' +
            '' +
            '  CUBISMO ANALÍTICO:\n' +
            '    Es el cubismo inicial. Aquel en que se busca la descomposición cientifista de los planos en diferentes perspectivas. Con el paso del tiempo, los artistas comienzan a multiplicar las perspectivasm haciendo que las obras' +
            '    Adquieran una difícil comprensión gracias a su grado de abstracción. En esta primera etapa los colores son escasos, predominando los pardos, grises y marrones.\n' +
            '  CUBISMO SINTÉTICO:\n' +
            '    En esta segunda etapa, la descomposición de los planos no será de forma científica, si no más libre. El autor realiza una deconstrucción de los objetos en los planos que el propio autor considera más importantes.' +
            '    Será característico la utilización del collage introduciendo elementos de la vida cotidiana como el papel y las telas. El Cubismo busca destacar la cualidad de objeto del cuadro. Los cuadros no son representaciones de la realidad' +
            '    sino que en si mismos son objetos. En esta etapa vuelven a aparecer los colores',
          url: '',
          title: 'Cubismo'
        },
        {
          id: 26,
          artist: 'George Braque',
          name: 'Puerto de Normandía (1909)',
          style: 'Cubismo (analítico?)',
          information: 'George Braque comenzó bajo los ideales del Fauvismo hasta que admiró Las señoritas de Aviñón de Picasso que hizo evolucionar su estilo hasta el cubismo como se ve en su obra Desnudo.\n' +
            'A partir de entonces comenzará a trabajar con paisajes sobre todo, descomponiéndolos en formas geométricas como se aprecia en esta obra de Puerto de Normandía. Los planos se superponen unos a otros haciendo que unos se acerquen al espectador mientras que otros se alejen permitiendo al espectador sentirse cercano a la obra.\n' +
            'Picasso y Braque decidieron trabajar juntos para desarrollar el nuevo estilo. La obra de Picasso tiende a ser más lineal, con dibujos angulares, mientras que Braque es más amable con las líneas más suaves. Decidieron que debian evitar el uso del color ya que distraía y dificultaba el interés por marcar los espacios superpuestos (Cubismo analítico)\n' +
            'Ambos optaron por la abtracción hasta que dieron un giro y volvieron al interés por lo real del objeto. Braque empezó a experimentar con las texturas incluyendo elementos naturales como tierra. Picasso ',
          url: 'http://pinturas.arteygalerias.com/georges_braque/galeria_obras_pinturas/georges_braque_puerto_normandia.jpg',
        },
        {
          id: 27,
          artist: 'Pablo Picasso',
          name: 'El Guernica',
          style: 'Cubismo',
          information: 'Pablo Picasso descomponía la realidad en planos y líneas superpuestos. En este caso la forma de mirar del espectador cambia, obligándole a ir más allá del cuadro y adentrarse en los planos que nos presenta el autor.\n' +
            'Picasso se deshace de los colores para acentuar aún mas los planos y para evitar distraer al espectador de la intención de la obra\n' +
            'Esta obra es un intento de despertar de la pbolación española un sentimiento de rechazo contra los totalitarismos de Europa, hacia el dolor y la destrucción de la guerra.\n' +
            'El guernica presenta una composición estudiada y equilibrada. Las figuras verticales de las mujeres enmarcan el cuadro cerrando la composición triangular cuyo vértice superior está coronado por la cabeza de caballo. Vemos figuras que Picasso ya había usado en obras anteriores. La presencia de la mujer gritando que representa el dolor, la muerte y la pérdida que provoca la guerra. El toro representa la fuerza animal y brutal descontrolada del ser humano. El caballo grita representando el triunfo de la muerte y sobre él incide la luz de la razón',
          url: 'https://dam.ngenespanol.com/wp-content/uploads/2019/10/Guernica-7.jpg',
        },
        {
          id: 28,
          artist: 'Juan Gris',
          name: 'Naturaleza muerta ante una ventana: Place Ravignan (1915)',
          style: 'Cubismo (analítico)',
          information: 'Juan Gris aprendió de Picasso no solo el lenguaje  cubista si no el proceso por el que se llega a ello. De personalidad más técnica y científica, su lenguaje no es tan libremente creativo. Tenderá al cubismo analítico.' +
            'Juan Gris no descartó el uso del color ni la combinación de la perspectiva múltiple como la tradicional',
          url: 'https://www.artehistoria.com/sites/default/files/styles/full_horizontal/public/imagenobra/JUN17036.jpg?itok=1_LW9m4r',
        },
        {
          id: 29,
          artist: 'Juan Gris',
          name: 'Arlequín con guitarra (1917)',
          style: 'Cubismo analítico',
          information: 'Juan Gris aprendió de Picasso no solo el lenguaje  cubista si no el proceso por el que se llega a ello. De personalidad más técnica y científica, su lenguaje no es tan libremente creativo. Tenderá al cubismo analítico.' +
            'Juan Gris no descartó el uso del color ni la combinación de la perspectiva múltiple como la tradicional.\n' +
            'En esta obra se aprecia la evolución que siguió también Picasso a una pintura más sensual con más libertad creativa y colorido.',
          url: 'https://www.artehistoria.com/sites/default/files/styles/full_horizontal/public/imagenobra/JUA12313.jpg?itok=BqP6CnZ4',
        },
        {
          id: 30,
          artist: 'Fernand Léger',
          name: 'Los fumadores (1911-1912)',
          style: 'Cubismo',
          information: 'Fernand Léger conocío a Braque y Picasso siguiendo sus pasos pero con un caracter más técnico que estético. Introdujo elementos geométricos en su obra hasta llegar a la abstracción. Y es a través de esa abstracción donde experimentó cómo transmitir la sensación de movilidad y velocidad de la vida moderna e industrial'+
            '',
          url: 'https://lh3.googleusercontent.com/proxy/w3tHAXRJ7yGl-AohwEpzLFxq-2Lvh3fN7FfEUJW6LLc9jJoHFFiNsYuVwufc73o-LAJqWDBfuk9OqcAcPDvMaLJ_G9axAiKgUp4',
        },
        {
          id: 31,
          artist: 'Fernand Léger',
          name: 'La escalera (1914)',
          style: 'Cubismo',
          information: 'Fernand Léger conocío a Braque y Picasso siguiendo sus pasos pero con un caracter más técnico que estético. Introdujo elementos geométricos en su obra hasta llegar a la abstracción. Y es a través de esa abstracción donde experimentó cómo transmitir la sensación de movilidad y velocidad de la vida moderna e industrial'+
            '',
          url: 'https://www.biodiversidadvirtual.org/etno/data/media/1241/Cuadro-La-escalera-(Segundo-estado)-Madrid-58867.jpg',
        },
        {
          id: 32,
          artist: 'Robert Delaunay',
          name: 'Torre Eiffel (1911)',
          style: 'Cubismo',
          information: 'Delaunay conoció también a Braque y Picasso y aunque no estaba interesado en la representación de la realidad a través de las formas geométricas y la superposición de planos, sí aprovechó el lenguaje cubista para desarrollar su propia personalidad pictórica' +
            'Delaunay trabajó la creación de formas geométricas a través del color con la intención de transmitir sensación de movimiento y evitar la apariencia de cualquier perspectiva. De esta forma, los espacios coloreados ofrecen otra sensación de espacio más dramático al espectador',
          url: 'https://cms.guggenheim-bilbao.eus/uploads/2014/07/Torre-Eiffel_Delaunay_300x443.jpg',
        },
        {
          id: 33,
          artist: 'Pablo Picasso',
          name: 'Cabeza de Fernande Olivier (1909)',
          style: 'Cubismo Escultórico',
          information: 'Esta obra corresponde al interés por la figura humana de la primera etapa cubista de Picasso. Comparte características con el retrato de Gertrude Stein y las Señoritas de Avignon con sus rostros escultóricos, afrícanos, íberos...'+
            '',
          url: 'http://www.bcn.cat/museupicasso/assets/content/works/Fernande-Olivier_057-Head-of-a-woman-(Fernande)-1909.jpg',
        },
        {
          id: 34,
          artist: 'Julio González',
          name: 'Máscara Acerada (1929-1930)',
          style: 'Cubismo Escultorico',
          information: 'Julio González fue un pionero en el uso del hierro para esculturas. Conoció a Picasso y su obra ejerció gran influiencia sobre él. En su obra usa un único plano simplificando su propio lenguaje (antes superponía dos planos de chapa). Aeste plano de chapa le aplica modificaciones que originan el rostro'+
            '',
          url: 'https://static5.museoreinasofia.es/sites/default/files/obras/AS03091.jpg',
        },
        {
          id: 35,
          artist: 'Julio González',
          name: 'Mujer sentada (1935)',
          style: 'Cubismo Escultorico',
          information: 'Julio González fue un pionero en el uso del hierro para esculturas. Conoció a Picasso y su obra ejerció gran influiencia sobre él. En su obra usa un único plano simplificando su propio lenguaje (antes superponía dos planos de chapa). Aeste plano de chapa le aplica modificaciones que originan el rostro' +
            'Gracias a su amistad con Picasso, Julio adpotará el lenguaje surrealista. Su escultura pasará a ser más lineal, basada en elementos alargados construyendo figuras simplificadas acercándose al imaginario surrealista de la mantis religiosa como símil de la mujer.',
          url: 'https://static4.museoreinasofia.es/sites/default/files/obras/AS10757.jpg',
        },
        {
          id: 37,
          artist: 'Pablo Gargallo',
          name: 'Gran Profeta (1933)',
          style: 'Cubismo Escultórico',
          information: 'Pablo Gargallo demostró su pasión por la escultura desde bien pequeño. Comenzó influenciado por el Art Nouveau. Tras conocer al grupo cubista, empieza a desarrollar su propio lenguaje escultórico basándose en la tradición del metal español\n' +
            'Comenzó a realizar finas máscaras de hierro y cobre que conseguían transmitir volumen jugando con la contraposición de las superficies cóncavas y convexas.',
          url: 'http://3.bp.blogspot.com/-Qf_-6LExYE8/UcftHhyl-lI/AAAAAAAAaSw/EMGYZJpUOpA/s1600/el+Profeta.jpg',
        },
        {
          id: 38,
          artist: 'Jaques Lipchitz',
          name: 'Marinero con guitarra (1917)',
          style: 'Cubismo escultórico sintético',
          information: 'El autor lituano adoptó el lenguaje cubista y empezó a realizar escuturas para representar en 3D las obras de Braque y Picasso. Empezó a estilizar las figuras terminando en un cubismo sintético' +
            '',
          url: 'https://static4.museoreinasofia.es/sites/default/files/obras/AD00516.jpg',
        },
                {
          id: 39,
          artist: 'Alexander Archipenko (1914)',
          name: 'Mujer peinándose',
          style: 'Cubismo escultórico',
          information: 'El autor ukraniano analiza la figura humana descompuesta en figuras geométricas utilizando el contraste entre la forma cóncava y convexa. Entre lo sólido y lo hueco. Trabajó la escultura policromada y la escultura móvil' +
            '',
          url: '',
        },
        {
          id: 40,
          artist: '-',
          name: 'Futurismo',
          style: '',
          information: 'En italia se juntaron un grupo de artistas preocupados por reaccionar ante la tradición y desarrollar un nuevo lenguaje para definir la nueva belleza: la belleza de la velocidad. Se trataba de un movimiento artístico y social debido a la gran cantidad de manifiestos ue firmaron.\n' +
            'En la obra de sus artistas podemos ver la herencia de estéticas de otros movimientos como el Puntillismo de Seurat o el Cubismo. Las pinceladas puntillistas se alargan y los facetados del cubismo se muestran más elásticos. El coche será el objeto fetiche a representar en sus obras.\n' +
            'Es habitual también enontrarse secuencias de la misma figura. La influencia de los estudios fotográficos ayudó a los pintores futuristas a crear dichas secuencias de imágenes para transmitir dinamismo. El líder teórico del movimiento ue Marinetti.\n' +
            'El futurismo desarrolló una estética ecléctica tomando elementos de movimientos anteriores. Aunque realmente introdujo una verdadera revolución en la temática y exaltación del dinamismo',
          url: '',
          title: 'Futurismo'
        },
        {
          id: 41,
          artist: 'Giancomo Balla',
          name: 'Dinamismo de un perro con correa (1912)',
          style: 'Futurismo',
          information: 'La imagen muestra un perro corriendo donde se presentan unas patas difuminadas dando la sensación de que está corriendo.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvZHluYW1pc20uanBnIiwicmVzaXplLDgwMCJdfQ.H3GB6WjgSvmaNxkkrxgPcAvj4Oo7AIue8tTpUDWZ5RA.jpg',
        },
        {
          id: 42,
          artist: 'Gino Severini',
          name: 'Expansión de la luz (Centrífuga y Centrípeta) (1912)',
          style: 'Futurismo',
          information: 'Su obra se caracteriza por el interés del pintor de unir imágenes tomadas de diferentes momentos. Es decir, crear secuencias de movimiento en las que se unen varias situaciones.' +
            'En un primer momento en su obra se distinguen elementos figurativos, pero su evolución se fue hacla la abstracción. Fue un referente en Italia',
          url: 'https://www.museothyssen.org/sites/default/files/styles/width_600/public/imagen/obras/1981.53_expansion-luz-centrifuga-centripeta.jpg',
        },
        {
          id: 43,
          artist: 'Umberto Boccioni',
          name: 'Formas únicas de continuidad en el espacio (1913)',
          style: 'Escultura Futurista',
          information: 'Pintor y escultor italiano de gran importancia en el movimiento futurista. Su pintura muestra ese carácter ecléctico del futurismo que toma tanto del Postimpresionismo como del Cubismo donde lo importante es transmitir la velocidad\n' +
            'Donde fue innovador fue en la aportación escultórica. La escultura futurista abog por una ruptura con la tradición, no solo figurativa, si no también de los materiales hasta ahora utilizados; el clásico mármol y bronce deben cambiarse por cartón, cuero, cemento, luz eléctrica, etc\n' +
            'Esta obra está realizada en barro y yeso fundida posteriormente en bronce tras la muerte del artista. En ella vemos esa pérdida figurativa y esa sensación de planos en movimiento',
          url: 'https://collectionapi.metmuseum.org/api/collection/v1/iiif/485540/1005475/main-image',
        },
        {
          id: 44,
          artist: '-',
          name: 'Expresionismo',
          style: '',
          information: 'Los expresionistas anuncian el final al que se verá abogado el ser humano por el positivismo que habita. Ese final será la primera Guerra Mundial. Su estética se aleja de intereses anteriores; no trata de mostrar el aspecto exterior de los impresionistas, postimpresionistas y cubistas, sino que buscan en adentrarse en el interior del ser humano para transmitir su angustia y su esperanza de vivir. Se trata de una diferencia temática más que técnica con sus predecesores \n' +
            'Existen tres generaciones de expresionistas:\n'+
            '- Los que comienzan en 1900 coincidiendo con el simbolismo\n' +
            '- A partir de 1905 con la aparición de Die Brücke y Der Blaue Reiter, coincidiendo con el Fauvismo y el Cubismo analítico:\n' +
            ' - Die Brücke (el puente): Sus artistas persiguen un objetivo común: reformar las reglas de creación artística rechazando lo tradicional para dar paso a la libertad de expresión personal. No comparten una estética común; les une su actitud hacia la libertad. Esto les lleva hacia un primitivismo manifestado por el uso de la xilografía. que se transforma en obras pictóricas con líneas muy marcadas y espacios de color plano representando el carácter primmitivo del interior del ser humano, su carácter animal. En un principio la temática fue de paisajes y naturaleza, pero evolucionaron hasta escenas callejeras y ambientes urbanos.\n' +
            ' - Der Blaue Reiter (el jinete azul): Fundado por Kandinsky y Marc. Al igual que Die Brükce, se interesa por representar el mundo interior. Pero a diferencia de sus predecesores no buscan la estética primitiva ni lo instintivo del ser humano, sino la representación de un mundo más espiritual. Dejan de lado poco a poco lo figurativo para representar el espíritu por medio de la abstracción\n' +
            '- La última etapa que será la que surja tras la Primera Guerra mundial\n',
          url: '',
          title: 'Expresionismo'
        },
        {
          id: 45,
          artist: 'James Ensor',
          name: 'La entrada de Cristo en Bruselas (1888)',
          style: 'Expresionismo',
          information: 'Al igual que Munch, tiene un gusto por el colorido de los Impresionistas, aunque sus colores son más estridentes. Este uso del color combinado con la fuerza agresiva de su pincelada, aúnan con los temas provocativos, inspiradoras para el posterior grupo Surrealista.' +
            '',
          url: 'https://64.media.tumblr.com/ec277565f6f8d98dfae99623f0a307ca/tumblr_oo52ybL9c61qfcut3o1_1280.jpg',
        },
        {
          id: 46,
          artist: 'Ernst Kirchner',
          name: 'Escena callejera en Berlín (1913)',
          style: 'Expresionismo (Die Brucke)',
          information: 'Sus artistas persiguen un objetivo común: reformar las reglas de creación artística rechazando lo tradicional para dar paso a la libertad de expresión personal. No comparten una estética común; les une su actitud hacia la libertad. Esto les lleva hacia un primitivismo manifestado por el uso de la xilografía. que se transforma en obras pictóricas con líneas muy marcadas y espacios de color plano representando el carácter primmitivo del interior del ser humano, su carácter animal. En un principio la temática fue de paisajes y naturaleza, pero evolucionaron hasta escenas callejeras y ambientes urbanos.' +
            '',
          url: 'http://2.bp.blogspot.com/-fFxLZ7XSpfw/T_QcZ-aBpRI/AAAAAAAA_0w/dAsn_L52np0/s640/Kirchner+-+Berlin+Street+Scene+-1913+-+Neue+Galerie,+Nueva+York.jpg',
        },
        {
          id: 47,
          artist: 'Wassily Kandinsky',
          name: 'Houses in Murnau on Obermarkt (1908)',
          style: 'Expresionista (Der Blaue Reiter)',
          information: 'Der Blaue Reiter (el jinete azul): Fundado por Kandinsky y Marc. Al igual que Die Brükce, se interesa por representar el mundo interior. Pero a diferencia de sus predecesores no buscan la estética primitiva ni lo instintivo del ser humano, sino la representación de un mundo más espiritual. Dejan de lado poco a poco lo figurativo para representar el espíritu por medio de la abstracción\n' +
            '',
          url: 'https://www.wassilykandinsky.net/images/works/86.jpg',
        },
        {
          id: 48,
          artist: 'Franz Marc',
          name: 'La vaca amarilla (1911)',
          style: 'Expresionista (Der Blaue Reiter)',
          information: 'Der Blaue Reiter (el jinete azul): Fundado por Kandinsky y Marc. Al igual que Die Brükce, se interesa por representar el mundo interior. Pero a diferencia de sus predecesores no buscan la estética primitiva ni lo instintivo del ser humano, sino la representación de un mundo más espiritual. Dejan de lado poco a poco lo figurativo para representar el espíritu por medio de la abstracción\n' +
            '',
          url: 'https://www.wassilykandinsky.net/images/works/86.jpg',
        },
        {
          id: 49,
          artist: 'Emil Nolde',
          name: 'Danza alrededor del becerro de oro',
          style: 'Expresionismo (última etapa)',
          information: 'Emil Nolde desarrolla una pintura de puro predominio del uso agresivo del color. Se aprecia un trazo expresivo y primitivo influenciado por el uso de la litografía' +
            '',
          url: 'https://i.pinimg.com/originals/9e/74/28/9e74282a2f2e61d8c81deb282010cd21.jpg',
        },
        {
          id: 50,
          artist: 'Oskar Kokoschka',
          name: 'La novia del viento (1914)',
          style: 'Expresionismo (última etapa)',
          information: 'Uso de las pinceladas enérgicas. Muestra su relación con Alma Mahler' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwva29rb3NjaGthLXZpZW50by5qcGciLCJyZXNpemUsMjAwMCwyMDAwIl19.wq3EXV2fUU60B8wjdjERorRFY20unjWjIcr6-N_2BtQ.jpg',
        },
        {
          id: 52,
          artist: 'Chaim Soutine',
          name: 'El conejo despellejado',
          style: 'Expresionismo (última etapa)',
          information: 'Comenzó pintando paisajes pero acabo mostrando interés por las naturalezas muertas. Más concretamente por las figuras de animales desollados que provocan al espectador rechazo' +
            '',
          url: 'https://imagenes.elpais.com/resizer/oyircRHMV9OdERs8gmApthsnHas=/414x0/arc-anglerfish-eu-central-1-prod-prisa.s3.amazonaws.com/public/OGX5MXO35OSXSYHICTIVACEWBM.jpg',
        },
        {
          id: 53,
          artist: '-',
          name: 'Neoimpresionismo',
          style: '',
          information: 'Fue fundado por George Seurat. Su formación como dibujante le llevara a desarrollar composiciones donde prima la estabilidad, el equilibrio de contención de las formas y las figuras estáticas. Siguiendo los pasos de Cezanne, se alejaba de la espontaneidad impresionista trabajand con una pincelada controlada.\n' +
            'Al contrario que Cezanne, no se caracterizaba por las pinceladas paralelas, si no que desarrolla el divisionismo, con el que representaba formas por medio de pequeños puntos de color con el que el pintor intentaba crear una mezcla óptica de pigmentos en la retina del espectador (puntillismo)',
          url: '',
          title: 'Neoimpresionismo'
        },
        {
          id: 54,
          artist: '-',
          name: 'Simbolismo',
          style: '',
          information: 'Movimiento revolucionario de finals del XIX cuyo origen se encuentra en la literatura. Sus obras se caracterizan por ser muy decorativas. Búsqueda de representar las escenas tradicionales desde un punto de vista subjetivo, como tratando de representar el inconsciente. Tratan de no fijar las ideas de forma directa, si no de simbolizarlas de tal forma que llegue al espectador a través de líneas ocultas.' +
            '',
          url: '',
          title: 'Simbolismo'
        },
        {
          id: 55,
          artist: '-',
          name: 'Fauvismo',
          style: '',
          information: 'El Fauvismo está formado por un grupo de pintores que han pasado por una etapa Neoimpresionista, influenciados por la obra de Gauguin. Encabezados por Henry Matisse. Este se inició bajo el ala Neoimpresionista de la mano de George Seurat y su puntillismo Se busca el simbolismo más que el realismo\n' +
            'Se caracterizan pr extender el color en grandes áreas que dotaban a la superficie de un color plano. A diferencia de Gauguin, aplicaban grandes cantidades de color. Buscan expresar sensaciones a través del color, no representar impresiones',
          url: '',
          title: 'Fauvismo'
        },
        {
          id: 56,
          artist: '-',
          name: 'Abstracción',
          style: '',
          information: '' +
            '',
          url: '',
        },
        {
          id: 57,
          artist: 'Wassily Kandinsky',
          name: 'Improvisación 9 (1910)',
          style: 'Abstracción',
          information: 'Wassily Kandinsy fue uno de los impulsores del grupo expresionista Der Blaue Reiter. A este autor le gustaba el uso del color frente a la línea, llevándole a la abstracción. Este cambo se inición cuando por casualidad, vio una de sus obras boca abajo. Al ver que no tenía ningún sentido desde esa perspectiva, se dio cuenta de las posibilidades que tenía la pintura abstracta' +
            '',
          url: 'https://reproarte.com/images/stories/virtuemart/product/kandinsky_wassily/improvisation_9.jpg',
        },
        {
          id: 58,
          artist: 'Wassily Kandinsky',
          name: 'Composition VIII (1923)',
          style: 'Abstracción',
          information: 'Tras colaborar en la revolución Rusa y pasar como profesor en la Bauhaus, Kandinsky adquirió un nuevo conocimiento, cambiando su estética hacia líneas más geométricas' +
            '',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/ad/Wassily_Kandinsky_Composition_VIII.jpg/1280px-Wassily_Kandinsky_Composition_VIII.jpg',
        },
        {
          id: 59,
          artist: 'Robert Delaunay',
          name: 'Ventana (1912)',
          style: 'Abstracción',
          information: 'Siguiendo la huella del neoimpresionismo y del Fauvismo, Delaunay desarrollará la pintura del color. Creó lo que se denomina "Cubismo Órfico" que suponía la aportación de elementos cromáticos a las composiciones de base cubista (como un facetado de cristales). Así el autor irá evolucionando hacia la abstracción' +
            '',
          url: 'https://artsdot.com/ADC/Art-ImgScreen-1.nsf/O/A-8XYUQD/$FILE/Robert-delaunay-window.Jpg',
        },
        {
          id: 60,
          artist: 'Paul Klee',
          name: 'Polifonía (1932)',
          style: 'Abstracción',
          information: 'Klee contactó con el grupo de Der Blaue Reiter y siguiendo sus pasos se dirigió a la abstracción. Al igual que Delaunay, desarrollaría una pintura abstracta liminista donde deja entrever su interés y fornación en la música. Abstracción lírica.' +
            '',
          url: 'https://i0.wp.com/www.tomasbartolome.com/wp-content/uploads/2016/05/image23.jpg',
        },
        {
          id: 61,
          artist: 'Paul Klee',
          name: 'Casa Giratoria (1921)',
          style: 'Abstracción',
          information: 'Klee contactó con el grupo de Der Blaue Reiter y siguiendo sus pasos se dirigió a la abstracción. Al igual que Delaunay, desarrollaría una pintura abstracta liminista donde deja entrever su interés y fornación en la música. Abstracción lírica.' +
            '',
          url: 'https://uploads3.wikiart.org/images/paul-klee/revolving-house-1921(1).jpg',
        },
        {
          id: 62,
          artist: 'Piet Mondrian',
          name: 'Composición en rojo, amarillo y azul (1921)',
          style: 'Abstracción',
          information: 'Pasó de una pintura figurativa a una abstracta por medio del postimpresionismo y el Fauvismo. Empez´a completar sus lienzos sólo con figuras geométricas y colores puros (amarillo, azul, rojo, blanco y negro). Influenció al mundo arquitectónico y decorativo. De Stijl' +
            '',
          url: 'https://www.meisterdrucke.com/kunstwerke/500px/Piet_Mondrian_-_Composition_with_Red_Yellow_and_Blue_1921_-_(MeisterDrucke-406919).jpg',
        },
        {
          id: 63,
          artist: 'Kasimir Malevich',
          name: 'Cuadro negro sobre fondo blanco',
          style: 'Suprematismo (abstracción)',
          information: 'Influenciado por el Postimpresionismo, el Fauvismo y el Cubismo, desarrolló la pintura suprematista, que superó a la abstracción. El suprematismo lo inició Malevich y defendía la no representación,si no una abstracción que definía la relaidad al margen de los convencionalismos figurativos porque la realidad también se percibe desde la sensibilidad abstracta.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvZDE4N2QxOTFkMTgwZDBiZGQxOGJkMGI5X2QxODFkMTgzZDBiZmQxODBkMGI1ZDBiY2QwYjBkMTgyZDBiOGQxODdkMGI1ZDE4MWQwYmFkMGI4ZDBiOV9kMGJhZDB/iMmQwYjBkMGI0ZDE4MGQwYjBkMTgyLV8xOTE1LV9kMGIzZDE4MmQwYjMuanBnIiwicmVzaXplLDgwMCJdfQ.OzXc-V4Bust7Bhzhh7JCCU36rTPQsyLd_ZEkCv0puGA.jpg',
        },
        {
          id: 64,
          artist: 'Kasimir Malevich',
          name: 'Circulo negro',
          style: 'Suprematismo (abstracción)',
          information: 'Influenciado por el Postimpresionismo, el Fauvismo y el Cubismo, desarrolló la pintura suprematista, que superó a la abstracción. El suprematismo lo inició Malevich y defendía la no representación,si no una abstracción que definía la relaidad al margen de los convencionalismos figurativos porque la realidad también se percibe desde la sensibilidad abstracta.' +
            '',
          url: 'https://artsdot.com/ADC/Art.nsf/O/8DP8VE/$File/Kazimir_Severinovich_Malevich-Black_circle.JPG',
        },
        {
          id: 65,
          artist: '-',
          name: 'Dadaismo',
          style: '',
          information: 'Paralelamente se empezaron a crear dos grupos, uno en Suiza (Hugo Ball, Tristán Tzara, Hans Arp) y otro en Nueva York (Marcel Duschamp y Francis Picabia) con los mismos intereses.\n' +
            'El Dadaísmo fue un movimiento ideológico que buscaba a través de la provocación, despertar a una población a raíz de la Primera Guerra Mundial. Buscaban eliminar la obra maestra y que fuera la mirada del espectador la que fuese la creadora de la obra de arte.',
          url: '',
          title: 'dadaismo'
        },
        {
          id: 66,
          artist: 'Francis Picabia',
          name: 'Parada amorosa (1917)',
          style: 'Dadaísmo',
          information: 'Picabia fue un pintor ecléctico que comenzó en el impresionismo, después pasó al cubismo, llegó a la abstracción y volvió a la figuración. Sus obras se pueden apreciar una clara exaltación a la máquina y una referencia claramente sexual' +
            '',
          url: 'https://2.bp.blogspot.com/-Ca71xx7OuFI/WyzV_u1SzII/AAAAAAABQlk/mATD-n0267MduQZ8l7JdU1oDkTBuu7zgQCLcBGAs/s1600/Imagen029.jpg',
        },
        {
          id: 67,
          artist: 'Hans Arp',
          name: 'Torso y cabeza de flor (1924)',
          style: 'Dadaísmo',
          information: 'Hans Arp, fimdadpr del grupo dadaísta en Colonia, comenzó creando composiciones por medio de papeles y cartones que más tarde trasladaría a la pintura y a la escultura. Se trata de formas orgánicas, abstractas que van siempre acompañadas por títulos que denotan figuración. En este Torso con cabeza de flor, nos lleva a buscar el torso' +
            '',
          url: 'https://imagenes.elpais.com/resizer/vmpWzVVmz-hruGslXzIKMS2POVo=/414x0/arc-anglerfish-eu-central-1-prod-prisa.s3.amazonaws.com/public/A5G5KBCRHIRJDIKC7UI7RKGAAM.jpg',
        },
        {
          id: 68,
          artist: 'Marcel Duchamp',
          name: 'Desnudo bajando la escalera (1912)',
          style: 'Futurismo/Cubismo',
          information: 'Marcel Ducham se inicio en el Futurismo y Cubsmo.' +
            '',
          url: 'https://theartwolf.com/wp-content/uploads/2021/05/Marcel_Duchamp_-_Nude-descending-a-staircase-no2_-_1912_-_Oil_on_canvas_-_Philadelphia_Museum_of_Art.jpg',
        },
        {
          id: 69,
          artist: 'Marcel Duchamp',
          name: 'Fuente (1917)',
          style: 'Dadaísmo',
          information: 'Duchamp desarrolló lo que llamó ready-made. Se trata de objetos ya hechos de la vida cotidiana que adquieren un rango artístico al ser expuestos en galerías. No hay una búsquedaa de llamada de atención respecto a la belleza o a la estética de estos objetos, sino que descontextualizando su uso y su espacio introduciéndolos en galerías de arte, trataba de hacer considerar al espectador la gran cantidad de convenciones que hay, como la valoración de una obra como artística\n' +
            'Eso es lo que quiso representar con su "Fuente". Duchamp envió un urinario firmado por "R. Mutt" para ser expuesto en la exposición de la Sociedad de Artistas Independientes. Esta sociedad trató de crear un espacio expositivo en el que ninguna obra fuera rechazada. Cualquier objeto expuesto en una galería o museo es considerado arte sólo por ocupar un espacio en esa galería o museo',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbGEtZnVlbnRlLWR1Y2hhbXAuanBnIiwicmVzaXplLDgwMCJdfQ.rA5MRNPJ_4w8tLL0ydGqjcgOxqO3nAtCz_iLj7DXrHc.jpg',
        },
        {
          id: 70,
          artist: 'Marcel Duchamp',
          name: 'La novia puesta al desnudo por sus célibes, incluso (1915-1923)',
          style: 'Dadaísmo',
          information: 'Es la obra más ambiciosa de Duchamp. También conocida como el gran vidrio. Es una obra realizada sobre un espejo dividida en dos partes, la parte superior está dedicada a la mujer, mientras que la inferior representa el mundo del hombre. Juntos representan las tensiones del deseo amoroso como maquinarioa que nos mueve.' +
            '',
          url: '',
        },
        {
          id: 71,
          artist: 'Giorgio de Chirico',
          name: 'El enigma de un día (1914)',
          style: 'Realismo/Pintura Metafísica',
          information: 'Influenciado por los simbolistas llevó a desarrollar la pintura metafísica. Sus pinturas, de influencia Renacentista tratan de imágines arquitectónicas con un aire de misterio casi mágico que influirá en los pintores Surrealistas' +
            '',
          url: 'http://4.bp.blogspot.com/-Cy4w2e8B0eM/VPHNeY3md5I/AAAAAAAB4N8/O4-QFTxwJJQ/s1600/untitled.pngenigma.png',
        },
        {
          id: 72,
          artist: 'Giorgio de Chirico',
          name: 'Turing Spring (1914)',
          style: 'Realismo/Pintura Metafísica',
          information: 'Influenciado por los simbolistas llevó a desarrollar la pintura metafísica. Sus pinturas, de influencia Renacentista tratan de imágines arquitectónicas con un aire de misterio casi mágico que influirá en los pintores Surrealistas' +
            'Se denomina pintura metafísica porque nos hace reflexionar sobre quiénes somos, qué hacemos aquí y hacia dónde nos dirigimos. Tiene un tono onírico y de desolación',
          url: 'https://uploads7.wikiart.org/images/giorgio-de-chirico/turin-spring-1914.jpg!Large.jpg',
        },
        {
          id: 73,
          artist: '-',
          name: 'Surrealismo',
          style: '',
          information: 'El movimieto Dadá se disuelve tras las diferencias ente Tzara y André Bretón. Este último empezará a dar los pasos hacia el Surrealismo. Si el Dadaísmo supuso una ruptura, este movimiento quiere establecer un nuevo orden\n' +
            'Los artistas de este movimiento tienen un estilo común, el automatismo. Este automatismo surgió de la escritura como medio de llegar al pensamiento fuera de todo control de la razón y del dictamen moral y estético. Su intención es dejar fluir el subconsciente. Los pintores y escultores tratarán de acercarse a esta esfera del pensamiento a través del mundo de los sueños. También trabajó con la oscilación, el decollage y la decalcomanía.\n' +
            '',
          url: '',
          title: 'Surrealismo'
        },
        {
          id: 74,
          artist: 'Max Ernst',
          name: 'El jardín de Francia (1962)',
          style: 'Surrealismo',
          information: 'Comenzó en el Dadaísmo. Fue el inventor de una de las técnicas más automáticas del estilo, el frottage. Consistía en tomar el objeto que se quería representar, ponerlo debajo de una hoja y con un lapiz frotar el papel hasta conseguir la textura y la forma del objeto. Así se conseguía representar sin ningún tipo de condicionamiento racional o estético. Esa figura podía pasarse a una superficie en dos dimensiones o a una escultura.\n' +
            '',
          url: 'https://wahooart.com/Art.nsf/O/8XYK5D/$File/Max-Ernst-The-Garden-of-France.JPG',
        },
        {
          id: 75,
          artist: 'Max Ernst',
          name: 'Edipo Rey (1921)',
          style: 'Surrealismo',
          information: 'Comenzó en el Dadaísmo. Fue el inventor de una de las técnicas más automáticas del estilo, el frottage. Consistía en tomar el objeto que se quería representar, ponerlo debajo de una hoja y con un lapiz frotar el papel hasta conseguir la textura y la forma del objeto. Así se conseguía representar sin ningún tipo de condicionamiento racional o estético. Esa figura podía pasarse a una superficie en dos dimensiones o a una escultura.\n' +
            'Su obra nos recuerda a la de Dalí por la unión de elementos heterogéneos en una misma obra.',
          url: 'https://elcastillodekafka.files.wordpress.com/2012/10/max-ernst-edipo-rey-1921.jpg',
        },
        {
          id: 76,
          artist: 'Joan Miró',
          name: 'Carnaval de Arlequín (1924-1925)',
          style: 'Surrealismo',
          information: 'Aunque Joan Miró no formó parte del grupo surrealista, se interesó en transformar la pintora como lenguaje de pensamiento poético.\n' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbWlyYzNiM19jYXJuYXZhbC5qcGciLCJyZXNpemUsODAwIl19.Haxj8-9ZQWpf7JhwMdCsPB6OSxOvK_KmuXeOejoJjFc.jpg',
        },
        {
          id: 77,
          artist: 'Joan Miró',
          name: 'La mancha roja (1925)',
          style: 'Surrealismo',
          information: 'Aunque Joan Miró no formó parte del grupo surrealista, se interesó en transformar la pintora como lenguaje de pensamiento poético.\n' +
            'Evolucionó hasta simplificar las composiciones. Son las pinturas de sueño, donde no trabaja con el automatismo, sino que trabaja con dichas composiciones en su estudio y de forma consciente abandona toda relación espacial buscando la poesía pictórica.',
          url: 'https://i.pinimg.com/474x/6d/d3/03/6dd303e7b87808a98aa34b899e04a9b0.jpg',
        },
        {
          id: 78,
          artist: 'Joan Miró',
          name: 'Personaje delante del sol (1968)',
          style: 'Surrealismo',
          information: 'Aunque Joan Miró no formó parte del grupo surrealista, se interesó en transformar la pintora como lenguaje de pensamiento poético.\n' +
            'En sus últimas etapas desarrolló una pintura catalogada como dibujo infantil donde libera su imaginación para mostrarnos su lenguaje simbólico basado en su propia gramática creando diferentes símbolos.',
          url: 'https://visitmuseum.gencat.cat/media/cache/1140x684/uploads/objects/photos/56ab953852d29_personatge-davant-del-sol-joan-miro-1968.jpeg',
        },
        {
          id: 79,
          artist: 'Salvador Dalí',
          name: 'Rostro del gran masturbador (1929)',
          style: 'Surrealismo',
          information: 'Adoptó el lenguaje surrealista tras conocer el Postimpresionismo, el Cubismo y el Futurismo. En sus obras se aprecian una composición de elementos heterogéneos como Max Ernst junto con un ambiente propio de la obra de Chirico.' +
            'En esta obra representa su relación con su mujer. Podemos ver elementos variados como insectos, un autoretrato del pintor, la playa...',
          url: 'https://images-na.ssl-images-amazon.com/images/I/41UDak6CquL._AC_.jpg',
        },
        {
          id: 80,
          artist: 'Georgia O`Keeffe',
          name: 'Summer Days',
          style: 'Realismos/Precisionismo',
          information: 'Pintura figurativa muy precisa. También representa un mensaje metafísico. Paisaje con elementos reconocibles que acaba convirtiendose en una pared de trofeo. Colores que contrastan mucho. Busca transcender sobre nuestro paso sobre el mundo.' +
            '',
          url: 'https://www.georgiaokeeffe.net/images/paintings/summer-days.jpg',
        },
        {
          id: 81,
          artist: 'Salvador Dalí',
          name: 'La persistencia de la memoria (1931)',
          style: 'Surrealismo',
          information: 'Representación de un mundo onírico, del mundo de los sueños. Planteamiento paranóico-crítico. Es figurativo, las figuras son reconcibles pero las leyes de la física se saltan al ser un mundo onírico. Esta obra habla del tiempo con unos relojes licuados y otro del que salen hormigas. Podemos ver la piel varada del gran masturbador.\n' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbnljLTItMjY4LmpwZyIsInJlc2l6ZSw2MDAsNjAwIl19.d8RQGol_J1Zdb7_rISS5XuharJRmbii-BY7A0iZv5ck.jpg',
        },
        {
          id: 82,
          artist: 'Salvador Dalí',
          name: 'Cristo de San Juan de la Cruz (1951)',
          style: 'Surrealismo',
          information: 'A partir de la Segunda Guerra Mundial, Dalí empieza a tener una fama importante. En esta época introduce representaciones religiosas por esa búsqueda de lo intangible.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvNjAwNzMzN2ZkZjlmYi5qcGciLCJyZXNpemUsMjAwMCwyMDAwIl19.0o4gk4RPWr-VETkvQpYkOfqWr51k_sGmgFrj3Ny-vBo.jpg',
        },
        {
          id: 83,
          artist: 'René Magritte',
          name: 'La traición de las imágenes (1929)',
          style: 'Surrealismo',
          information: 'Magritte no dejaba rienda suelta al automatismo, si no que buscaba una pintura meditada. En esta obra trataba la pintura con una condición de artificio, de imitación de los objetos tridimensionales en las dos dimensiones.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbW9tYV9tYWdyaXR0ZV90cmVhY2hlcnlvZmltYWdlc18uanBnIiwicmVzaXplLDgwMCJdfQ.W3hb8VpjRH6knd1ItQydoUBCgoGcr_P2jD6uziZV47w.jpg',
        },
        {
          id: 84,
          artist: 'Oskar Schlemmer',
          name: 'Danzas en la Bauhaus (1927-1929)',
          style: 'Expresionismo',
          information: 'Concibe el teatro como una sintesis de tres elementos: el hombre en el espacio, la luz en movimiento y la arquitectura. En esta obra relacionan la arquitectura de Gropius con los trabajos de Klee y Kandisnky convirtiendo estas danzas una obra de arte total donde integran música, coreografía y vestuario.' +
            '',
          url: '',
        },
        {
          id: 85,
          artist: '-',
          name: 'Expresionismo Abstracto',
          style: '',
          information: 'Expresionismo abstracto puede considerarse una etiqueta para denominar el lenguaje de una serie de artistas de Nueva York tras la II Guerra Mundial. Este grupo de artistas de personalidades distintas defienden la libertad individual, la materialidad del cuadro como superficie y el carácter expresivo del arte\n' +
            'Con influencias del Surrealismo de Dalí y Ernst, del Cubismo europeo, de la pintura realista americana y la pintura mural de los artistas mexicanos. Se pueden distinguir dos corrientes:' +
            ' - Action Painting: Es una técnica pictórica que intent expresar movimiento, velocidad y energía a partir de la materia, el gesto o el color. El pintor se mueve y actúa en relación al soporte pictórico, salpicando con pintura la superficie de manera espontánea y enérgica (influencia del automatismo surrealista)\n' +
            ' - Color-Field: El color se convierte en un sujeto en sí mismo. Se trata de pintar o teñir grandes espacios de color liso y sólido creando así superficias lisas y uniformes. Evolucionará más tarde a la Abstracción Post-pictórica',
          url: '',
          title: 'Expresionismo Abstracto'
        },
        {
          id: 86,
          artist: 'Arshile Gorky',
          name: 'Garden in Sochi (1941)',
          style: 'Expresionismo Abstracto',
          information: 'Sus obras se centraron en vivencias personales a través de figuras biomorfas, distorsionadas y amenazantes que transmitía la angustia vital que padecía' +
            '',
          url: 'https://www.moma.org/media/W1siZiIsIjIwNDMyMCJdLFsicCIsImNvbnZlcnQiLCItcXVhbGl0eSA5MCAtcmVzaXplIDIwMDB4MjAwMFx1MDAzZSJdXQ.jpg?sha=bbaea9808bd5485f',
        },
        {
          id: 87,
          artist: 'William Baziotes',
          name: 'Dwarf (1947)',
          style: 'Expresionismo Abstracto',
          information: 'Su obra tiene más elementos surrealistas que abstractos con una pincelada que no es ni gestual ni expresionista. La representación de las formas morfológicas y biológicas suspendidas en el espacio pictórico las realiza sirviéndose del automatismo surrealista' +
            '',
          url: '',
        },
        {
          id: 88,
          artist: 'Hans Hoffmann',
          name: 'Art Like Love is Dedication (1965)',
          style: 'Expresionismo Abstracto',
          information: 'Profesor de entre otros, Pollock y Rothko. Sintetizó el color y la forma del Fauvismo y del Cubismo.' +
            '',
          url: 'https://uploads7.wikiart.org/images/hans-hofmann/art-like-love-is-dedication-1965.jpg!Large.jpg',
        },
        {
          id: 89,
          artist: 'Jackson Pollock',
          name: 'Convergence',
          style: 'Expresionismo Abstracto (Action Painting)',
          information: 'Representante del Action Painting. Desarrolló la técnica del Dripping que consistía en extender un lienzo sobre el suelo y moviéndose alrededor de él, dejaba caer gotas o chorros de pintura fluidas desde un recipiente con el fonde perforado. Así el acto de pintar se convertía en una actividad de todo el cuerpo.' +
            '',
          url: 'https://totenart.com/noticias/wp-content/uploads/2019/01/totenart-pollock-convergence.jpg',
        },
        {
          id: 90,
          artist: 'Willem de Kooning',
          name: 'Woman I (1952)',
          style: 'Expresionismo Abstracto (Action Painting)',
          information: 'En sus obras trabaja las abstracción, gestualidad y violencia con unas formas biomórficas que sugerían la figura humana. En esta obra se centra en la figura femenina con una pintura entre figurativa y gestual. Trabajaba alrededor del cuadro en constante movimiento con pinceladas cargadas de pntura y colores aplicados de forma salvaje' +
            '',
          url: 'http://2.bp.blogspot.com/-gJ64wb9DVIg/UXPR6vyTRdI/AAAAAAAAAvo/3za5h6qIyw0/s1600/MAIN_Woman,_I_1950_52.jpg',
        },
        {
          id: 91,
          artist: 'Franz Kline',
          name: 'Mahoning (1947)',
          style: 'Expresionismo Abstracto (Action Painting)',
          information: 'Es un pintor de acción cuya pincelada expresiva y violenta de color negro sobre fondo blanco le hicieron reconocible y reconocido. Antes de cada pintura realizaba muchos estudios y bocetos previos, su obra conservaba un carácter inmediato, dinámico y espontáneo' +
            '',
          url: 'https://whitneymedia.org/assets/artwork/1997/168639.jpeg',
        },
        {
          id: 92,
          artist: 'Robert Motherwell',
          name: 'Elegía a la República Española (1965)',
          style: 'Expresionismo Abstracto (Action Painting)',
          information: 'Se convirtió e ensayista del movmiento Expresionsta Abstracto. Su obra utiliza la pintura negra como elemento base diluyéndola con aguarrás para crear efecto de sombra. Especial importancia del acto físico de pintar sobre un lienzo de grandes dimensones que intenta superar los límites del marco.\n' +
            'Estudia la tradición dramática de la pintura española y su situación política',
          url: 'https://static4.museoreinasofia.es/sites/default/files/obras/AD01740.jpg',
        },
        {
          id: 93,
          artist: 'Clifford Still',
          name: 'Sin título (1964)',
          style: 'Expresionismo Abstracto (Color-Field)',
          information: 'Composición a base de grandes planos de color. Se interesó por la verticalidad en lienzos de grandes formatos teñidos por manchas de colores contrastados. Sustituyó los títulos por números para intentar no influenciar en las obras.' +
            '',
          url: 'https://cms.guggenheim-bilbao.eus/uploads/2012/05/Still_C_Sin-titulo-Untitled_1964-880x1024.jpg',
        },
        {
          id: 94,
          artist: 'Mark Rothko',
          name: '(sin título) (1955)',
          style: 'Expresionismo Abstracto (Color-Field)',
          information: 'Sus obras se tratan de pinturas de grandes dimensiones que presentan composiciones formadas por rectángulos de varios colores que se suceden paralelamente sobre lienzos verticales con bordes ligeramente irregulres en las zonas de separación entre colores. El color es el único protagonista y lleva al espectador que la contempla a una sensación de contemplación epiritual.\n' +
            'Su paleta de colores fue oscureciéndose con el paso de los años a medida que aumentaba su depresión.',
          url: 'https://mytaleiteachdotcom.files.wordpress.com/2013/02/rothko-obra.jpg',
        },
        {
          id: 95,
          artist: 'Barnett Newman',
          name: 'Onement I (1948)',
          style: 'Expresionismo Abstracto (Color-Field)',
          information: 'Sus cuadros están divididos en bandas verticales de color, de forma racional y sin contenido emocional. En sus composiciones, un campo de color puro y liso es atravesado por una o dos líneas finas verticales (zip) creando un efecto dramático y místico\n' +
            'El autor alcanzó su madured con este Onement I en el que se aprecia su línea vertical que se mantuvo como un rasgo de su obra.Exploró el impacto que causaba el enorme tamaño de sus cuadros superando el campo de visión del espectador.',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvMjdmODUyMjFhYWNmMzI2ODUzYWE2YmVjNzI2Njc1NWIuanBnIiwicmVzaXplLDIwMDAsMjAwMCJdfQ.5mzQeAtHMJMqXhZdmtuBZFObuwQ_YmVcx4GdSX5tE0Q.jpg',
        },
        {
          id: 96,
          artist: 'Adolph Gottlieb',
          name: 'Eclipse (1952)',
          style: 'Expresionismo Abstracto (Color-Field)',
          information: 'En su obra, el color es pintad mediante pinceladas gestuales y se sistancia en formas concretas que se transforman en asociaciones de símbolos casi caligráficos. Con el tiempo realizará una serie de paisajes imaginarios en los que la línea del horizonte separa las dos zonas del cuadro.' +
            '',
          url: 'https://static4.museoreinasofia.es/sites/default/files/obras/AD01557.jpg',
        },
        {
          id: 97,
          artist: '-',
          name: 'Informalismo',
          style: '',
          information: 'El Informalismo nace en europa a finales de los 40 como tendencia pictórica abstracta, instintiva y espontánea. Supone una ruptura con las vanguardias históricas y se desarrolla en paralelo al Expresionismo Abstracto de Estados Unidos. Utilizan un lenguaje abstracto, preeminencia del gesto, atracción por todo tipo de materiales y se le da importancia al automatismo surrealista.\n' +
            'La personalidad del artista se plasma a través de las técnicas y materiales empleados, del gesto y del azar. Existe una gran vinculación con la filosofía existencial.',
          url: '',
          title: 'Informalismo'
        },
        {
          id: 98,
          artist: 'Wols',
          name: 'Composition (1947)',
          style: 'Informalismo',
          information: 'Influido por el surrealismo, parte de la figuración para llegar a soluciones donde elcolor y la forma se plasman impulsivamente. Tanto la pincelada como la materia cobran importancia creando obras con relieve. Utiliza manchas de color y por ello se le considera el padre del Tachismo' +
            '',
          url: 'https://uploads1.wikiart.org/images/wols/composition-1947.jpg!Large.jpg',
        },
        {
          id: 99,
          artist: 'Jean Fautrier',
          name: 'L`arbre vert (1942)',
          style: 'Informalismo',
          information: 'Jean Fautrier introduce densas texturas matéricas en sus obras llamándolas "superficies construidas". Combinación del cromatismo apagado con referencias a cuerpos y elemntos naturales.' +
            '',
          url: '',
        },
        {
          id: 100,
          artist: 'Jean Dubuffet',
          name: 'Dhôtel nuancé d`abricot (1947)',
          style: 'Informalismo',
          information: 'Se puede apreciar en su obra la provocación del Dadaismo y del automatismo surrealista. Glorificación del arte realizado por pacientes mentales, niños o delincuentes. Este Art Brut es el arte producido por personas que trabajan al margen de las normas estéticas y no son profesionales. Sus obras muestran personajes pueriles, crueles y morbosos utilizando diferentes texturas materiales.' +
            '',
          url: 'https://www.centrepompidou.fr/media/picture/da/d4/dad4072462fcffef1cc3112f0c20ab02/thumb_large.jpg',
        },
        {
          id: 101,
          artist: 'Hans Hartung',
          name: 'Composition (1952)',
          style: 'Informalismo',
          information: 'Hartung incorpora la caligrafía a la pintura, desarrollando una pintura de acción gestual del signo caligráfico. Su obra influyó a la abstracción lírica de los 60-70' +
            '',
          url: 'https://assets.phillips.com/image/upload/t_Website_LotDetailMainImage/v1/auctions/UK010716/172_001.jpg',
        },
        {
          id: 102,
          artist: 'Alberto Burri',
          name: 'Legno e rosso 3 (1956)',
          style: 'Informalismo',
          information: 'Su obra la trabaja sobre tela de arpllera a la que oncorpora distintos elementos tomados de la relidad, como chapas, plásticos, maderas parcialmente quemadas... Es un renacer del collage en todo su esplendor material como medio a la representacion de sentimientos y vivencias subjetivos.' +
            '',
          url: 'https://i.pinimg.com/originals/9b/64/78/9b6478dd54083707e1c051263d2de57e.jpg',
        },
        {
          id: 103,
          artist: 'Manolo Millares',
          name: 'Cuadro 173 (1962)',
          style: 'Informalismo',
          information: 'Al igual que Burri, realizaba sus obras sobre tela de arpillera incorporando sacos, cuerdas, maderas y objetos de deshecho. Pinturas en blanco, rojo o negro que eran aplicadas en capas chorreantes' +
            '',
          url: 'https://lamecanicaceleste.files.wordpress.com/2020/06/image038.jpg',
        },
        {
          id: 104,
          artist: 'Antoni Tápies',
          name: 'Pintura (1955)',
          style: 'Informalismo',
          information: 'Para el autor es importante el sustrato material de la obra, creando cuadros en los que trabaja como si fuera un muro con arena y cemento al que incorpora huellas informales, escritos, cruces y huellas de manos y pisadas. Uso de colores sobrios incorporados desde las propias calidades de los materiales usados.' +
            '',
          url: 'https://catalogo.artium.eus/sites/default/files/imagenes/artistas/TapiesAntoni/imagen069.jpg',
        },
        {
          id: 105,
          artist: 'Antonio Saura',
          name: 'Grito Nº7 (1959)',
          style: 'Informalismo',
          information: 'Empieza experimentando en el surrealismo y la abstracción hasta que empieza con sus pinturas con trazos poderosamente gestuales en blanco, begr, grises y tierras a partir de la estructura de la figura humana' +
            '',
          url: 'https://static1.museoreinasofia.es/sites/default/files/obras/AS05695.jpg',
        },
        {
          id: 106,
          artist: 'Karel Appel (Grupo COBRA)',
          name: 'Hip Hip Hoorah! (1949)',
          style: 'Informalismo',
          information: ' Su objetivo es alcanzar una pintura pura, capaz de transformar el impulso vital de la creación en improvisación pictórica. Sus obras tienen un aire primitivista y una violencia deliberadas. Aunque se acerca a la abstracción, tiene temas y referentes reconocibles.' +
            '',
          url: 'https://i.pinimg.com/originals/91/02/72/9102727766055fb76632e6299cf8dbed.jpg',
        },
        {
          id: 107,
          artist: 'Asger Jorn (Grupo COBRA)',
          name: 'Prosit Neujahr (1958)',
          style: 'Informalismo',
          information: 'Plantea una deformación extrema y expresionista de la figura humana. Esta deformación esquizofrénica le sirve para rebelarse contra lo normalizado y le sirve para asentar las bases de su investigación sobre las capas inconscientes de la creatividad' +
            '',
          url: 'https://i.pinimg.com/originals/fe/d3/97/fed3979aa038b1a47a5c1c1354e8b2aa.png',
        },
        {
          id: 108,
          artist: 'Pierre Alechinsky (Grupo COBRA)',
          name: 'La Nuit (1952)',
          style: 'Informalismo',
          information: 'Tiene un estilo vigoroso y un trazo expresivo próximo a la abstracción. Inventa una iconografía informal más allá de lo figurativo trabajando desde la gestualidad usando materiales más fluidos y de rápido secado.' +
            '',
          url: 'http://www.artnet.com/WebServices/images/ll00144lldv5mJFgU7S62CfDrCWvaHBOcOP9F/pierre-alechinsky-la-nuit.jpg',
        },
        {
          id: 109,
          artist: '-',
          name: 'Pop Art',
          style: '',
          information: 'El término hace referencia a la expresión Popular Art para referirse a un amplio repertorio de imágenes provenientes de la cultura de masas elaboradas y difundidas por la televisión, el cine, la publicidad o el cómic.\n' +
            'Sus antecedentes artísticos son la síntesis del realismo y surrealismo en la tradición norteamericana (Edward Hopper) y las técnicas que empieza a explotar el Neo Dadá. Ls trabajos de Ready made de Duchamp introducen la inclusión del objeto banal y cotidiano al discurso artístico como propio objeto de arte.',
          url: '',
        },
        {
          id: 110,
          artist: 'Robert Rauschenberg',
          name: 'Monogram (1955-1959)',
          style: 'Expresionismo Abstracto => Pop Art',
          information: 'Trabaja combinando materiales de diversa procedencia para realizar composiciones artísticas innovadoras buscando la asociación de pintura y objeto (assemblages)' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvbW9ub2dyYW1hLXJhdXNjaGVtYmVyZy5qcGciLCJyZXNpemUsODAwIl19.RysuQ2yqIHzE94A7AqH1y4iLzDsDzSf2fA3Mf7wFx4E.jpg',
        },
        {
          id: 111,
          artist: 'Jasper Johns',
          name: 'Flag (1954)',
          style: 'Pop Art',
          information: 'De referencias dadaístas, sus obras muestran una imagen de un objeto trivial y cotidiano para criticar el cunsumo de bienes materiales y espirituales. Sus obras más conocidas son las American Flags' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvYmFuZGVyYS1qYXNwZXIuanBnIiwicmVzaXplLDgwMCJdfQ.UEVyJHqVutNmWlljsK3ORc_x-F52WcrU-ITTc6E6yk8.jpg',
        },
        {
          id: 112,
          artist: 'Richard Hamilton',
          name: 'Just what is it that makes today’s homes so different, so appealing? (1956)',
          style: 'Pop Art',
          information: 'Considerada la primera obra de Pop Art de la historia del arte. Mediante un collage con diferentes imágenes sacadas de la industria del momento en las que aparecen un hombre y una mujer desnudos y muy estilizados realiza una crítica al consumismo de la época.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvaGFtaWx0b24uanBnIiwicmVzaXplLDgwMCJdfQ.czZObNYKAobTob6_80t2xaoeQXfOuWfLkPTOJo452o8.jpg',
        },
        {
          id: 113,
          artist: 'Claes Oldenburg',
          name: 'Clothespin (1976)',
          style: 'Pop Art',
          information: 'Realiza instalaciones en el espacio público de esculturas gigantescas que replican los objetos cotidianos de consumo. De esta forma, estos objetos pierden su cotidiandad y aparecen desnaturalizados ante el espectador.' +
            '',
          url: 'https://i.pinimg.com/originals/52/b4/73/52b4731595267d362b608d5225003104.jpg',
        },
        {
          id: 114,
          artist: 'Claes Oldenburg',
          name: 'Soft Toiler (1966)',
          style: 'Pop Art',
          information: 'Se trata de una Soft Sculpture, que son esculturas blandas sdonde el espectador puede tocar y disfrutar de la obra de arte y dejarse llevar por su sensación placentera.' +
            '',
          url: 'https://whitneymedia.org/assets/artwork/425/146494.jpeg',
        },
        {
          id: 115,
          artist: 'Roy Lichtensteiin',
          name: 'Whaam! (1963)',
          style: 'Pop Art',
          information: 'Los cuadros de este autor senormes cuadros realizados a mano a partir de imágenes tomadas del cómic utilizando la técnica del tramado y los colores brillantes de su impresión original. Sus temas y composiciones aparecen como triviales y desindividualizadas.' +
            '',
          url: 'https://assets.catawiki.nl/assets/2018/10/19/0/7/e/07e37591-8a40-430a-a4cc-a14847ecb702.jpg',
        },
        {
          id: 116,
          artist: 'Andy Warhol',
          name: 'Marilyn Monroe (1967)',
          style: 'Pop Art',
          information: 'Warhol es uno de los artistas más conocidos del siglo XX. Su trabajo se integra en el modelo productivo de la cadena de montaje, eligiendo modelos figurativos (objetos cotidianos de consumo o personajes de fama mundial) y transformándolos en obras de arte a partir del uso masivo de seriación (serigrafía)' +
            '',
          url: 'https://1.bp.blogspot.com/-HYtIaWzfDIc/TfnbpPwF0II/AAAAAAAAA1U/-gUGfl6KHMk/s1600/andy_warhol_marilyn_monroe.jpg',
        },
        {
          id: 117,
          artist: 'Tom Wesselmann',
          name: 'Great American Nude nº92 (1967)',
          style: 'Pop Art',
          information: 'Sus obras de grandes desnudos amercanos fueron realizados al principio como collages pero acabó pintándolos con óleo y pintura acrílica. Las obras fueron ganando en tamaño hasta alcanzar dimensiones tales que acabarían siendo enormes murales en los que introducía elementos cotidianos del consumo como televisiones, teléfonos, radiadores, mesas o ventanas. Para que el espectador pudiera disfrutar en este caso del tema, sólo se podía mirar la obra de frente.' +
            '',
          url: 'https://www.tomwesselmannestate.org/wp-content/uploads/2016/04/GAN92.jpeg',
        },
        {
          id: 118,
          artist: 'James Rosenquist',
          name: 'Untitled #3',
          style: 'Pop Art',
          information: 'Rosenquist comenzó pintando carteles publicitarios de colores fluorescentes. Aplicando el lenguaje publicitario consiguió su fama internacional. Sus obras de gigantesco tamaño y por la intensidad fosforescente de su puntura  tiene un complejo entramado óptico y mecánico que hace ver a lo artificial como la única verdad.' +
            '',
          url: 'https://www.galeriedada.com/img_big/james-rosenquist-untitled-number-3-00003719.jpg',
        },
        {
          id: 119,
          artist: '-',
          name: 'Hiperrealismo',
          style: '',
          information: 'Nació en Estados Unidos a finales de los sesenta y fue denominada como fotorrealismo, que es la pintura basada en el uso de las fotografías para reunir la información visual y a partir de estas, proceder a la creación de una pintura de apariencia fotográfica.\n' +
            'Esta idea de pasar de la fotografía a la pintura deja de lado cualquier forma de subjetividad, fijando un fragmento de la realidad de forma exacta y objetiva.\n' +
            'Es un movimiento que evolucionó desde el Pop Art como una opción contrapuesta al Expresionismo Abstracto. Usaban también las imágenes estereotipadas del consumismo norteamericano. Existen diferentes temáticas pero no existe ni la ironía ni la nostalgia de la forma de vida americana propia del Pop Art.\n' +
            'Del Pop Art también toma la técnica impersonal y mecánica utilizada en la realización de sus obras usando técnicas como la proyección de diapositivas y transparencias sobre el lienzo, pintando encima de una imagen proyectada o mediante el sistema de transferencia de cuadrícula. Se debía hacer desaparecer la pincelada, empleando con forma meticulosa el pincel o recurriendo al aerógrafo.',
          url: '',
        },
        {
          id: 120,
          artist: 'Malcom Morley',
          name: 'Onsettant Moie (1974)',
          style: 'Hiperrealismo',
          information: 'Este artista destacaba por agrandar imágenes de revistas o postales a través de una cuadrícula. En un primer momento su iconografía se basa en las memorias de la guerra y posteriormente en las estrellas del deporte' +
            '',
          url: 'https://uploads5.wikiart.org/images/malcolm-morley/onsettant-moie-1974.jpg!Large.jpg',
        },
        {
          id: 121,
          artist: 'Richard Estes',
          name: 'Six Views of Edo: Shinjuko III (1989)',
          style: 'Hiperrealismo',
          information: 'Es un artista reconocido por sus pinturas de paisajes urbanos como cines, bares, establecimientos comerciales y en especial el coche. Parte de la fotografía, destacando especialmente ne los reflejos de los cristales y metales cromados.' +
            '',
          url: 'https://d32dm0rphc51dk.cloudfront.net/wbj_TAW5yTynsblUj-tnuA/large.jpg',
        },
        {
          id: 122,
          artist: 'Chuck Close',
          name: 'Mark (1979)',
          style: 'Hiperrealismo',
          information: 'Realiza pinturas de gran formato del rostro humano con una precisión asombrosa, consiguiendo casi un análisis entomológico del sujeto. El uso icónico del rostro humano casi parece una imagen de fotomatón ampliada\n' +
            'Al principio usaba el blanco y el negro para, posteriormente, ir incorporando el color creando una retícula puntillista que se puede contemplar de forma diferente en función del ángulo de visión. A partir de los 80, incorpora la información computerizada a sus obras sustituyendo al a fotografía.',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvd29yazA3NS16b29tLmpwZyIsInJlc2l6ZSw4MDAiXX0.y-qF2ciGWRy2TjOEErTypCkjGA6XsrsvUCO8ruGWRx0.jpg',
        },
        {
          id: 123,
          artist: 'Duane Hanson',
          name: 'Supermarket Lady',
          style: 'Hiperrealismo',
          information: 'Tanto Duane Hanson como John de Andrea realizan esculturas hiperrealistas. Ambos trabajan a partir de moldes de figuras humanas hechas en poliester o fibra de vidrio, a los que pintan, visten o desnudan creando una serie de personajes arquetípicos de la sociedad contemporánea. En este caso, el autor realiza una crítica a la sociedad de consumo.' +
            '',
          url: 'http://1.bp.blogspot.com/-WdDPdHl1klM/UclhZ5xToJI/AAAAAAABoY4/lk7qCBpnesk/s1600/duane-hanson-supermarket-lady.jpg',
        },
        {
          id: 124,
          artist: '-',
          name: '',
          style: 'Abstracción Post-pictórica',
          information: 'Térnmino para referirse a un grupo de artistas que pretendían superar el Expresionismo Abstracto sin que ello significara posicionarse en la pintura figurativa. Sustituyeron la pincelada gestual expresiva por las áreas geométricas definidas y claras de color. Dentro de la Abstracción post-pictórica podemos identificar dos tendencias:' +
            '- Colour Field: Se caracteriza por amplios campos de color liso aplicados en los cuadros mediante una finísima capa, eliminando cualquier ilusión espacial, dando lugar a obras de gran formato.' +
            '- Hard edge: El color se aplica en formas geométricas claramente definidas y delimitadas entre sí por unos contornos muy pronunciados, produciendo la figuración plástica del color en el borde del cuadro.',
          url: '',
          title: 'Abstracción Post-pictórica'
        },
        {
          id: 125,
          artist: 'Piet Mondrian',
          name: 'Broadway Boogie Woogie',
          style: 'Abstracción Post-pictórica',
          information: 'Se evidencia el uso de las superficies geométricas de Color' +
            '',
          url: 'https://images-na.ssl-images-amazon.com/images/I/61fD4Nd1eML._AC_SX522_.jpg',
        },
        {
          id: 126,
          artist: 'Max Bill',
          name: 'Radiation of Pink',
          style: 'Abstracción Post-pictórica',
          information: 'Define el espacio de la abstracción a partir del espacio, color, luz y movimiento en una combinación de elementos constructivos a paritr de superficies geométricas de colores planos.' +
            '',
          url: 'https://uploads1.wikiart.org/images/max-bill/radiation-of-pink-1973.jpg',
        },
        {
          id: 127,
          artist: 'Ad Reinhardt',
          name: 'Abstract Painting, Red (1952)',
          style: 'Abstracción Post-pictórica',
          information: 'Presenta espacios de color simétricos en los que intenta llevar al máximo la expresividad cromática' +
            '',
          url: 'https://www.moma.org/media/W1siZiIsIjE3OTUyNiJdLFsicCIsImNvbnZlcnQiLCItcXVhbGl0eSA5MCAtcmVzaXplIDIwMDB4MjAwMFx1MDAzZSJdXQ.jpg?sha=b20788ae2192cb02',
        },
        {
          id: 128,
          artist: 'Keneth Noland',
          name: 'Turnsole (1961)',
          style: 'Abstracción Post-pictórica (Colour field)',
          information: 'Noland dispone en sus cuadros mezclas luminosas de color ordenadas en el lienzo en formatos geométricos (rectángulos, cuadrados o círculos). Noland deja que la tela se coloree superficialmente eliminando cualquier atisbo de jesto o pincelada. Esta técnica se llama soak satin.' +
            '',
          url: 'https://m.media-amazon.com/images/I/41sm41QhwxL._AC_.jpg',
        },
        {
          id: 129,
          artist: 'Morris Louis',
          name: 'Beta Lambda (1961)',
          style: 'Abstracción Post-pictórica (Colour field)',
          information: 'Louis utilizaba también la técnica del derrame de color mediante pintura acrílica muy diluida y vertida sobre la tela sin preparar. Las capas de color las aplica de forma sucesiva' +
            '',
          url: 'https://deplatayexacto.files.wordpress.com/2010/11/beta-lambda-morris-louis-1961.jpg?w=640',
        },
        {
          id: 130,
          artist: 'Ellsworth Kelly',
          name: 'Mediterranee (1952)',
          style: 'Abstracción Post-pictórica (Hard Edge)',
          information: 'Kelly trabaja a menudo con un solo color, en cuadros muy definidos o juntando cuadros monocromos. La formación geométrica de cada cuadro se coloca en primer plano' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/L/L02/L02465_9.jpg',
        },
        {
          id: 131,
          artist: 'Frank Stella',
          name: 'Empress of India (1965)',
          style: 'Abstracción Post-pictórica (Hard Edge)',
          information: 'Enfatizaba la pintura como objeto físico. Para él la pintura es una superficie plana con pintura en ella. Rompe con el formato de cuadro tradicional de tal forma que las formas geométricas creadas en la superficie de este, determinan la forma física exterior del cuadro (Shaped canvas)' +
            '',
          url: 'https://uploads5.wikiart.org/images/frank-stella/empress-of-india-1965.jpg!Large.jpg',
        },
        {
          id: 132,
          artist: '-',
          name: 'Supports-surfaces',
          style: '',
          information: 'Movimiento pictórico que surge en Francia, llamado también Nuevo Reduccionismo. Los artistas declaran que el objeto de la pintura es la propia pintura, sin apelar a los sentimientos, artista o incluso a la historia del arte. Son obras inexpresivas y neutras. Cuestiona los principios elemntales de la pintura. Se cuestionan la función del bastidor tradicional' +
            '',
          url: '',
          title: 'Supports-surfaces'
        },
        {
          id: 133,
          artist: 'Claude Viallat',
          name: 'Untitled Nº56 (1996)',
          style: 'Supports-surfaces',
          information: 'Pintaba sobre tejidos y telas reciclados de forma repetitiva y neutra el mismo motivo pictórico en forma de ameba y mancha de camuflaje.' +
            '',
          url: 'https://uploads8.wikiart.org/images/claude-viallat/untitled-2007-126-2007.jpg!Large.jpg',
        },
        {
          id: 134,
          artist: '-',
          name: 'Arte cinético',
          style: '',
          information: 'Es el arte que implica movimiento cuyo interés no radica en el movimiento representado, si no en el movimiento mismo como parte sustancial de la obra artística. Su origen se centra en los manifiestos futuristas. ' +
            '',
          url: '',
          title: 'Arte cinético'
        },
        {
          id: 135,
          artist: 'Moholy-Nagy',
          name: 'Licht-Raum-Modulator (1922-1930)',
          style: 'Arte cinético',
          information: 'Plantea la importancia de la luz en sus construcciones conéticas. La luz abarca el ambiente que rodea a la máquina envolviendo el entorno. Contribuyó a la reflexión sobre el papel del espectador delante de una pieza de arte cinético, donde esta tiene que funcionar de forma activa integrando toda la información que le ofrece la obra.' +
            '',
          url: 'http://www.artnet.com/WebServices/images/ll04417lldqpYGFg8GECfDrCWvaHBOcXUaC/l%C3%A1szl%C3%B3-moholy-nagy-licht-raum-modulator-(+-wire-sculpture;-2-works).jpg',
        },
        {
          id: 136,
          artist: 'Alexander Calder',
          name: 'Mobile Rouge Triomphant (1963)',
          style: 'Arte cinético',
          information: 'Introdujo la idea de la escultura móvil (obras donde el aire se convertía en el motor del movimiento de la misma). Sus obras estaban formadas por planchas metálicas suspendidas por varillas del mismo material que permitía su movimiento libre en cualquier dirección y pintadas con colores primarios. Al principio fue de dimensiones reducidas y posteriormente fueron ganando tamaño hasta ocupar el espacio público.' +
            '',
          url: 'https://arthur.io/img/art/000173449bc51017a/alexander-calder/rouge-triomphant/large/alexander-calder--rouge-triomphant.jpg',
        },
        {
          id: 137,
          artist: 'Jean Tinguely',
          name: 'Méta-Matic Nº. 6 (1959)',
          style: 'Arte cinético',
          information: 'Creó toda una serie de máquinas escultóricas (Meta-Matic) que se movían gracias a motores eléctricos. Su intención era irónica, mostrar máquinas inútiles haciendo un trabajo constante en clara referencia al sistema de producción en cadena del sistema capitalista. También diseño una máquina que mediante un brazo mecánico dibujaba garabatos en un papel.' +
            '',
          url: 'https://uploads4.wikiart.org/images/jean-tinguely/m-ta-matic-no-6-1959.jpg',
        },
        {
          id: 138,
          artist: '-',
          name: 'Op Art',
          style: '',
          information: 'Existen dos corrientes en el Op Art: una estática que trabaja a nivel bidimensional del cuadro y una cinética que a partir de las investigaciones constructivistas operan en las tres dimensiones del espacio a partir de la modulación física de la luz.\n' +
            'La finalidad de este movimiento es producir la ilusión de vibración o movimiento en la superficie del cuadro. A diferencia del Arte cinético, estas obras no tienen un movimiento real. Fueron rápidamente aceptadas por el público e influyeron en la publicidad, moda y artes gráficas de los 60 (psicodelia)\n' +
            'El movimiento nace en Europa a partir de una exposición cuyos artistas investigan acerca de la ilusión óptica',
          url: '',
          title: 'Op Art'
        },
        {
          id: 139,
          artist: 'Josef Albers',
          name: 'White Line Square IV (1966)',
          style: 'Op Art',
          information: 'Albers trabaja en el proceso de reducción de color y forma usando la figura del cuadrado. Gracias a este, el color "vibra" libremente en correspondencia con el color vecino' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/P/P01/P01786_9.jpg',
        },
        {
          id: 140,
          artist: 'Victor Vasarely',
          name: 'Zebra (1937)',
          style: 'Op Art',
          information: 'Comienza sus investigaciones perceptivas trbajando con la vibración que origina en el ojo del espectador a partir de estructuras regulares blancas y negras. Se crea una ilusión de proyección tridimensional que da al cuadro una sensación de profundidad que no está basada en la perspectiva tradicional.' +
            '',
          url: 'https://uploads5.wikiart.org/images/victor-vasarely/zebra-1937.jpg',
        },
        {
          id: 141,
          artist: 'Bridget Riley',
          name: 'Fall (1963)',
          style: 'Op Art',
          information: 'Uso de planos seriados ondulados que producen un efecto cinético inmediato superponiéndose dos efectos simultáneos de movimiento.' +
            '',
          url: 'https://lh3.googleusercontent.com/proxy/-E27Z-Q257sQe92XUtnGHQRZYSS1i-x6_QfqEWziViOcvOucE7tJiujQnm5FP86BqKtko7kqVXRVF3O-xLeMK4xIkDqd3Gt4ICUB6vACworUqDRP6hriv3YC9z8DhqhkZGJ7UisPemhBhTgqKp4',
        },
        {
          id: 142,
          artist: 'Jesús Rafel Soto',
          name: 'Horizontal Movement (1963)',
          style: 'Op Art',
          information: 'Su trabajo se centra en una búsqueda del movimiento que le lleva a desafiar las posibilidades perspectivas del ojo. En su obra sitúa hilos de nylon, varillas metálicas o formas bidimensionales superpuestas delante de un cuadro de rayas verticales u horizontales creando un efecto de cambio perceptivo en el espectador dependiendo de su situación en relación al cuadro. De esta forma involucra al espectador en sus obras' +
            '',
          url: '',
        },
        {
          id: 143,
          artist: '-',
          name: 'Minimal Art',
          style: '',
          information: 'Tendencia escultórica de los 60 en Estados Unidos. Se trata de una serie de objetos de contenido mínimo con un origen no artístico (elementos industriales o tomados de la naturaleza). Era una reacción tanto a los excesos gestuales y subjetivos del Expresionismo Abstracto como a las nuevas expresiones del Pop art y el Hiperrealismo. Parte de la base de Van der Rohe de menos es más.\n' +
            'Se imponía una práctica artística abstracta cuyo potencial expresivo se limitaba a formas geométricas elementales, creando esculturas a partir de estos objetos y del espacio que los rodeaba. Este concepto rompe con el de la tradicional escultura como pieza individual y ubicada con independencia del espacio que le rodea\n' +
            'A la vez, se deshace de cualquier ornamento superfluo que dificulte la percepción de las características de la obra. De esta manera el espectador está obligado a percibir aspectos y características funcionales del espacio. Al tener la sensación de no haber nada que ver, el espectador debe hacer un esfuerzo y reaizar un recorrido por la obra para entender lo que el artista le ofrece.',
          url: '',
          title: 'Minimal Art'
        },
        {
          id: 144,
          artist: 'Robert Morris',
          name: 'Untitled (1965)',
          style: 'Minimal Art',
          information: 'El artista presenta un conjunto de piezas que recuerda a un juegode construcción gigante. Esto le sugiere al espectador la posibilidad mental de jugar con dichas estructuras, multiplicándose las posibilidades perceptivas.' +
            '',
          url: 'https://smarthistory.org/wp-content/uploads/2018/08/Robert-Morris-L-Beams-thumb-570x350.png',
        },
        {
          id: 145,
          artist: 'Donald Judd',
          name: 'Untitled (10 cajas de acero) (1969)',
          style: 'Minimal Art',
          information: 'Judd plantea una serie de cajas y cubos de metal idénticos y repetidos que limitan un espacio interior, un espacio exterior y la relación con el espacio circundante.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/T/T03/T03087_9.jpg',
        },
        {
          id: 146,
          artist: 'Carl André',
          name: '43 Roaring forty (1968)',
          style: 'Minimal Art',
          information: 'Plantea construcciones a partir de piezas repetidas, sobretodo láminas cuadradas o rectangulares metálicas estableciendo una relación entre el número de piezas y el material del que están hechas. Su lienco es el suelo, que se convierte en el espacio expositivo donde distribuir los signos. El espectador se ve obligado a recorrer y repensar el espacio donde se ubica cada obra, e incluso a pisarla.' +
            '',
          url: 'https://i.pinimg.com/originals/bc/5d/2b/bc5d2b85bff69df83e50e50dbdf43d2d.jpg',
        },
        {
          id: 147,
          artist: 'Dan Flavin',
          name: 'Ultraviolet Light Room (1968)',
          style: 'Minimal Art',
          information: 'En sus trabajos usa tubos de luz fluorescentes incorporando así la luz eléctrica a la escultura. Las sencillas compsociones de diferente tamaño destacan por la energía y el color de los mismos de tal forma que los espacios donde se ubican quedan distorsionados y crean diferentes ambientes. Pretende transformar la atmósfera donde se instalaban. El propio espacio es la obra en si' +
            '',
          url: 'http://www.rudedo.be/amarant08/wp-content/uploads/2016/02/Flavin23.jpg',
        },
        {
          id: 148,
          artist: 'James Turrell',
          name: 'Rondo (Blue) (1969)',
          style: 'Minimal Art',
          information: 'La línea de trabajo de Turrel converge con la de Dan Flavin. Su objetivo es modificar los espacios a través de la luz. No trabaja con la luz, sino que su propio trabajo es la luz. Crea espacios de meditación, intimidad y reflexión donde la experiencia del espectador es la base de su obra.' +
            '',
          url: 'https://uploads5.wikiart.org/00210/images/james-turrell/rondo-image-at-total1-1.jpg!Large.jpg',
        },
        {
          id: 149,
          artist: 'Eva Hesse',
          name: 'Untitled (1970)',
          style: 'Minimal Art',
          information: 'Se trata de una abstracción excéntrica. Pone énfasis en lo exótico, excéntrico, vitalista y sensual. Hesse utiliza materiales extraños, flexibles y formas y gamas cromáticas indeterminadas. Con una fuerte influencia surrealista.' +
            '',
          url: 'https://i2.wp.com/lebastart.com/wp-content/uploads/2017/10/eva-hesse-untitled-rope-piece.jpg?fit=820%2C597',
        },
        {
          id: 150,
          artist: 'Robert Morris',
          name: 'Untitled (brown felt) (1973)',
          style: 'Process Art/Anti-form',
          information: 'Robert Morris evoluciona desde el Minimal Art hasta la reivindicación del uso de materiales no rígidos en la experiencia escultórica que abrían camino hacia lo impeciso e imprevisible en el resultado final de la obra.' +
            '',
          url: 'https://www.guggenheim.org/wp-content/uploads/1973/01/91.3802_ph_web-1.jpg',
        },
        {
          id: 151,
          artist: '-',
          name: 'Land Art',
          style: '',
          information: 'Los artistas que formaban parte del Anti-Form defendían la necesidad de utilizar nuevos materiales para expresar sus planteamientos artísticos. Algunos de ellos empezarn a utilizar materiales tomados de la naturaleza (piedras, troncos...) y/o utilizar el paisaje natural como objeto de trabajo manipulándolo o alterándolo con intención artística.' +
            '',
          url: '',
          title: 'Land Art'
        },
        {
          id: 152,
          artist: 'Robert Smithson',
          name: 'Spiral Jetty (1970)',
          style: 'Land Art',
          information: 'Smithson se interesó sobretodo en la transformación de espacios naturales en obras de carácter artístico. Sus intervenciones efímeras necesitaban ser documentadas. Spiral Jetty es una esperal de tierra y pedras creada en las aguas del Great Salt Lake de Utah. La espiral corresponde al minimalismo así como recuerda a las formas iconográficas místicas de la prehistoria.' +
            '',
          url: 'https://masdearte.com/media/n_spiraljetty.jpg',
        },
        {
          id: 153,
          artist: 'Michael Heizer',
          name: 'Double Negative (1969-1970)',
          style: 'Land Art',
          information: 'Este artista empezó a trabajar en lugares desérticos desplazando tierra y usando materiales del terreno. Realizó una gran cantidad de obras geométricas ya desaparecidas por la erosión del terreno. En este Double Negative, crea una gigantesca fosa en forma de cruz vaciando y desplazando tierra para conseguirla' +
            '',
          url: 'https://i.pinimg.com/originals/97/66/36/97663655597859345e06b5e41a2c8d81.jpg',
        },
        {
          id: 154,
          artist: 'Walter de María',
          name: 'The Lighting Field (1977)',
          style: 'Land Art',
          information: 'Trabajó tanto en obras efímeras como en otras de caracter permanente. En The Lighting Field dispuso 400 postes de acero con función de pararrayos colocados formando un rectángulo en el desierto de Nuevo México creando un potencial espectáculo de rayos cuando el tiempo lo permite.' +
            '',
          url: 'https://cdn.kastatic.org/ka-perseus-images/f710ad86d546a698a3a5bd2a5d84319a75ba40b8.png',
        },
        {
          id: 155,
          artist: 'Christo',
          name: 'Wrapped Reichstag (1971-1995)',
          style: 'Land Art',
          information: 'Christo interviene el espacio público envolviendo y/o empaquetando lugares con el fin de modificar y transformar la experiencia visual sobre los mismos.' +
            '',
          url: 'https://picnic.media/wp-content/uploads/2019/10/a0acb261455367c89fa8d7b439f1dac7-1050x700.jpg',
        },
        {
          id: 156,
          artist: '-',
          name: 'Performance Art',
          style: '',
          information: 'El Performance Art es el concepto genérico usado para todos los comportamientos de arte de acción (teatralizado) en los que el papel del público, en principio, se limita a la observación.' +
            '- Happening: Deudores del Dadaísmo. Se basa en improvisar, provocar y estimular la participación espontánea del público asistente. Se suelen ejecutar en lugares públicos. Sin la participación del público la obra no estaría completa.\n' +
            '   En este estilo destaca el Grupo Gutai, formado en Japón, realizó numerosas acciones de críticas a la guerra y a la sociedad capitalista de posguerra. La violencia de sus actos influyó en otros grupos como el Fluxus. El Fluxus es un movimiento artístico que engloba la música, la literatura y las artes plásticas.' +
            '- En el Body Art, el cuerpo del artista es el lugar y el medio de expresión artística realizandose acciones (públicas o privadas) sobre él mismo',
          url: '',
          title: 'Performance Art'
        },
        {
          id: 157,
          artist: 'Allan Kaprow',
          name: 'Yard (1967)',
          style: 'Happening',
          information: 'Artista Pop y alumno de John Cage, Allan Kaprow realizaba sus trabajos con situaciones prefijadas pero  no de un desarrollo continuo e inalterable. La acción-inacción improvisada del público marcaba el desarrollo de la actuación. La separación entre arte-vida y espectador-artista se volvía difusa' +
            '',
          url: 'https://masdearte.com/media/reb_accion2.jpg',
        },
        {
          id: 158,
          artist: 'Yoko Ono',
          name: 'Cut Piece (1965)',
          style: 'Happening',
          information: 'Perteneciente al movimiento Fluxus, en esta obre define el espíritu de la intervención espontánea del público al invitarle a cortarle la ropa con unas tijeras' +
            '',
          url: 'https://revistamirall.com/wp-content/uploads/2017/07/cut-me-bitch.jpg',
        },
        {
          id: 159,
          artist: 'Dennis Oppenheim',
          name: 'Reading Position for Second Degree Burn (1970)',
          style: 'Body Art',
          information: 'Trabaja con su cuerpo o con cuerpos ajenos en acciones relacionadas con el dolor y color pictórico. En esta acción el artista se expone al sol durante varias horas con un libro abierto sobre su pecho. Al final se nota la diferencia del tono de la piel. Con el tiempo abandonó el uso del cuerpo para sus acciones.' +
            '',
          url: 'https://uploads5.wikiart.org/images/dennis-oppenheim/reading-position-for-second-degree-burn-1970.jpg!Large.jpg',
        },
        {
          id: 160,
          artist: 'Chris Burden',
          name: 'Shoot (1971)',
          style: 'Body Art',
          information: 'El artista realizó una gran cantidad de controvertidas acciones en las que ponía en primer término la idea del riesgo y la autolesión como método de denuncia social. En este Shoot permitió que un amigo le disparara en el brazo a una corta distancia' +
            '',
          url: 'http://www.ahmagazine.es/wp-content/uploads/2015/05/tumblr_n2o2movjQi1qdrgo9o1_12801.jpg',
        },
        {
          id: 161,
          artist: '-',
          name: 'Arte Póvera',
          style: '',
          information: 'El Arte Póvera pretende ir en contra de la imaginería ensalzada del Pop Art y de las obras frías e industriales del Minimal. En contra del uso de materiales industriales y de la tecnología, apuesta por el uso de materiales perdurables y pobres cuya reutilización o transformación expresan la espontaneidad, libertad y creatividad del artista. Este uso de materiales humildes, la ocupación del espacio y la participación del público alejan el objeto artístico de su comercialización.' +
            '',
          url: '',
          title: 'Arte Póvera'
        },
        {
          id: 162,
          artist: 'Mario Merz',
          name: 'Iglú (1968)',
          style: 'Arte Póvera',
          information: 'Es conocido por sus esculturas iglús. Estas estructuras hemisféricas están realizadas con materiales de diversa procedencia (en este caso de piedra y metal) que identifica con viviendas nómadas y efímeras. Intenta buscar la obra de arte total con el contraste de elementos naturales y espacios artificiales.' +
            '',
          url: 'https://krollermuller.nl/media/cache/collection_item_detail_small/media/collectionitempage/tmsImage/igloo-di-pietra-mario-merz-48826-copyright-kroller-muller-museum.jpg',
        },
        {
          id: 163,
          artist: 'Michelangelo Pistoletto',
          name: 'Venere Degli Stracci',
          style: 'Arte Póvera',
          information: 'Realizó numerosas intervenciones como esta en la que se colocaba una escultura clásica de venus rodeada de trapos y ropa usada intentando representar desde la ironía los límites entre la belleza arminica y los deshechos.' +
            '',
          url: 'http://analisidellopera.it/wp-content/uploads/2019/09/Pistoletto_Venere_degli_stracci.jpg',
        },
        {
          id: 164,
          artist: 'Joseph Beuys',
          name: 'Como se explican los cuadros a una liebre muerta (1968)',
          style: 'Escultura Social',
          information: 'El hecho de que su avión fuera derribado y un grupo de nómadas le salvaran la vida usando grasa animal y fieltro hizo que usara estos materiales en su obra artística. En est performance que realiza ritualizada y simbólica se transforma en una escultura viviente. Empapado en miel y pan de oro y con una liebre muerta en sus brazos, recorre el espacio explicándole los cuadros a una liebre muerta' +
            '',
          url: 'https://2.bp.blogspot.com/_cOhtz9jGWSY/S-EKcVXNW8I/AAAAAAAAJSE/8P1Z8iGwAFM/s1600/beuys.jpg',
        },
        {
          id: 165,
          artist: 'Joseph Beuys',
          name: 'Fat Chair (1963)',
          style: 'Escultura Social',
          information: 'Beuys trabaja con materiales extraños aplicados a las prácticas artísticas que le sirvieron para ampliar y socializar el concepto de arte. Además de grasa animal y fieltro, usó botellas, hilos de cobre, animales disecados, cajas, archivadores, platos o vitrinas. La diferencia con el ready made es que los materiales usados los extrae de su vida personal. Los objetos escultura que él crea hacen que el arte se refiera a la totalidad de la gente y no solo a los artistas.' +
            'En este caso usa grasa animal y alambre en una silla.',
          url: 'https://jessesartspace.files.wordpress.com/2016/11/160c92a9cf55cb52e409c776fee8f78a.jpg?w=640',
        },
        {
          id: 166,
          artist: '-',
          name: 'Arte Conceptual',
          style: '',
          information: 'Con el arte Conceptual se culmina el proceso de desmaterialización de la obra de arte. Se realiza un desplazamiento del objeto artístico hasta la idea, el concepto. La teoría y el proceso se colocan en primer término en detrimento de la obra objetual terminada. Es por esto que la idea o el concepto es el aspecto más importante de la obra.\n' +
            'Duchamp es un antecedente directo del Conceptual a través del ready made cuestionando el papel del autor poniendo en primer lugar el concepto. Las ideas del Minimal Art intentan desmitificar el objeto a favor del concepto. El arte reflexiona sobre su propia naturaleza. El arte conceptual surgió de la obra más teorica de los artistas minimalistas',
          url: '',
          title: 'Arte Conceptual'
        },
        {
          id: 167,
          artist: 'Joseph Kosuth',
          name: 'One and three chairs (1965)',
          style: 'Arte Conceptual (lingüístico)',
          information: 'Entiende el arte como una actividad más que como una praxis. One and three chairs se puede observar la instalación de una silla, una fotografía de esa silla a tamaño real y un panel con la definición silla obtenida del diccionario. Se pone de manifiesto la limitación informativa que poseen tanto el objeto real como su reproducción visual como su definición lingüística. Se ponen de manifiesto las artes plásticas, la poesía y la linguística.' +
            '',
          url: 'https://www.researchgate.net/profile/David-Lopez-Rubino/publication/308795808/figure/fig1/AS:413179877314561@1475521167386/Joseph-Kosuth-One-and-three-chairs-1965-Siendo-cierto-que-cualquier-imagen-puede.png',
        },
        {
          id: 168,
          artist: 'Lawrence Weiner',
          name: 'To See and be Seen (1972)',
          style: 'Arte Conceptual (lingüístico)',
          information: 'Este artista basa su práctica de escultor en el lenguaje. Considera las palabras como arte. Palabras objeto sin contexto ni consideraciones literarias.' +
            '',
          url: 'https://uploads0.wikiart.org/images/lawrence-weiner/to-see-and-be-seen-1972.jpg',
        },
        {
          id: 169,
          artist: 'On Kawara',
          name: 'June 19, 1967 (1967)',
          style: 'Arte Conceptual (empírico medial)',
          information: 'Este autor desarrolla desde el 4 de enero de 1966 una monumental serie de pinturas bajo el título de Today' +
            '',
          url: 'https://uploads5.wikiart.org/images/on-kawara/june-19-1967-from-today-series-no-108-1967.jpg!Large.jpg',
        },
        {
          id: 170,
          artist: '-',
          name: 'Neoexpresionismo',
          style: '',
          information: 'La posmodernidad se refiere a la tendencia de la cultura, el arte y la filosofía que surgió en los 80. Se asocia al culto a lo individual desinterés por las utopías y rechazo al racionalismo. Hay una defensa de la hibridación, la diversidad, la cultura popular y se cuestionan los textos y las verdades universales.\n' +
            'Los pintores neoexpresionistas se caracterizan por su agresividad gestual, por los temas descarnados, los grandes formatos y la figuración expresiva. Surge como reacción a las tendencias formalistas del Minimal Art, Arte Conceptual, etc',
          url: '',
          title: 'Neoexpresionismo'
        },
        {
          id: 171,
          artist: 'Georg Baselitz',
          name: 'Weg vom Fenster (1982)',
          style: 'Neoexpresinismo',
          information: 'Baselitz pinta motivos figurativos con un lenguaje cercano a la abstracción cuyo autor denomina ornamento. Representa figuras cabeza abajo que se han convertido en su sello de identidad. Intenta que el espectador asuma el arte como una forma de oposición a las convenciones sociales y políticas imperantes.' +
            '',
          url: 'https://www.fondationbeyeler.ch/fileadmin/museumplus/multimedia/68199.jpg',
        },
        {
          id: 172,
          artist: 'Markus Lüpertz',
          name: 'Clitunno (1990)',
          style: 'Neoexpresionismo',
          information: 'PRetende buscar un lenguaje que define como concreción de lo abstracto. Juega co la geometría y la gestualidad.' +
            '',
          url: 'https://media.mutualart.com/Images/2018_03/13/08/085547834/4bd80ec5-bcc2-4c85-9c41-03625bce1207_570.Jpeg',
        },
        {
          id: 173,
          artist: 'Gerhard Richter',
          name: 'Chromatic Abstractions (1990)',
          style: 'Neoexpresionismo',
          information: 'Es un autor con una obra muy extensa y en la que ha experimentado con todo tipo de lenguajes. Su idea es despersonalizar el arte creando fotografías a través de la plástica. En sus pinturas abstractas amplía el efecto del rastro del pincel siguiendo esquemas geométricos Intenta mostrar la inexistencia de diferencias entre la figuración y la abstracción intercambiando ambos lenguajes constantemente\n' +
            '',
          url: 'https://i1.wp.com/revistaestilo.org/wp-content/uploads/2020/06/gerhard-richter-chromatic-abstractions-abstract-painting-1990.jpg?fit=970%2C705&ssl=1',
        },
        {
          id: 174,
          artist: 'Sigmar Polke',
          name: 'Girlfriends (1965-1966)',
          style: 'Neoexpresionismo',
          information: 'Sus pinturas son de diversas técnicas y soportes en las que plantea la crítica social como temática ya sea de la reciente historia alemana como en el consumo desmesurado de las imágenes pop por parte de la sociedad occidental.' +
            '',
          url: 'https://uploads1.wikiart.org/00288/images/sigmar-polke/girlfriends-freundinnen-1965-66.jpg!Large.jpg',
        },
        {
          id: 175,
          artist: 'A.R. Penck',
          name: 'Ur-End (1970)',
          style: 'Neoexpresionismo',
          information: 'Penck llena sus pinturas de figuras esquemáticas y primitivas y de pictogramas simples realizando una suerte de jeroglíficos universalmente comprendibles. Sus esculturas totémicas policromadas evoca los mismos tema y utiliza materiales de diversa procedencia como botellas, cartón, latas, madera, alambre...' +
            '',
          url: 'https://i.pinimg.com/originals/2f/2b/2c/2f2b2c2b509be68dd206bc45c9ba6e97.jpg',
        },
        {
          id: 176,
          artist: 'Jörg Immendorff',
          name: 'Café Desutschland IV (1978)',
          style: 'Neoexpresionismo',
          information: 'La obra de este autor tiene un gran contienido crítico al sistema capitalista e imperialesta. Sus enormes cuadros recrea situaciones que muestra esa dualidad política que sugría Alemani mediante un imaginario simbólico repleto de personajes.' +
            '',
          url: 'https://srv.deutschlandradio.de/media/thumbs/e/e17cdc4dfc062568c6c3839d1415ac6ev2_max_460x345_b3535db83dc50e27c1bb1392364c95a2.jpg?key=ae77a0',
        },
        {
          id: 177,
          artist: 'Anselm Kiefer',
          name: 'Velimir Chlebnikov (2004)',
          style: 'Neoexpresionismo',
          information: 'Este artista trabaja una pintura de enorme formato con gruesas capas de color combinadas con madera, alambre, plomo, ceniza, vidrio, paja, material de desecho y ramas de árboles. Sus cuadros destacan por sus colores sombríos. Unos assemblages en los que conviven pintura, materia y fotografía junto con un trazo expresivo y violento. Su concepción de la pintura es más literaria y folosófica mostrando interés por el paso del tiempo, el olvido y el desperdicio. Las capas superpuestas de sus obras forman una supericie densa y empastada pero permitiendo ver los diferentes estratos' +
            '',
          url: 'https://d32dm0rphc51dk.cloudfront.net/FDTH8uH5Utwjw9arYlh4hQ/large.jpg',
        },
        {
          id: 178,
          artist: 'Robert Combas',
          name: 'Composition aux trois pieds avec chaussures (1994)',
          style: 'Neoexpresionismo (figurativo)',
          information: 'Es el padre de la Figuración Libre. Su obra reivindica lo instintivo, satírico y la cultura popular. Realiza obras que son una especie de cómics de grandes dimensiones que proporciona un fresco de la sociedad contemporánea  con un componente claramente autobiográfico. Figuras humanas en entornos violentos y casi orgiásticos mezcladas con motivos deudores de la propia historia del arte con la intención de involucrar al espectador.' +
            '',
          url: 'http://www.artnet.fr/WebServices/images/ll00236lldXZ0GFgpeECfDrCWvaHBOcVCmD/robert-combas-composition-aux-trois-pieds-avec-chaussures.jpg',
        },
        {
          id: 179,
          artist: 'Jean-Michel Alberola',
          name: 'Labros (1982)',
          style: 'Neoexpresionismo (figurativo)',
          information: 'Al contrario que Combas, Alberola se implica en la renovación de la pintura volviendo la mirada a la Historia del Arte reivindicando la misma. Usando una figuración culta impregna sus obras con reflexiones sobre la historia de la pintura, los motivos religiosos católicos y guiños a las culturas africanas' +
            '',
          url: 'http://www.artnet.com/WebServices/images/ll00172lld0pYGFgVNECfDrCWvaHBOc7vaC/jean-michel-alberola-labros.jpg',
        },
        {
          id: 180,
          artist: 'José Manuel Broto',
          name: 'Los Prodigios II (1989)',
          style: 'Neoexpresionismo abstracto',
          information: 'Broto plantea una abstracción que combina formas abstractas con referencias formales a objetos geométricos, formas orgánicas o signos matemáticos, musicales o linüísticos. Realiza un trazo gestual con una gran expresividad acentuada por el uso de pintura de intensos colores que chorrea y gotea por el cuadro.\n' +
            'En su cuadro crea tensión entre la forma y el color utilizando veladuras mediante la superposición de finas capas de pintura acrílica muy líquida',
          url: 'https://static.arteinformado.com/resources/app/docs/organizacion/28/127828/obras/ad00148.jpg',
        },
        {
          id: 181,
          artist: 'Xavier Grau',
          name: 'Pelikan II (1996)',
          style: 'Neoexpresionismo abstracto',
          information: 'Sus obras parecen desprender una atmósfera de caos y destrucción pero hay diferentes niveles de lectura y se pueden ver una sucesión de colores enérgicos, movimiento y una efervescencia luminosa. En sus paisajes abstractos las figuras deambulan entre arquitecturas y escenografías sensuales resueltas mediante manchas de color espontáneas.' +
            '',
          url: 'https://static1.museoreinasofia.es/sites/default/files/obras/AD02075.jpg',
        },
        {
          id: 182,
          artist: 'Miquel Barceló',
          name: 'La gran cena española (1985)',
          style: 'Neoexpresionismo figurativo',
          information: 'En sus pinturas trata los problemas tradicionales de la pintura como la perspectiva y la luz, interesándose por la figuración tanto animal como humana, pintada de manera expresionista, descuidada y violenta. Sus motivos están extraídos de la naturaleza mediterránea y africana.' +
            '',
          url: 'http://3.bp.blogspot.com/-6LrxeFTVbgE/UujkDQKHkSI/AAAAAAAANCk/x9Vf54ToA7o/s1600/cena+espa%25C3%25B1ola+barcelo.jpg',
        },
        {
          id: 183,
          artist: 'José María Sicilia',
          name: 'Plaza de la Bastilla (1984)',
          style: 'Neoexpresionismo figurativo',
          information: 'En un primer momento crea obras de gran formato cuyos elementos figurativos son de uso doméstico, como tijeras o aspiradoras. Se puede apreciar sus trazos gestuales enérgicos y la aplicación de materia pictórica. Con el tiempo su pintura virará a la abstracción radical.' +
            '',
          url: 'https://static5.museoreinasofia.es/sites/default/files/obras/AS08737.jpg',
        },
        {
          id: 184,
          artist: 'Ferrán García Sevilla',
          name: 'Tata 13',
          style: 'Neoexpresionismo figurativo',
          information: 'Pasa del arte conceptual a la pintura expresiva donde reinan las figuras antropomorfas resueltas mediante grafismos primitivos y signos fragmentados y repetidos, de sus propias vivencias, sensaciones y obsesiones.' +
            '',
          url: 'https://static5.museoreinasofia.es/sites/default/files/obras/AD00149.jpg',
        },
        {
          id: 185,
          artist: '-',
          name: 'Transvanguardia',
          style: '',
          information: 'En Italia el movimiento pictórico de la Transvanguardia se enmarca dentro del neoexpresionismo de los 80. Se trataba de un grupo dispar de artistas que les unía la idea de recuperar la pintura como medio expresivo y superar las experiencias ideologizadas.\n' +
            'Valoran la pintura en la que prime el trabajo manual del artsta y su propia subjetividad e intuición frente a la impersonalidad y la objetividad planteadas por el Pop Art y el Minimal Art o el Conceptual Art. Retoman la figuración, el gesto y el signo.',
          url: '',
          title: 'Transvanguardia'
        },
        {
          id: 186,
          artist: 'Sandro Chia',
          name: 'Nicht for Richt (1984)',
          style: 'Transvanguardia',
          information: 'Chia comienza como artista conceptual hasta que reivindica el retorno a la pintura y al análisis y la reutilización de la obra de artistas del pasado y la incorporación irónica de temas mitológicos. Incorpora a menudo figuras humanas con aspecto de héroes clásicos en un escenario colorido, expresivo y teatral. En cambio, el héroe parece desmitificado y se le priva de cualquier épica.' +
            '',
          url: 'https://i.pinimg.com/originals/62/6b/a1/626ba116e593faf13934d8c072654b12.jpg',
        },
        {
          id: 187,
          artist: 'Mimmo Paladino',
          name: 'Sonata (1985)',
          style: 'Transvanguardia',
          information: 'Paladino expone que el arte es nómada porque atraviesa fonteras geográficas y temporales. Sus obras son deudoras de la mitología clásica y de los formatos y técnicas tradicionales. Mezcla objetos del presente con figuras arquetípicas representadas con trazos violentos y colores intensos. Con el tiempo crea esculturas de madera, bronce y piedra para dar vida a estos personajes' +
            '',
          url: 'http://2.bp.blogspot.com/-pIwr66HG7cI/VJGMrb1wzGI/AAAAAAABLUc/mmolAHFQJZ4/s1600/lacma_sonata%2B1985.jpg',
        },
        {
          id: 188,
          artist: 'Enzo Cucchi',
          name: 'Vitebsk-Harar (1984)',
          style: 'Transvanguardia',
          information: 'Introduce en sus obras figuras que remiten a la mitología y la tradición de las culturas arcaicas de Italia. Pinta y dibuja con una intensidad y una expresividad poderosas. Incorpora en ocasiones textos poéticos de su propia cosecha a sus obras. Usa óleo, carboncillo y collage.' +
            '',
          url: 'https://www.castellodirivoli.org/wp-content/uploads/2012/02/cucchi-Vitebsk.jpg',
        },
        {
          id: 189,
          artist: 'Francesco Clemente',
          name: 'Moon (1980)',
          style: 'Transvanguardia',
          information: 'Su obra se basa en una relectura del retrato narcisista, la sexualidad y la autodestrucción, dando como resultado una pintura irreverente. Su iconografía se basa en su experiencia en la India.' +
            '',
          url: 'https://www.moma.org/media/W1siZiIsIjIzNDQzNiJdLFsicCIsImNvbnZlcnQiLCItcXVhbGl0eSA5MCAtcmVzaXplIDIwMDB4MjAwMFx1MDAzZSJdXQ.jpg?sha=d1ef7a26b8e642ca',
        },
        {
          id: 190,
          artist: 'Nicola de Maria',
          name: 'Testa Rosa (1989)',
          style: 'Transvanguardia',
          information: 'A diferencia de otros artistas de este movimiento, realiza obras abstractas, laberínticas compuestas por formas irregulares y de colores estridentes. Sus obras son pintadas en paredes o muros otorgando una sensación de espacio irreal y onírico.' +
            '',
          url: 'https://i.pinimg.com/originals/06/f0/10/06f0103cd486b4a4accdd792231b2483.jpg',
        },
        {
          id: 191,
          artist: '-',
          name: 'Graffiti',
          style: '',
          information: 'Desde finales de los 60 se empezó a extender por los barrios marginales de las grandes ciudades de norteamérica el fenómeno de cubrir las paredes de espacios públicos con dibujos, garabatos, imágenes tomadas del cómic, mensajes o firmas. Convivían las intenciones reivindicativas con otras menos politizadas. Utilizaban el spray para sus obras.\n' +
            'La exposicion Post-Graffiti en una sala de arte de Nueva York fue determinante para el reconocimiento de este estilo por parte del mundo contemporáneo.',
          url: '',
          title: 'Graffiti'
        },
        {
          id: 192,
          artist: 'Jean Michek Basquiat',
          name: 'Profit I (1982)',
          style: 'Graffiti',
          information: 'Con una carrera artística meteórica (murió a los 27) pasó de los comienzos más marginales a tener relación artística con Warhol. Comenzó formando mensajes crípticos bajo el pseudónimo de SAMO pero pronto sintió una atracción por el dominio gestual de algunos artistas del Expresionismo Abstracto.\n' +
            'Basquiat afirmó que sus obras eran pinturas que estaban entre la abstracción gestual y la figuración expresiva más que en el propio grafiti. Su obra combina agresividad, humor, ironía con imágenes pobladas de elementos relacionados con la simbología primitiva. Sus textos e imágenes mezclan temas que abarcan desde el vudú hasta los retratos expresivos de héroes afroamericános de la música y el deporte de la época.',
          url: 'https://uploads0.wikiart.org/images/jean-michel-basquiat/profit-i.jpg!Large.jpg',
        },
        {
          id: 193,
          artist: 'Keith Haring',
          name: 'The Tree of Monkeys (1984)',
          style: 'Graffiti',
          information: 'Haring comenzó como accionista conceptual expresado en sus dibujos a tiza en el metro de nueva york. Utilizaba colores básicos muy saturados y líneas y contornos marcados y definidos. Sus temas iban desde la libertad sexual al activismo social y político. Su iconografía presenta personajes danzantes, mujeres embarazadas, hombres-animales, perros aulladores, máscaras tribales, etc. Con un estilo esquemático simplificado y lineal, llevó su obra a multitud de soportes que vendía en su tienda.' +
            '',
          url: 'https://uploads2.wikiart.org/00159/images/keith-haring/formatfactorykeith-haring2.jpg!Large.jpg',
        },
        {
          id: 194,
          artist: 'Kenny Scharf',
          name: 'Hannah Barbaric Paradise (1981)',
          style: 'Graffiti',
          information: 'Mediante su obra de colores estridentes, imágenes simplificadas y blandas quería minimizar la distancia entre el arte y la cultura popular. Sus personajes son extraídos de los dibujos animados, el comic o la mitología llenando cualquier superficie.' +
            '',
          url: 'https://uploads3.wikiart.org/images/kenny-scharf/hannah-barbaric-paradise-1981.jpg',
        },
        {
          id: 195,
          artist: '-',
          name: 'Apropiacionismo',
          style: '',
          information: 'El apropiacionismo convivió en EE.UU. con el Neoexpresionismo y es una tendenci también dispuesta a superar los límites impuestos por la teoría y la racionalidad. En este caso se reivindica la imagen, su lugar en el mundo mediático y su potencialidad narrativa.\n' +
            'La pintura se entendía como un proceso en el que se presentaban todo un mundo de imágenes cuyo origen era la apropiación de otras imágenes. Las imágenes resultantes eliminaban todo el significado de las originales para otorgarles uno nuevo. Su intención no era representar la realidad, si no rehacerla a partir de imágenes preexistentes.',
          url: '',
          title: 'Apropiacionismo'
        },
        {
          id: 196,
          artist: 'Richard Prince',
          name: 'Untitled Cowboy (1989)',
          style: 'Apropiacionismo',
          information: 'Comienza realizando collages con fotografías para acabar en la refotografía (fotografía de una fotografía) para intentar borrar la distancia entre arte y realidad y entre realidad y ficción\n' +
            'Su obra Untitled Cowboy es una refotografía de un anuncio de Marlboro. Este tipo de obras suscitaron la controversia acerca de la autoría, la autenticidad y los derechos de autoría de la misma.',
          url: 'https://www.zoomescuela.com/wp-content/uploads/2020/09/time-100-influential-photos-richard-prince-untitled-cowboy-82.jpg',
        },
        {
          id: 197,
          artist: 'Sherrie Levine',
          name: 'Fountain (Buddha) (1996)',
          style: 'Apropiacionismo',
          information: 'La artista llevó más lejos el trabajo de retrografía apropiándose directamente del trabajo de otros artistas y presentándolo sin modificación ni reinterpretación alguno. Al apropiarse sólo de obras de hombres, se deja ver una reflexión crítica sobre el tema de género en el mundo del arte.\n' +
            'Cuestiona y desmitifica la importancia de la creación original. También se dedic a versionar obras capitales de artistas masculinos del siglo XX.',
          url: 'https://www.thebroad.org/sites/default/files/art/levine_fountain_buddha.jpg',
        },
        {
          id: 198,
          artist: 'Robert Longo',
          name: 'Raphael and Barbara (1998)',
          style: 'Apropiacionismo',
          information: 'Se interesó por las imágenes del cine y la televisión. Se apropió de imágenes de ambos medios y se sirvió del dibujo para convertirlas en fotogramas bidimensionales "congelados" de gran formato. Su serie Men in the Cities aparecen hombres vestidos de traje y corbata en posiciones contorsionadas como si estuvieran siendo disparados. Compone una especie de coreografía dramatizada del instante de sus muertes.' +
            '',
          url: 'https://assets.phillips.com/image/upload/t_Website_LotDetailMainImage/v1/auctions/NY030212/204_001.jpg',
        },
        {
          id: 199,
          artist: 'Jeff Koons',
          name: 'St Johns the Baptist (1996)',
          style: 'Apropiacionismo',
          information: 'Su obra no trata de simular objetos de consumo, si no que pretende reproducir la capacidad seductora que estos ejercen sobre el público. Se posiciona entre la frontera entre el arte y el comercio. Crea obras que entiende y comprende la mayoría del público pero se encuentran fuera de su poder adquisitivo. Tiene un estilo muy cercano a lo Kitsch.' +
            '',
          url: 'https://2.bp.blogspot.com/-7RMkqN8cy4E/VAi7ADVG1fI/AAAAAAAAFK8/xwiTFjBx_No/s1600/Koonsb.jpg',
        },
        {
          id: 200,
          artist: '-',
          name: 'Arte NeoGeo o Neobjetual',
          style: '',
          information: 'A mediados de los 80 comenzó un abndono de las propuestas neoexpresionistas. Los artistas alemanes fueron los primeros en abandonar los postulados expresionistas. Los NeoGeos o Neoabstractos reinterpretaron la Abstracción Geométrica\n' +
            'Los artistas neobjetuales trabajan con objetos "atravesados por la historia" y ponen énfasis en lo cotidiano, lo irónico y lo subjetivo',
          url: '',
          title: 'Arte NeoGeo o Neobjetual'
        },
        {
          id: 201,
          artist: 'Reinhard Mucha',
          name: 'Hagen Vorhalle (1983)',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Mucha crea instalacones y monumentos reutilizando muebles encontrados que una vez concluida la intervención los devuelve a donde los ha sacado. Pone en cuestión los elementos de la forma y la función de los objetos planteando también cuestiones de propiedad. Multitud de referencias autobiográficas y viajes  en ferrocarril muy presentes en su obra.' +
            '',
          url: 'https://galerie-graesslin.de/media/img/exhibitions/Hagen-Vorhalle-2_1983.jpg',
        },
        {
          id: 202,
          artist: 'Tony Cragg',
          name: 'Britain Seen From the North (1981)',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Realiza obra con materiales de construcción, consumo y objetos domésticos deshechados. Planea las esculturas amontonando, rompiendo o aplastando los materiales. En Britain Seen From the North recrea la forma de la isla de Gran Bretaña vista desde el norte donde se encuentra una figura, quizás el propio autor, donde ve al país como un extranjero.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/T/T03/T03347_10.jpg',
        },
        {
          id: 203,
          artist: 'Christian Boltanski',
          name: 'Rezerve: La Fete de Pourim (1988)',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Incorpora la dimensión simbólica al objeto. Utiliza materiales usados como testimonios de la memoria, la vida y la biografía personal (carpetas, fotografías, cartas...). Con ello recrea vidas individuales imaginadas o imaginarias. Usa cajas de galletas de metal oxidado que dispone de diferente forma en función del lugar expositivo y son contenedores de recuerdos individualizados mediante una fotografía de archivo anónima.' +
            '',
          url: 'https://media.mutualart.com/Images/2013_05/14/09/092418936/776a8633-0f80-48cd-bba2-792b1ec76c96_570.Jpeg',
        },
        {
          id: 204,
          artist: 'Rosemarie Trockel',
          name: 'Living Means to Play Some Records (2002)',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Reinterpreta el ready made confrontando el trabajo manual y artesanal y el conceptual. Utiliza la ironía para mostrar su mensaje cuestionando el concepto de autoría y la representación de la mujer en la sociedad moderna. Anticipa las cuestiones de género.' +
            '',
          url: 'https://i.pinimg.com/originals/f6/61/01/f66101ff0e9f7714140630c42266e6fc.jpg',
        },
        {
          id: 205,
          artist: 'Louise Bourgeis',
          name: 'Maman (1999)',
          style: 'Arte Neogeo o Neobjetual/Arte de género',
          information: 'Se dedicó a a crear esculturas e instalaciones transgresoras atraída por nuevos materiales e influenciada por los movimientos feministas. Sus obras se mueven entre la sexualidad, la fertilidad y la identidad de género. Sus obras están a medio camino entre lo formal y lo informe con tintes autobiográficos.' +
            '',
          url: 'https://upload.wikimedia.org/wikipedia/commons/thumb/a/ab/Bilbao_-_Guggenheim_28.jpg/1200px-Bilbao_-_Guggenheim_28.jpg',
        },
        {
          id: 206,
          artist: 'Juan Muñoz',
          name: 'Plaza (Madrid) (1996)',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Juan Muñoz comenzó a trabajar en instalaciones llenas de figuras de un tamaño algo más pequeño que el original que interaccionaban entre ellas y se relacionaban con el espacio circundante. Sus figuras son monocromáticas (gris plomo o color cera) que llegan a incomodar al espectador por su universalidad y su falta de interés por sí mismas. Crea situaciones en las que sus escenografías son de caráter narrativo y obliga al espectador a relacionarse y participar en la propia obra.' +
            '',
          url: 'https://static1.museoreinasofia.es/sites/default/files/obras/AD00608.jpg',
        },
        {
          id: 207,
          artist: 'Jaume Plensa',
          name: 'Julia',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Comenzó trabajando con el hierro hasta empezar con sus célebres cabezas translúcidas a gran escala, realizadas en rejilla de acero inoxidable que parecen desvanecerse ante el espectador. Sus obras se suelen exponer en el espacio público.' +
            '',
          url: 'https://www.revistadearte.com/wp-content/uploads/2018/12/Julia-Jaume-Plensa-Plaza-de-Col%C3%B3n-en-Madrid-20-dic-2018.jpg',
        },
        {
          id: 208,
          artist: 'Anish Kapoor',
          name: 'Cloud Gate',
          style: 'Arte Neogeo o Neobjetual',
          information: 'Empezó con trabajos abstractos realizados con pigmentos que recreaban espacios ambiguos a medio camino entre la pintura y la escultura. Ha investigado tanto con la ausencia del reflejo de la luz, en sus obras con pigmentos y en las esculturas de superficies pulidas que acentúan la sensación inversa. En este Cloud Gate ofrece al espectador otra forma de admirar el Skyline de Chicago.' +
            '',
          url: 'https://www.ecured.cu/images/b/b4/CloudGate.jpg',
        },
        {
          id: 209,
          artist: '-',
          name: 'Arte Neoconceptual',
          style: '',
          information: 'Es un movimiento que se produce paralelamente al Arte Neogeo o Neobjetual. Se interesan en la recuperación del código pero en un sentido diferente al del Arte Conceptual. Toma referencias de Kosuth, Weiner o Kawara (Arte Conceptual) y de Wharhol (Pop Art). Esto les llevó a la crítica social y a cuestionar la obra de arte como mercancía. Este grupo podría ser considerado como activistas posmodernos.\n' +
            'Algunos de los artistas pasaron de ser productores de objetos de arte a manipuladores de signos artísticos. Esto obliga al espectador a ser un lector activo de mensajes. Mensajes dirigidos a la crítica de las representaciones, los estereotipos, la sexualidad o los roles sociales.',
          url: '',
          title: 'Arte Neoconceptual'
        },
        {
          id: 210,
          artist: 'Barbara Kruger',
          name: 'Untitled (We don`t need another hero) (1987)',
          style: 'Arte Neoconceptual',
          information: 'Con una influencia previa en el diseño gráfico, presenta fotografías en blanco y negro a las que superpone frases y textos decorativos y agresivos con letras sobre fondo blanco o blancas sobre fondo rojo. Sus mensajes son claros y directos dirigidos a fomentar la igualdad de género, a luchar contra los estereotipos y a reivindicar el papel femenino tanto en el mundo social como en el artístico.\n' +
            'Más adelante trata temas que van desde el racismo hasta el sexo, el aborto o la libertad religiosa.',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwva3J1Z2VyXzIuanBnIiwicmVzaXplLDgwMCJdfQ.P0xcsjf89Q5qKrDNCCYVod853PBrHzlbNwwDPA87Ccc.jpg',
        },
        {
          id: 211,
          artist: 'Jenny Hozler',
          name: 'Projections (2009)',
          style: 'Arte Neoconceptual',
          information: 'Se sirve de estrategias publicitarias para proyectar textos en el espacio público en los que formula denuncias, críticas y demandas sociales. Recurre a la ironía y a la supuesta banalidad para reformular diferentes problemas sociales.' +
            '',
          url: 'https://4.bp.blogspot.com/-h5Y4yMEu9WQ/WfrwP8f2AJI/AAAAAAAAkmc/KKwy09RUmVkN8Rb-33zHkGRwGHtRBlu2wCLcBGAs/s1600/JENNY-HOLZER-14.jpg',
        },
        {
          id: 212,
          artist: 'Adrian Piper',
          name: 'Catalysis IV (1971)',
          style: 'Arte Neoconceptual',
          information: 'Sus trabajos conceptuales intentan plantear desde su posición de artista afroamericana, las situaciones raciales de la época, la construcción de la identidad o la xenofobia.\n' +
            'En Catalysis IV se introduce un pañuelo blanco en la boca dejando que sobresalga parte del mismo y toma un transporte público obligando al resto de pasajeros a afrontar una situación anormal concebida como protesta. Sus obras actúan como un catalizador que desafía el orden social',
          url: '',
        },
        {
          id: 213,
          artist: 'Damien Hirst',
          name: 'The Physical Impossibility of Death in the Mind of Someone Living (1991)',
          style: 'Arte Neoconceptual',
          information: 'Hirst es uno de los artistas más influyentes del mundo. En sus obras presenta animales suspendidos en formol dentro de una vitrina. En esta expone un tiburón tigre.' +
            '',
          url: 'https://www.plataformadeartecontemporaneo.com/pac/wp-content/uploads/2012/04/Hirst-The-Physical-Impossibility-of-Death-in-the-Mind-of-Someone-Living-1991.jpg',
        },
        {
          id: 214,
          artist: 'Gillian Wearing',
          name: 'I`m Desperate (1992-1993)',
          style: 'Arte Neoconceptual',
          information: 'Utiliza la fotografía y el vídeo para grabar confesiones de la gent común, mostrando las diferencias entre la vida pública y la privada y entre la experiencia individual y la colectiva.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/P/P78/P78348_9.jpg',
        },
        {
          id: 215,
          artist: 'Tracey Emin',
          name: 'I Have Ever Slept With (1963-1995)',
          style: 'Arte Neoconceptual',
          information: 'Presenta un gusto por la notoriedad y el escandalo del grupo YBA, pero se interesa por mostrar su propia intimidad. Su obra consiste en una tienda de campaña adornada con los nombres de todas las personas con quienes alguna vez durmió, ya sean familiares, amigos o gente con quien mantuvo relaciones sexuales.' +
            '',
          url: 'https://upload.wikimedia.org/wikipedia/en/b/b9/Emin-Tent-Exterior.jpg',
        },
        {
          id: 216,
          artist: 'Liam Gillick',
          name: 'Annlee You Proposes (2001)',
          style: 'Arte Neoconceptual',
          information: 'Desarrolló sus primeras obras con un método de trabajo con el que cuestionaba desde los problemas que plantea la arquitectura hasta los procedimientos de recopilación de noticias. Su trabajo es reconocido por el uso de pantallas, construcciones y plataformas translúcidas de diferentes colores que funcionan como metáforas de lugares de discusión. En este caso, el artista incluye su obra en la tradición conceptual de presentar el arte como una actividad para la comunicación y el intercambio de ideas.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/T/T07/T07901_10.jpg',
        },
        {
          id: 217,
          artist: 'Cildo Meireles',
          name: 'Abajur (1997-2010)',
          style: 'Arte Neoconceptual',
          information: 'Sus objetos o instalaciones conducen a la ampliación de la experiencia sensorial del espectador. En sus obras y esculturas ofrece un ambiente rico en cuanto a la percepción del tiempo y del espacio. Cuestiona desde los asuntos políticos y sociales de su país hasta los generados por el propo arte.' +
            '',
          url: 'https://lh3.googleusercontent.com/9SAy3xT4Ihq_8-sKGi7ThzBy9FDJyD4h1lOwFMSMXGUoVoSQWJO0pT2ng6iE_2O_vA=s1200',
        },
        {
          id: 218,
          artist: '-',
          name: 'Arte activista, político y alternativo',
          style: '',
          information: 'En el contexto mundial de líderes conservadores como Ronald Reagan y Margaret Thatcher se inicia un movimiento de arte postmoderno activista. Sus raíces se encuentran en el arte político de los años 60 y 70. Este nuevo arte activista no dirigía sus mensajes tanto a la lucha de clases, el belicismo o al racismo como a la crítica de las representaciones, los estereotipos étnicos, la sexualidad y los roles sociales. En norteamérica hay un mensaje contra la implicación de Estados Unidos en la Guerra de Vietnam.' +
            '',
          url: '',
          title: 'Arte activista, político y alternativo',
        },
        {
          id: 219,
          artist: 'Martha Rosler',
          name: 'First Lady (1967-1972)',
          style: 'Arte activista, político y alternativo',
          information: 'Emplea técnicas de fotografía, fotomontaje y video. Las series de Bringing the War Home, consta de una serie de montajes fotográficos que pretende llevar la guerra al espacio doméstico. Para ello combina imágenes procedentes de diferentes medios como la publicidad en revistas para mujeres, la pornografía y las imágenes documentales de la guerra. Difunde su obra a través de folletos y periódicos.' +
            '',
          url: 'https://www.moma.org/media/W1siZiIsIjIzNDI3NiJdLFsicCIsImNvbnZlcnQiLCItcXVhbGl0eSA5MCAtcmVzaXplIDIwMDB4MTQ0MFx1MDAzZSJdXQ.jpg?sha=a8abb56ecfe2fedds',
        },
        {
          id: 220,
          artist: 'Nancy Spero',
          name: 'Paz, helicóptero y Cristo colgado (1968)',
          style: 'Arte activista, político y alternativo',
          information: 'Nancy Spero se interesó por los movimientos antibelicistas desde el arte y por el papel de la mujer en la sociedad del momento hasta que la reivindicación de la mujer en el arte y la política pasa a ser su único objetivo.' +
            '',
          url: 'http://2.bp.blogspot.com/_sD9yQTE5QZQ/SwL2BMCBlQI/AAAAAAAAHnM/sP9Cdd2--lw/w1200-h630-p-k-no-nu/Spero8.jpg',
        },
        {
          id: 221,
          artist: 'Alfredo Jaar',
          name: 'The Eyes of Gutete Emerita (1996)',
          style: 'Arte activista, político y alternativo',
          information: 'Forma parte de su Proyecto Ruanda, que busca hacer reflexionar al espectador sobre el genocidio acaecido en ese país. Los ojos de Gutete Emerita, muestra la mirada de una víctima del conflicto de Ruanda. Los pone ante los ojos de un testigo del asesinato de su propia familia y nos está mirando a nosotros. Esa interpelación nos hace cómplices de lo que ha vivido.' +
            '',
          url: 'https://revistacolibri.com.ar/wp-content/uploads/2018/08/the-visual-politics-of-rwanda.jpg',
        },
        {
          id: 222   ,
          artist: 'Krysztof Wodiczko',
          name: 'Hirshhorn Museum (1988)',
          style: 'Arte activista, político y alternativo',
          information: 'Wodiczko ha realizado numerosas proyecciones de video o fotogradías de escala enorme sobre los muros de edificios y monumentos de todo el mundo. Con estas proyecciones invita a reflexionaar sobre las contradicciones del propio lugar. Él mismo lo denomina arte público crítico\n' +
            'Esta obra es un videomapping que habla de algunos dirigentes evangelistas americanos que por un lado defienden el derecho a llevar armas y a defenderse pero a la vez llevan la palabra de Dios y sirven de amplificadores de ella. Convierte este edificio en una especie de persona. Existe una dualidad ya que a pesar de ser una religión y llevar la palabra de Dios muchas veces se alía con el poder para dirgir o defender matanzas a unas minorías.',
          url: 'https://news.artnet.com/app/news-upload/2018/01/Wodiczko-Hirshhorn-Museum-1024x773.jpg',
        },
        {
          id: 223,
          artist: 'Félix González-Torres',
          name: 'Sin Título (Cama) (1991)',
          style: 'Arte activista, político y alternativo/Arte de género (masculino)',
          information: 'Artista visual de origen cubano que realiza instalaciones mínimas, efímeras y técnicamente sencillas en las que invita a reflexionar sobre la construcción de la memoria colectiva y personal. En esta obra, colocó en vallas publicitarias de NY la imagen de su cama vacía con el rastro de dos cuerpos ausentes tras la muerte de su propia pareja por SIDA. Su trabajo a pesar de ser muy autobiográfico, es un reflejo de lo problemas de la sociedad.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvNWM2N2ZiNTVjYWU1My5qcGciLCJyZXNpemUsODAwIl19.3GTpyAxmA0JptGCBi5t5GiBlwRbrCRDc5OHDH5q-Bs8.jpg',
        },
        {
          id: 224,
          artist: 'Guerrilla Girls',
          name: 'Billboard for the Public Art Fund (1989)',
          style: 'Arte activista, político y alternativo',
          information: 'Este colectivo de mujeres artistas anónimas lleva trabajando desde 1985 en el activismo feminista. Denuncian la discriminación de la mujer y la corrupción del arte, el cine, la política y la cultura. Mediante talleres, ruedas de prensa, conferencias, performances, siempre cubiertas con una máscara de Gorila.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/P/P78/P78793_10.jpg',
        },
        {
          id: 225,
          artist: 'Santiago Sierra',
          name: '3000 huecos de 180x50x50cm cada uno (1992)',
          style: 'Arte activista, político y alternativo',
          information: 'Trabaja la crítica social y política de una forma muy cruda. Utiliza estrategias espectaculares y controvertidas, pero muy eficaces. En sus acciones roza el límite de lo aceptable, llegando a convertir una sinagoga en una cámara de gas o tatuar una línea de 2,5 metros sobre 6 personas remuneradas.\n' +
            'En este casó, contrató a inmigrantes del estrecho para cavar 3000 tumbas que luego se quedaban vacías. Cavaron 3000 tumbas, un número correspondiente al número de personas que perdieron la vida en el estrecho en una serie de años. Es tan interesante el resultado final como el propio proceso.',
          url: '',
        },
        {
          id: 226,
          artist: 'Kara Walker',
          name: 'Grub for Sharks: A concession to the Negro Populance (2004)',
          style: 'Arte activista, político y alternativo',
          information: 'Explora en su obra la identidad de raza, género, la sexualidad y la violencia. En esta obra nos muestra tras una aparente ingenuidad de piezas recortadas y pegadas sobre la pared, los momentos más olvidados y duros de la esclavitud. Temas como el abuso (algunos de ellos sexuales) o la violencia eran elementos más que cotidianos para ese colectivo.' +
            '',
          url: 'https://www.tate.org.uk/art/images/work/T/T12/T12906_294055_10.jpg',
        },
        {
          id: 227,
          artist: 'Nikki de Saint Phalle',
          name: 'Hon-en Katedral (1996)',
          style: 'Arte de género (femenino)',
          information: 'Es una de las obras más emblématicas del redescubrimiento femenino. Se trata del cuerpo de mujer más grande representado en la Historia del arte Contemporáneo. Ese cuerpo se encuentra tendido y con las piernas abiertas pudiéndose acceder a su interior por la vagina y recorrer los diferentes espacios.' +
            '',
          url: 'https://womennart.files.wordpress.com/2018/08/imagen2-hon1.jpg?w=584',
        },
        {
          id: 228,
          artist: 'Judy Chicago',
          name: 'Dinner Party (1979)',
          style: 'Arte de género (femenino)',
          information: 'Instalación que consistía en la recreación de una cena imaginaria para mujeres célebres. La mesa tiene forma de triángulo. El nombre de las invitadas aoarecen en las 999 baldosas y en los 39 manteles. En cada mantel hay una copa, un cubierto y un plato con vaginas de formas diferentes.' +
            '',
          url: 'https://historia-arte.com/_/eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpbSI6WyJcL2FydHdvcmtcL2ltYWdlRmlsZVwvNWU2MzgyY2EyNWZkNS5qcGciLCJyZXNpemUsODAwIl19.5_nsLnMuygEoRj__qVUwkvIaiKZPawtblHweDm71YMk.jpg',
        },
        {
          id: 229,
          artist: 'Mary Kelly',
          name: 'Post-Partum Document. Document IV (1976)',
          style: 'Arte de género (femenino)',
          information: 'Esta obra aborda la relación madre/hijo en el contexto de las teorías psicoanalíticas del desarrollo evolutivo de Jaques Lacan' +
            '',
          url: 'https://www.researchgate.net/publication/290233114/figure/fig5/AS:669036182511624@1536522064334/Mary-Kelly-Post-partum-Document-Documentation-IV-Transitional-objects-diary-and.png',
        },
        {
          id: 230,
          artist: 'Sophie Calle',
          name: 'Les Dormeurs (1979)',
          style: 'Arte de género (femenino)',
          information: 'Transfiere actos y vivencias íntimas y personales a diferentes registros impersonales (textos, fotografías o películas). En esta obra invita a personajes anónimos que encuentra en las calles de París a dormir en su propia cama transcribiendo sus impresiones y conversaciones de forma fría, sin emoción alguna.' +
            '',
          url: 'http://www.artnet.com/WebServices/images/ll00161lldjQ5GFgVNECfDrCWvaHBOcvSDE/sophie-calle-les-dormeurs---patrick-x-(in-9-parts).jpg',
        },
        {
          id: 231,
          artist: 'Cindy Sherman',
          name: 'Sex Pictures. Sex Dolls. Untitled #250 (1999)',
          style: 'Arte de género (femenino)',
          information: 'En sus primeras obras trata de reglejar los estereotipos femeninos de la época. En posteriores trabajos se presenta a sí misma como objeto de voyeurismo. Arte obsceno y abyecto con un potente mensaje' +
            '',
          url: 'https://robtownsendgm.files.wordpress.com/2016/04/untitled-250.jpg',
        },
        {
          id: 232,
          artist: 'Zoé Leonard',
          name: 'Vagina I (1992)',
          style: 'Arte de género (femenino)',
          information: 'Utiliza fotografías en blanco y negro para denunciar el papel femenino en la sociedad occidental. En esta Vagina I se apropia de de la obra de Coubert para colgar imágenes de vaginas entre retratos pictóricos de damas de la alta sociedad del XVII colgados en un palacio barroco. Pretende mostrar la "verdadera" exhibición del cuerpo femenino frente a las representaciones tradicionales.' +
            '',
          url: 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wCEAAkGBxMTEhMTExIVFRMVGBcVGBcVFxUXFRUVFRUWFxUVFRUYHSggGBolGxUVITEhJSkrLi4uFx8zODMtNygtLisBCgoKBQUFDgUFDisZExkrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrKysrK//AABEIAKsBJgMBIgACEQEDEQH/xAAbAAACAwEBAQAAAAAAAAAAAAACAwEEBgAFB//EAEMQAAEDAgIGBwQGCQQDAQAAAAEAAhEDITFBBAUSUWFxBiKBkaGx8BMywdEHI0JykuEVQ1JTYmOCsvEUJDNzg6LSVP/EABQBAQAAAAAAAAAAAAAAAAAAAAD/xAAUEQEAAAAAAAAAAAAAAAAAAAAA/9oADAMBAAIRAxEAPwD55CKEYai2EC4RsapDU2m2yAAxOaxEAihAvZTKbVDQnUm4II2E+k1TFwE0BAtzLo6DLwR2/BcwYyn6OLHw5IOFIplOlCbMJrWzz3IKr2X+HzRMYZwn5IyIM8fQRUBBMYfFA0MRbCbSAzThHBBXdTtOHxUhh3Jj2+HkiAmIQcGIDTVkNQoFhiRo/uj1mm6a4hhjGwHMmAvP1RpzWgtrvAcMnNcLZYdqD0YshhJqa4ofvKfe9I/TVCR9dSj+q6C+GqCFTdruhP8Ay0vxO+SX+maV/raX4j8kF6J+Ch7bLzXa8YMKlI/1H5JZ18P2qUffPyQemKaTVZHJUHa9H8v8f5JL9eAmSG23PCD0HAdhXPpRZeb+n/4Wn+tqWekP8sfjCC+WHcqlen1xG4/BVna/x+rH42qvV1qSWkNAxHvDxhBcqNUqaFQua1wAgjn4qUHkEJjMF0T2I2XQQ1k3RsF0UqY5oAKdTwKGJTWtJ/LBBDac3ITaYgwpmICJzYuM8fyQA8GdxT6OHJLc2Y4J9Ns4YesSg4NnLd+asNEOAGByz5qJgRifWCPZwIxQDVndG5N0Mb0LpIjDn6wR0hNhhhA+aApLsrX5lEGwBHjmiENnf4diY1sjiMIQS5pwyRNZB3/mubMX/LsTW+uSDnTMAetyNtOAeCKmyPFMbeRFkEAkjBIIurEHd64oC3O3BAFQwGH+Nlv6gvG6W050gGP1be8k2XuPYeqf4mcB7wXl9IGzXAcf1bbfiQZU6PNosLDv8Fn9ZUBtmcMuXBafSXbOdzfsWe1kJLgN/qEHkVeWHwVdysVHC2W/mkbOKAFEKSoKASulTCgoOlEShKhBO0Vs/o40VtV9fbAOy1hG1eOvksWtx9Ftq1UHNrf7kGj0zQ4qPaIABiAuVzTHN9rU+8VyDKubxlOpCyAiCbWKdSYgj2aY1qAv705qBWzxkqxo8QbJG1BMZqxQbnv9WQH7IJoalGsO1PFxZBX2YMTJlWtFcL7/AAKrF8EkDH1ZWdHp57/hkEDm0ge1OptiFXdXiysUzIQLe2Dd0k+oTtGgGIvfDhjKS90O2s8DuTtFE9bs5T8UB1KU3iU+jRgerIHVA1O0d8oOfTvc8giC52XBGGz68EDWslMZS7EO1s44pjKslBz2SI70nZ7QrLxYpANgIQFk2P2mf3BeH0lI/wBSwZmm2/C9l72xAb95vms90jg6QP8ArYPAlB4+l0gTOWMrM6ys4/LxWs0ho7F4GsqDTfsQZypRGM5pVQAk3V6pSEgDeqml6OQTayBNOi5xholKqMIJBEEKzTpuDcSJIMibqK+jFtyZzQVULkZQkIOa0lSwXV2lRhvFd7IYlAplHMrZ/RwPrqn3B/csqFrvo5H11X7jR/7INJp1Imo4i4lcrNaoA4j1ioQZgCwXNEGEbsUQZKBDm34puzY3uohNZTmDlw38UEsZIC6nIMZYduSJ5vn2JgbMn0bbkFZzIPHf+at7EAybnwSQOEZhNp0y6DNtw3oDpCzbKWjZdjb54KHG4x7FYDdq/rkQgrV25nHeL/4Vui0gSXXIjwSAwXEQO4SjpMLhjEY7+aB2je6fQTHDZMg43QPOA+SczrRvG/FB1YSJxzEfFN0UWBnApOBI7CRZOpCeqMkD6WJTHDMIWCLJgKCZkeaKgDhhxQlsJtM+KBjxhdS5kyuY0g3UNfdAJfhN+s3tusz0jqD24v8AYZ5LS122B/iHnksd0ucRpIj90ztMIKOl3EA24c15ukts7w+aeJ4/BUNKeR4oPMLTljKVVm5JurdKnJMZoatJBZ1DpDdsBw6vHCVf6UNoub1AARBMDevF1RX9lUNgRmDuyV/WlZ3sW0zF4w4XxQZohQAmlC0XQXGlO2ZEoTTK4OtCAQFr/o7b9bV37Lf7issAtZ9HY+srHg3zKD2dIf13Te57FyZUGy9xiQd3xUoPIAR7Xl5JJcmtda6A9GpNddzo7JkkTCtN0QZE9w+a7VQEu3SsjrXpLU9uWsJDQ6NmwuDF+aDXHRwASDgN2N0s27kw1fqpwJbPI2SWm0lADTaY2jinUSItmkNacvdPwVnR3jtHcEDQ2+5N4qk6tBmeStUTLb9/zQCySCYk7sscOxM0VodcCDcHsyStg/ZwwMWuVa0Iw6LSJsOSCyzRbYnu/NF7CBMm18FmulGvqlKzSWyYEXJjE4L1NQ6bUqMLnODmxAIxwvKC06dojGDHDCUejwThBEepQ6QOuYxmexTRMe9ifFBbYM0yEiU5pQGXYckbQJgjklkJlOZkoHrguSjU70E6UYH9TfNYvpUZ0mf5bPJbTSMBzCwfSqpGk/8AjZ5IKD3rztKurT3FedXddAJcJtYlIqOxAucYSqj4wOCsaE6DtRM9UkccZKDtTaC+rUmLYFbZ+pWvpBpAAbcJWg6O1jA4brr1NFrtLZc6BzQYXWPRttNpeHw2YAO84LPOYWug4grba80thcxo6w2pvnC8DWWiB7j7MTB44IBclOp5pbnltjY7s0NOoTKCZg45LY/RxUBfW4BvmVhtLmRuWw+jZ1tI47PxQaqoGkmXhvDmpS6zw+BGGe9Qg8iESCUbSg9HVjQdocPgV801w0jSHu3vJHYV9D0WdlwESSBiBHFLqdG9Gc1wf1nuJJftCQT+zuHBAOrtI26AJN4EntCKcss53pGrtCdSpva6IwBkGRtC8DgrVMWQGABGUZc1zDBM+gh2SdyZsgi4lAoi4jxyVoCxAzNzkIVemcbK5RZ2oGU2AAZZp9Fv1k8CR3KqQT6urFOYJAlwa6BvMWAQYv6QqpZVpxGbh4A2VvoHrF2waRgAAkEY9Y5ptHotW0t/tdMc6mMBTaJcB97AJVfofW0aq2poznVGFwBaWw4NkTJwNkGwqMG088SFDsjku0n3ncz6CiibQgc2E5oVcKywIJbinA2SwiYUDNoGLpTcVLgglAelOsIy+RXz7pfWjSj/ANdP+1b/AEv3O34FfL+ntWNLP3GeSBH+qkcVUrOkwLk7vILz/bnem6JXhwJMRmg9L9DOi+yJv71+WyEVUFtEj2ZEEEuNohMZWnB0CMjirVPRmVQaba0OeI2Xe6TkZyKCq7XrvZwCN3GFWZrNxAE235rz9Y6BU0d5ZUaRuIwI3tOaOjAjD8kDKtQvrMG8gdp4rStZRoTYiTEgkm2NlnNGIbWa5x3gc4s7vVjR6v1jWPMgiJnObzxQdr2mHu9o0HIHszXm02wLYyfJabXuhmnS6riabsP4TjHI3WSqVCLGyA9NdwWt+jr3K/NvkViHPlbPoCfqq3FzfIoN1o4gGQO7guVSk83v3rkHhIqaCVKBhKJqSmNQEM0ymlwjpuQWAQjaVTlPD7GyCW+8ZPJWKGfH1KqgSQrFJ+RQWgQOxEXYEFU5VinUtyCAto7UEwPNGxxnE4cewJMTfBMpuixQPARgzh6Krko6bkD01jkhjpTAUFlS0pbXyiQSSoQufCjaQRpbuqPWRXy7pyJ0t33WeS+m6a/qz6wK+V9ODOlv5N8kHjvo4QUylowtJVcAplFhJxQNa4gub3J+rK2yHktJGTh9l2So1iQbm6mhp72AhriAbkWieRQabSdcsr0gyqBtAYkZj9k4gledU0BrWbdOsxxAktgh44bikaNrVsdek0neAL8wUzWGthV2WCm2m0Yxj/hBW0oyZ7huRO0r2jw50B0gdWwOU81XeYkG/FL2M5Qal+kl9KrQcQXAbTCftbNx4LMGqMwRw+Ss7Ymd0Dim6Q8PBl0kABpMQBxQeQ/GwgLZ9BDFGt94eSx9WnELY9B7Uah3vjwag3HswuVenXLiSButuXIM/KkFIBRhyBqYEoOUtKBykIVIQEjlACjCA22ITYvKQrDEBJu2lAIwgaDAjFG+6SmMMIDRBAHIggJpVgKsnNqBAxpTC/gkNeilBJXSgNRR7RAGnu6vf5FfMemR/wB2/k3yX0fWb+r63FfM+lbv90/hHkgoCkcoJz+CKhbH81NDSi11gL5qy11RxMgGcQIEzuQebpTpKUAjrtIcZtfA4oqVOQg6kyROe7yROGE4EIqLIJRSMCLoGNHVE9p4HBLqUx9kygdhKBA2sSM0oViMbrglvQG6pIjjK1/Qx0UXff8A/lYuVseiv/BzqfJBrNGaLyRuxXIatQjAQpQeE0LpUsdvxUZz6KBkIpSS5HOCBgKaHJTTmpab3QORsSmuRtKBgTWOShvRNQWAUbTZJDkc2QNBU7SCmiJQNZgmBImMCjYZmUDFKClzRoDa63apcbXF0vKZXbclBClDmiQUdbO6ovn8CsDr3ZNeptCTzjJbvWjZA5/BfOtfVP8AcVRODiJ3wgW2vse6B2381afrURBiCMADIXlbQS3FBY0rS9v7PacUqhVi2SUVLDdBeomZk3yt4JVQ3BQNfxRioIQC42SoXSolAUoXhSHKCUALadFB9Sz/ALPisWtn0VE0mX+14yUGsrPcDA6w5YcFC4NIEgzK5Bn4wQvegGA3+Smrl65IGsKJpVYFG1yC0FJKUHYcVJQPYjDlWD0YKC00myZKr7WCY84IHsRAjNVw9GSgssd2o5jmkNd2InYTPYgsNuiDgDwVQVkQqSgugickUhV6VW0AYYlRUJIsZCBz3zZc4xCqNqx2qH6RKC04DL12Ituc1TpVYPFNDuxAvT2EhuyMDlyR6uY1jYdSkkzJDYPYobUT21EEtZT/APzt7Q35qP8AS0z+oZ+EfNMa5NDkFcaBS/cU/wAH5rjoFPKhT/B+attejBQedU1c0fqWfhSn6sblSZ+FextpLjxug8g6rH7pn4SlVdVfymdy92mVDhOfcgzz9T2n2TOUKtU1RI/4mdy1MQqleZkkDIIMydUO/dMHrcppase10hkCWmxjDGy0TIBznwKCvffHBAB6wxIXIdgjjzXIM4HxYLntzmQlVMSmUvdKB7Rbih2b811E2KU03QWWuAspf5pLsSmfZQOYF2fNRRNkIN0DwRgjeUh+Kc33e5A6my0ribomhA5xkDigcDkVL3YBLPvJlK7T6zQFTpyFFSxsipHyUVzbuQMpOxmwKE1YkJb3XATQwTggULoHiAiZYmN/wRVBdANF900COKrNPVTKF+5AYdKc1qR9qFaiyA6bk8FVmi5TaZQWAUwOSGI0DSlkwVxKhBDVBqgIKTrwlPxQWC+yp13XmP8AKMuvHBJBkHmg4XM8+9c94FkqYcUrTMkDm1VypveQBC5B/9k=',
        },
        {
          id: 233,
          artist: 'Tania Burguera',
          name: 'El Peso de la Culpa (1997)',
          style: 'Arte de género (femenino)',
          information: 'Encarna la actitud feminista política reacia a las prácticas intimistas. En esta acción, la artista comió tierra ligada con agua y sal llevando un carnero muerto colgando al cuello, enteramente desnuda delante de una bandera cubana hecha con cabello humano por ella misma.' +
            '',
          url: 'https://d32dm0rphc51dk.cloudfront.net/7pM9pEOFOrjEkQXjn7MZJw/large.jpg',
        },
        {
          id: 234,
          artist: 'Robert Gober',
          name: 'Untitled (leg) (1989-1990)',
          style: 'Arte de género (masculino)',
          information: 'Crea escultura reproduciendo objetos domésticos y familiares como modelo (puertas, urinarios, lavabos...). Sus obras son meticulosas y artesanalmente realizadas. No sólo reproduce estos objetos sino que establece conexiones entre ellos y el cuerpo humano a través de los nombres de las piezas.\n' +
            'Más adelante empieza a trabajar directamente con partes de anatomía humana, piernas o torsos modelados en yeso, cera y pelo natural. Al colocarlos colgando del techo o entrando en las paredes acentúa la sensación de violencia y de exclusión.',
          url: 'https://www.moma.org/media/W1siZiIsIjY2MjE0Il0sWyJwIiwiY29udmVydCIsIi1xdWFsaXR5IDkwIC1yZXNpemUgMjAwMHgyMDAwXHUwMDNlIl1d.jpg?sha=3b66416006226fc2',
        },
        {
          id: 235,
          artist: 'Mathew Barney',
          name: 'Cremaster (1994-1997)',
          style: 'Arte de género (masculino)',
          information: 'Se interesa por la anatomía y los cuerpos representando seres inexistentes, a medio camino entre lo masculino y lo femenino o entre lo biológico y lo mecánico. En sus videos-performances se transforma en animal mitológico o se traviste de mujer en un ambiente complejo y extraño.' +
            '',
          url: 'https://www.alejandradeargos.com/images/Matthew_Barney/15_Cremaster_2.jpg',
        },
        {
          id: 236,
          artist: '-',
          name: 'Arte Relacional',
          style: '',
          information: 'Término acuñado para distinguir el arte de los 90 del producido anteriormente. Estos años, la sociedad se enfrentaba a tres coyunturas: la caída del muro de Berlín, la rápida y masiva implantación de los ordenadores y la aparición de internet y los desarrollos propios y cuestionamientos sociales de la propia práctica artística.\n' +
            'Las relaciones personales sufrían de crisis y aislamiento, por lo que la imperiosa respuesta de algunos artistas consistió en generar propuestas que tenían como rpemisa las relaciones humanas, el encuentro, la proximidad y la interacción. Lo relacional está ligado a la acción, por eso se encuentra una hibridación entre las artes plásticas, la música y la danza, cine o teatro.',
          url: '',
          title: 'Arte Relacional',
        },
        {
          id: 237,
          artist: 'Rirkrit Tiravanija',
          name: 'Pad Thai ())1990)',
          style: 'Arte Relacional',
          information: 'Este artista realica instalaciones donde invita a los espectadores a compartir la experiencia de comer, cocinar, leer o escuchar música. En este caso invita al público a participar de la comida tradicional tailandesa sirviendo comida a todos los asistentes. Pretende crear la estructura para el intercambio, la interacción y la socialización' +
            '',
          url: 'http://www.zoilus.com/rirkritTiravanija.jpg',
        },
        {
          id: 238,
          artist: 'Vanessa Beecroft',
          name: 'VB46 (2011)',
          style: 'Arte Relacional',
          information: 'Trabaja en el arte de acción implicando a modelos femeninos medio desnudos con el público participando. Así incita a la provocación y el voyeurismo mostrando mujeres cosificadas, desnudas y unificadas a través de un hilo conductor que permanecen inmóviles e inaccesibles mientras los espectadores las observan. Cada acción intenta que contenga elementos y problemátias socio políticas específicas del lugar donde se realiza la obra. Los vídeos y las fotografías de la preparación de sus acciones sirven tanto de documentación como de obra autónoma' +
            '',
          url: 'https://i.pinimg.com/originals/c5/56/2d/c5562d46d98c329cb665c307c8ab5b26.jpg',
        },
        {
          id: 239,
          artist: 'Maurizio Cattelan',
          name: 'La Nona Ora (1999)',
          style: 'Arte Relacional',
          information: 'Su trabajo se burla del orden social establecido a través del humor negro y la ironía, con lo que consigue establecer relaciones de complicidad con el espectador. En La Nona Ora, la escultura realista del Papa Juan Pablo II es aplastada por un meteorito. Delante de la figura aparecen unos cristales rotos que simbolizan la fragilidad de la vida' +
            '',
          url: 'https://farmacon.files.wordpress.com/2015/09/la-nona-ora.jpg',
        },
        /*
        {
          id: 2,
          artist: '',
          name: '',
          style: '',
          information: '' +
            '',
          url: '',
        },

        */
      ]
    }
  },
  methods: {
    getRandomArt() {
      this.solved = false;
      this.artList = this.artList.map(a => ({ sort: Math.random(), id: a })).sort((a, b) => a.sort - b.sort).map(a => a.id);
      console.log(this.artList);
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
