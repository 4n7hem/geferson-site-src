<template>
  <div>
    <header>
      <img class="logo_main" src="~/assets/geferson.png" @click="clickLogo()" />
      <nav>
        <div class="container_botao">
          <ul class="botoes">
            <li><a class="text-white header-menu" href="#"> Login </a></li>
            <li><a class="text-white header-menu" href="#"> Contato </a></li>
          </ul>
        </div>
      </nav>
    </header>

    <div class="container_body" v-if="!hideSearch">
      <img
        class="main_logo"
        v-if="this.showLogo"
        src="https://i.pinimg.com/originals/a0/6f/e2/a06fe237110e6da70fefe36b99f3c681.gif"
      />
      <input
        type="Search"
        placeholder="Procure por seus filmes, séries, animes...."
        v-model="search"
        name="Search"
      /><br />
      <button class="button-pesquisar" @click="buscar" id="submit">
        Pesquisar
      </button>
    </div>

    <div class="respostas_container" v-if="notSelected">
      <ul class="respostas">
        <li
          class="item-frame"
          :key="item"
          v-for="item in this.valores"
          @click="queryDoSelecionado(item)"
        >
          <img class="thumbnails" :src="item.image" />
        </li>
      </ul>
    </div>

    <div class="movie-details" v-if="hideSearch">
      <button class="button-voltar" @click="voltar" id="submit">Voltar</button>
      <div class="details-row-1">
        <h1 class="movie-title">{{ currentMovie.name }}</h1>
        <div>
          <div class="container-streamings">
            Disponivel em:
            <div class="streamings-logos">
              <div
                class="m-2"
                v-for="(streaming, index) in currentMovie.streamings"
                :key="index"
              >
                <img class="streamings" :src="`${streaming}.png`" />
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="content-center">
        <img class="thumbnails" :src="currentMovie.image" />
        <div>
          <div
            class="flex-1"
            v-for="(value, key) in currentMovie.rates"
            :key="key"
          >
            <img class="streamings" :src="`${key}.png`" />
            {{ value }}
          </div>
        </div>
        <div >
          <h1 class="titulo_comentarios">Comentários</h1>
          <div class="linha"></div>
          <div class="card_comentario"
            v-for="(commentary, index) in currentMovie.comments"
            :key="index"
          >
            {{ commentary }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
function goToResultado() {
  this.$router.push("./resultado");
}
export default {
  data: () => {
    return {
      search: "",
      valores: [],
      pirarucu: "",
      showLogo: true,
      notSelected: true,
      hideSearch: false,
      currentMovie: {},
      database: [
        {
          name: "narnia",
          streamings: ["netflix", "amazon", "hbo", "disney"],
          rates: {
            imdb: 8,
            rotten: "79%",
          },
          comments: [
            "Neque porro quisquam est qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit...",
            "Lorem ipsum dolor sit amet.",
          ],
          image:
            "https://br.web.img3.acsta.net/medias/nmedia/18/90/59/44/20103781.jpg",
        },
        {
          name: "narnia",
          image:
            "https://http2.mlstatic.com/D_NQ_NP_975889-MLB44424533206_122020-O.jpg",
        },
        {
          name: "joker",
          image:
            "https://i.pinimg.com/736x/fe/e7/ea/fee7eab62f787cf7bbd3aa3cce3ac833.jpg",
        },
        {
          name: "dora",
          image:
            "https://img.moviepostershop.com/dora-and-the-lost-city-of-gold-movie-poster-1000779403.jpg",
        },
        {
          name: "avengers",
          image:
            "https://cdn11.bigcommerce.com/s-ydriczk/images/stencil/608x608/products/88997/93196/Avengers-Endgame-Final-Style-Poster-buy-original-movie-posters-at-starstills__42370.1563973516.jpg?c=2",
        },
        {
          name: "pantera negra",
          image:
            "https://www.washingtonpost.com/graphics/2019/entertainment/oscar-nominees-movie-poster-design/img/black-panther-web.jpg",
        },
        {
          name: "pulp fiction",
          image:
            "https://cdn.shopify.com/s/files/1/0057/3728/3618/products/950e439404c3d5eddd86ae876cec83bf_949b5045-2503-4883-bcd2-ff1f31f5b14c_240x360_crop_center.progressive.jpg?v=1573588746",
        },
      ],
    };
  },
  methods: {
    clickLogo() {
      this.showLogo = true;
      this.notSelected = false;
    },
    buscar() {
      this.pirarucu = "_nuxt/assets/placeholder.png";
      this.valores = this.database.filter(
        (movie) => movie.name === this.search
      );
      this.showLogo = false;
      this.notSelected = true;
      if (this.search === "") {
        this.valores = this.database;
      }
    },
    queryDoSelecionado(selectedMovie) {
      this.currentMovie = selectedMovie;
      this.notSelected = false;
      this.hideSearch = true;
    },
    voltar() {
      this.showLogo = true;
      this.hideSearch = false;
    },
  },
};
</script>

<style scoped>
.logo_main {
  @apply cursor-pointer;
}

.container_botao {
  display: flex;
  align-content: center;
  align-items: center;
  flex-direction: row-reverse;
}

.container_body {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.botoes {
  display: flex;
  margin-top: 10px;
}

header {
  @apply h-28 bg-red-800;
  display: flex;
  justify-content: space-between;
}

li,
a {
  @apply font-sans text-3xl font-medium p-4;
}

li a:hover {
  @apply text-red-600;
}

input {
  @apply rounded-2xl p-2.5 text-left m-8 border-2;
  width: 70rem;
}

button {
  @apply w-96 h-auto border-2 text-base p-2.5 rounded-2xl cursor-pointer;
}

.main_logo {
  @apply h-auto w-1/2;
  margin: 10px;
  height: 40vh;
  width: auto;
  border-radius: 30px;
}

.header-menu:hover {
  background-opacity: 0 !important;
}

.button-pesquisar {
  @apply bg-red-600;
  @apply text-white;
  font-weight: bold;
  font-size: 26px;
}

.respostas_container {
  display: flex;
  flex-flow: row wrap;
  align-content: flex-start;
  align-items: center;
}

.respostas {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  @apply w-full h-auto;
}

.item-frame {
  margin-top: 5vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  width: 20vw;
  border-radius: 30px;
  /* @apply w-1/5 h-auto bg-gray-300 m-10 cursor-pointer rounded-3xl; */
}

.thumbnails {
  @apply w-auto rounded-3xl max-h-80 cursor-pointer;
}

.container-streamings {   
  display: flex;
  flex-direction: column;
}

.streamings {
  @apply w-auto max-h-10 mr-4;
}

.movie-details {
  @apply bg-gray-200 rounded-3xl;
  margin: 5vw;
  display: flex;
  flex-direction: column;
}

.movie-title {
  justify-content: center;
  text-transform: uppercase;
  font-weight: bold;
  font-size: 5vw;
}

.streamings-logos {
  display: flex;
  flex-direction: row;
}

.flex-1{
  display:flex;
  flex-direction: row;
  @apply text-3xl p-3 font-bold;  
  align-items: center;
}

.details-row-1 {
  display: flex;
  justify-content: space-between; 
  @apply ml-24 mr-24; 
}

.button-voltar {
  border: none;
  width: 5vw;
  background-color: rgb(221, 161, 161);
  @apply m-2.5;
}

.content-center{
  @apply ml-24;
}

.linha{
  @apply w-5/6 h-1 bg-black rounded-3xl;
}

.titulo_comentarios{
  text-transform: uppercase;
  @apply text-4xl font-bold; 
}

.card_comentario{
  display:flex;
  flex-direction: column;  
  @apply h-36 w-2/3 bg-gray-500 m-8 rounded-2xl text-3xl p-6;
}

</style>
