<script setup>

const query = gql`
  query Pokemons {
      types_Pokemon {
        nom
        logo {
          url
        }
        forces {
        nom
        logo {
          url
        }
      }
      faiblesses {
        id
        nom
        logo {
          url
        }
      }
      }
  }
`;

const { data } = await useAsyncQuery(query);

const pokemons = ref([]);

console.log(data.value);
pokemons.value = data.value.types_Pokemon;

</script>

<template>
  <div>
    <table class="types-table">
      <thead>
        <tr>
          <th>Types</th>
          <th>Fort contre</th>
          <th>Faible contre</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="pokemon in pokemons" :key="pokemon.nom">
          <td><img :src="pokemon.logo.url" alt="Type Logo" class="type-logo" />
            {{ pokemon.nom }}</td>
          <td>
            <ul>
              <li v-for="force in pokemon.forces" :key="force.nom">
                <img :src="force.logo.url" alt="Force Logo" class="type-logo" />
                {{ force.nom }}
              </li>
            </ul>
          </td>
          <td>
            <ul>
              <li v-for="faiblesse in pokemon.faiblesses" :key="faiblesse.id">
                <img :src="faiblesse.logo.url" alt="Faiblesse Logo" class="type-logo" />
                {{ faiblesse.nom }}
              </li>
            </ul>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="fetching">Loading...</div>
    <div v-if="error">{{ error.message }}</div>
  </div>
</template>

<style scoped>
  .types-table {
    width: 70%;
    margin: 0 auto;
    border-collapse: collapse;
    table-layout: fixed;
    background-color: #ddd;
    transform: translateY(10%);
  }

  th, td {
    text-align: center;
    border: 1px solid black;
    max-width: 150px;
    word-wrap: break-word;
  }

  .type-logo {
    max-width: 50px; 
    max-height: 50px; 
    display: block; 
    margin: 0 auto;
  }

  ul {
    list-style: none;
    padding: 0;
    margin: 0;
    display: flex;
  }

  div {
    text-align: center;
  }
</style>

