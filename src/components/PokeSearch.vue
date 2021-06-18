<template>
  <main class="container">
    <img
      src="https://upload.wikimedia.org/wikipedia/commons/9/98/International_Pok%C3%A9mon_logo.svg"
      id="logo"
      alt="Pokemon Logo"
    />

    <form action="" class="search">
      <input
        type="search"
        class="search-input"
        v-model="pokename"
        placeholder="Digite o nome do pokémon ou número"
      />
      <button class="search-button" v-on:click="getPokemon">Pesquisar</button>
    </form>

    <section class="pokemon" id="section-poke" ></section>
  </main>
</template>


<script>
export default {
  el: ".container",
  props: [],
  data() {
    return {
      pokename: "",
    };
  },
  methods: {
    getPokemon(e) {
      let datas;
      e.preventDefault();
      let newPokemon = this.pokename.toLowerCase();
      getApi();

      async function getApi() {
        await fetch(`https://pokeapi.co/api/v2/pokemon/${newPokemon}`)
          .then((response) => response.json())
          .then((data) => {
            datas = data;
          })
          .catch((err) => console.log(err));

        const layout = `
                <div id="imgbox">
                 <img id="pokeimg"src="https://pokeres.bastionbot.org/images/pokemon/${
                   datas.id
                 }.png" alt="">
                 <h1 class="name">Nome: ${datas.name}</h1>
                 <h2 id="id">Nr: ${datas.id}</h2>
                 <h2 id="type">Tipo: ${datas.types[0].type.name}</h2>
            </div>
            <div id="skills">
                <h1 id="peso" class="name">Peso: ${datas.weight / 10} KG</h1>
                <h1 class="name">Altura: ${datas.height / 10} M</h1>
                <div id="skil">
                    <h2 class="name">Habilidades: <h2>${datas.moves.map(
                      (skill) => skill.move.name
                    )} </h2>
                    </h2>
                </div>
           </div>`;

        const section = document.querySelector('.pokemon')
        
       section.innerHTML = layout;

        return section;
      }
    },
  },
};
</script>

<style >
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500&display=swap");
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
}

.container {
  width: 70vw;
  height: auto;
  background-color: rgba(255, 255, 255, 0.897);
  border-radius: 7px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding-bottom: 1.4rem;
  margin-top: 10px;
  padding-top: 30px;
  
}

#logo {
  margin-top: 1rem;
  width: 25%;
  height: auto;
  background-size: cover;
}

.search {
  width: 80%;
  padding: 1rem;
  margin-top: 1.2rem;

  display: flex;
  justify-content: space-evenly;
}

.search-input {
  width: 80%;
  height: 2rem;
  border: none;
  border-bottom: 2px solid #213a8a;
  background-color: transparent;
  outline: none;
  font-size: 1.2rem;
  padding: 5px 2px;
}

.search-input::placeholder {
  color: #0d2268;
}
.search-button {
  cursor: pointer;
  outline: none;
  border: 2px solid #0d2268;
  background-color: #ffffff;
  font-size: 1rem;
  padding: 10px 15px;
  text-align: center;
  color: #0d2268;
  text-decoration: solid;
  border-radius: 5px;
  font-weight: 500;
}

.search-button:hover {
  background-color: #0d2268;
  color: #ffffff;
  transition: 0.2s ease-in;
  font-weight: 500;
}

.pokemon {
  width: 100%;
  max-height: 100%;
  display: grid;
  grid-template-columns: 1fr 2fr;
}

#imgbox {
  display: flex;
  flex-direction: column;

  align-items: center;
  padding: 10px 0px;
}

#pokeimg {
  margin-top: 3rem;
  width: 40%;
  height: auto;
  background-size: cover;
  object-fit: cover;
}

.name {
  color: #353535;
  text-shadow: 1px 1px rgb(90, 90, 90);
  text-transform: capitalize;
  margin-top: 1rem;
}

#type {
  margin-top: 3rem;
  color: #353535;
  text-shadow: 1px 1px rgb(90, 90, 90);
  text-transform: capitalize;
}

#id {
  margin-top: 1rem;
  color: #353535;
  text-shadow: 1px 1px rgb(90, 90, 90);
}

#peso {
  margin-top: 3rem;
}

#skills {
  display: flex;
  flex-direction: column;
  align-items: left;
}

#skil {
  margin-top: 2rem;
  font-size: 0.7rem;
  text-align: left;
  padding: 0px 20px 15px 0px;
}
</style>