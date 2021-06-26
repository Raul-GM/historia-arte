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
        /*
        {
          id: 8,
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
