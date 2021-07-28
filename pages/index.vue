<template>
  <div>
    <header>
      <nav>
        <div class = "container_botao">
          <ul class="botoes">
            <li><a href="#">Login</a></li>
            <li><a href="#">Contato</a></li>
          </ul>
        </div>
      </nav>
    </header>
    <div class = "container_body">
      <img src="~/assets/geferson.png" />
      <form>
        <input
          type="Search"
          placeholder="Procure por seus filmes, séries, animes...."
          name="Search"
        /><br />
        <button type="submit">Pesquisar</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>

.container_botao{
  display: flex;  
  align-content: center;
  align-items: center;
  flex-direction: row-reverse; 
}

.container_body{  
  display: flex;
  flex-direction: column;
  align-items: center;
  
}

.botoes{
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
  @apply w-96 h-auto ml-96 border-2 text-base p-2.5 rounded-2xl cursor-pointer;
}

img {
  @apply h-auto w-1/2;
}
</style>
