<template>
  <div>
    <header>
      <nav>
        <div class="container_botao">
          <ul class="botoes">
            <li><a href="#">Login</a></li>
            <li><a href="#">Contato</a></li>
          </ul>
        </div>
      </nav>
    </header>
    <div class="container_body">
      <img class="main_logo" v-if="this.showLogo" src="~/assets/geferson.png" />
      <input
        type="Search"
        placeholder="Procure por seus filmes, séries, animes...."
        name="Search"
      /><br />
      <button @click="buscar" id="submit">Pesquisar</button>
    </div>
    <div class="respostas_container">
      <ul class="respostas">
        <li class="item-frame" :key="item" v-for="item in this.valores">
          <img class="thumbnails" :src="pirarucu" />
          {{ item }}
        </li>
      </ul>
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
      valores: [],
      pirarucu: "",
      showLogo: true,
    };
  },
  methods: {
    buscar() {
      this.pirarucu = "_nuxt/assets/placeholder.png";
      this.valores = [
        "As Crônicas de Nárnia: O Leão, A Feiticeira e o Guarda-Roupa",
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        10,
        11,
      ];
      this.showLogo = false;
    },
  },
};
</script>

<style scoped>
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
}

header {
  @apply h-28 bg-red-800;
}

li,
a {
  @apply font-sans text-3xl font-medium p-4;
}

li a:hover {
  @apply bg-red-600;
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
  display: flex;
  flex-direction: column;
  align-items: center;
  overflow: hidden;
  @apply w-1/5 h-auto bg-gray-300 m-10 cursor-pointer rounded-3xl;
}

.thumbnails {
  display: flex;
  @apply w-4/6 h-auto rounded-3xl;
}
</style>
