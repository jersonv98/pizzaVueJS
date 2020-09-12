<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">API GRAPHQL PIZZA</span>
        </h1>
        <button class="button is-success is rounded" v-on:click="fetch">
          Consultar
        </button>
      </div>
    </div>

    <div class="container">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">ID</th>
            <th scope="col">Nombre</th>
            <th scope="col">Origen</th>
            <th scope="col">Ingredientes</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="pizza of pizzas" v-bind:key="pizza.id">
            <th scope="row">{{ pizza.id }}</th>
            <td>{{ pizza.name }}</td>
            <td>{{ pizza.origin }}</td>
            <td>{{ pizza.ingredient.name }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <!-- <h1 class="title">Consultar datos</h1>
    <div v-for="pizza of pizzas" v-bind:key="pizza.id"></div> -->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data: function() {
    return {
      pizzas: [],
    };
  },
  methods: {
    fetch() {
      var axios = require("axios");
      const axiosInstance = axios.create({
        headers: {
          "Access-Control-Allow-Origin": "*",
        },
      });
      let result = axiosInstance({
        method: "POST",
        url: "http://127.0.0.1:8000/graphql",
        data: {
          query: `
            query ListPizzas{
              pizzas{
                id
                name
                origin
                ingredient{
                  name
                  calories
                }
              }
            }
          `,
        },
      })
        .then((responsive) => {
          this.pizzas = responsive.data.data.pizzas;
          console.log(responsive.data);
        })
        .catch((error) => {
          console.log(error);
        });
      // async mounted(){
      //   try {
      //     let result = await axiosInstance({
      //       method: "POST",
      //       url: "http://127.0.0.1:8000/graphql",
      //       data: {
      //         query: `
      //           {
      //             {
      //               pizzas{
      //                 id
      //                 name
      //                 origin
      //               }
      //             }
      //           }
      //         `
      //       }
      //     });
      //     this.pizzas = result.data.data.pizzas;
      //   } catch(error) {
      //     console.log(error)
      //   }
      // }
    },
  },
};
</script>
