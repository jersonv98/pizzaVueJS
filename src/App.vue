<template>
  <div id="app">
    <header>
      <h1 class="text-center">
        <span class="badge badge-info">CRUD PIZZA-INGREDIENTS</span>
      </h1>
    </header>

    <div class="container">
      <div class="row">
        <div class="col">
          <button
            id="btnNuevo"
            type="button"
            class="btn btn-success"
            data-toggle="modal"
            data-target="#modalPizza"
            title="Crear Pizza"
          >
            <font-awesome-icon icon="plus-circle" />
          </button>
        </div>
      </div>

      <div
        class="modal fade"
        id="modalPizza"
        tabindex="-1"
        role="dialog"
        aria-labelledby="exampleModalLabel"
        aria-hidden="true"
      >
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header text-white bg-success">
              <h5 class="modal-title" id="exampleModalLabel">Ingresar Pizza</h5>
              <button
                type="button"
                class="close"
                data-dismiss="modal"
                aria-label="Close"
              >
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <form id="formPizzas">
              <div class="modal-body">
                <div class="form-group">
                  <label for="name" class="col-form-label">Nombre:</label>
                  <input type="text" class="form-control" id="name" />
                </div>
                <div class="form-group">
                  <label for="origin" class="col-form-label">Origen:</label>
                  <input type="text" class="form-control" id="origin" />
                </div>
                <div class="form-group">
                  <label for="nameIngredient" class="col-form-label"
                    >Ingredients:</label
                  >
                  <div class="row">
                    <div class="col">
                      <input
                        type="text"
                        class="form-control"
                        id="nameIngredient"
                        placeholder="Nombre"
                      />
                    </div>
                    <div class="col">
                      <input
                        type="text"
                        class="form-control"
                        id="calories"
                        placeholder="Calorias"
                      />
                    </div>
                  </div>
                </div>
              </div>
              <div class="modal-footer">
                <button
                  type="button"
                  class="btn btn-light"
                  data-dismiss="modal"
                >
                  Cancelar
                </button>
                <button
                  type="button"
                  id="btnGuardar"
                  class="btn btn-dark"
                  @click="btnCrear()"
                >
                  Guardar
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>

      <div class="row mt-5">
        <div class="col-lg-12">
          <table class="table table-hover" id="tablaPizzas">
            <thead class="thead-dark text-center">
              <tr>
                <th scope="col">ID</th>
                <th scope="col">Nombre</th>
                <th scope="col">Origen</th>
                <th scope="col">Ingredientes</th>
                <th scope="col">Acciones</th>
              </tr>
            </thead>
            <tbody class="text-center">
              <tr v-for="pizza of pizzas" v-bind:key="pizza.id">
                <th class="align-middle" scope="row">{{ pizza.id }}</th>
                <td class="align-middle">{{ pizza.name }}</td>
                <td class="align-middle">{{ pizza.origin }}</td>
                <td class="align-middle">
                  <div>
                    <table class="table table-hover">
                      <thead class="thead-light">
                        <tr>
                          <th scope="col">Nombre</th>
                          <th scope="col">Calorias</th>
                          <th scope="col">Acciones</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr
                          v-for="ingredient of pizza.ingredients"
                          v-bind:key="ingredient.id"
                        >
                          <td class="align-middle">{{ ingredient.name }}</td>
                          <td class="align-middle">
                            {{ ingredient.calories }}
                          </td>
                          <td class="align-middle">
                            <div class="btn-group" role="group">
                              <button class="btn btn-primary" title="Editar">
                                <svg
                                  width="1em"
                                  height="1em"
                                  viewBox="0 0 16 16"
                                  class="bi bi-pencil-square"
                                  fill="currentColor"
                                  xmlns="http://www.w3.org/2000/svg"
                                >
                                  <path
                                    d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456l-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"
                                  />
                                  <path
                                    fill-rule="evenodd"
                                    d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"
                                  />
                                </svg>
                              </button>
                              <button class="btn btn-danger" title="Eliminar">
                                <svg
                                  width="1em"
                                  height="1em"
                                  viewBox="0 0 16 16"
                                  class="bi bi-trash"
                                  fill="currentColor"
                                  xmlns="http://www.w3.org/2000/svg"
                                >
                                  <path
                                    d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"
                                  />
                                  <path
                                    fill-rule="evenodd"
                                    d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"
                                  />
                                </svg>
                              </button>
                            </div>
                          </td>
                        </tr>
                      </tbody>
                    </table>
                  </div>
                </td>
                <td class="align-middle">
                  <div class="btn-group" role="group">
                    <button
                      id="btnEditar"
                      type="button"
                      class="btn btn-primary"
                      title="Editar"
                      @click="btnEditar(pizza.id, pizza.name, pizza.origin)"
                    >
                      <svg
                        width="1em"
                        height="1em"
                        viewBox="0 0 16 16"
                        class="bi bi-pencil-square"
                        fill="currentColor"
                        xmlns="http://www.w3.org/2000/svg"
                      >
                        <path
                          d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456l-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z"
                        />
                        <path
                          fill-rule="evenodd"
                          d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5v11z"
                        />
                      </svg>
                    </button>

                    <!-- <div
                      class="modal fade"
                      id="modalEditarPizza"
                      tabindex="-1"
                      role="dialog"
                      aria-labelledby="exampleModalLabel"
                      aria-hidden="true"
                    >
                      <div class="modal-dialog" role="document">
                        <div class="modal-content">
                          <div class="modal-header text-white bg-primary">
                            <h5 class="modal-title" id="exampleModalLabel">
                              Editar Pizza
                            </h5>
                            <button
                              type="button"
                              class="close"
                              data-dismiss="modal"
                              aria-label="Close"
                            >
                              <span aria-hidden="true">&times;</span>
                            </button>
                          </div>
                          <form id="formEditPizzas">
                            <div class="modal-body">
                              <div class="form-group">
                                <label for="name" class="col-form-label"
                                  >Nombre:</label
                                >
                                <input
                                  type="text"
                                  class="form-control"
                                  id="name"
                                />
                              </div>
                              <div class="form-group">
                                <label for="origin" class="col-form-label"
                                  >Origen:</label
                                >
                                <input
                                  type="text"
                                  class="form-control"
                                  id="origin"
                                />
                              </div>
                            </div>
                            <div class="modal-footer">
                              <button
                                type="button"
                                class="btn btn-light"
                                data-dismiss="modal"
                              >
                                Cancelar
                              </button>
                              <button
                                type="button"
                                id="btnGuardar"
                                class="btn btn-dark"
                                @click="
                                  btnEditar(pizza.id, pizza.name, pizza.origin)
                                "
                              >
                                Guardar
                              </button>
                            </div>
                          </form>
                        </div>
                      </div>
                    </div> -->

                    <button
                      class="btn btn-danger"
                      title="Eliminar"
                      @click="btnEliminar(pizza.id, pizza.name)"
                    >
                      <svg
                        width="1em"
                        height="1em"
                        viewBox="0 0 16 16"
                        class="bi bi-trash"
                        fill="currentColor"
                        xmlns="http://www.w3.org/2000/svg"
                      >
                        <path
                          d="M5.5 5.5A.5.5 0 0 1 6 6v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm2.5 0a.5.5 0 0 1 .5.5v6a.5.5 0 0 1-1 0V6a.5.5 0 0 1 .5-.5zm3 .5a.5.5 0 0 0-1 0v6a.5.5 0 0 0 1 0V6z"
                        />
                        <path
                          fill-rule="evenodd"
                          d="M14.5 3a1 1 0 0 1-1 1H13v9a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V4h-.5a1 1 0 0 1-1-1V2a1 1 0 0 1 1-1H6a1 1 0 0 1 1-1h2a1 1 0 0 1 1 1h3.5a1 1 0 0 1 1 1v1zM4.118 4L4 4.059V13a1 1 0 0 0 1 1h6a1 1 0 0 0 1-1V4.059L11.882 4H4.118zM2.5 3V2h11v1h-11z"
                        />
                      </svg>
                    </button>
                  </div>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
      <!-- <select id="ingredient" class="form-control"
        ><option
          v-for="ingrediente of ingredients"
          v-bind:key="ingrediente.id"
          :value="ingrediente.name"
          >{{ ingrediente.name }}</option
        ></select
      >-->
    </div>
  </div>
</template>

<script>
var metodo = "POST";
var url = "http://127.0.0.1:8000/graphql";
var axios = require("axios");
const Swal = require("sweetalert2");
const axiosInstance = axios.create({
  headers: {
    "Access-Control-Allow-Origin": "*",
  },
});

export default {
  name: "App",
  data: function() {
    return {
      ingredients: [],
      pizzas: [],
      id: 0,
      name: "",
      origin: "",
      ingredient: "",
      calories: "",
      modal: false,
    };
  },
  created() {
    this.fetch();
    this.listarIngredients();
  },
  methods: {
    toggleModal() {
      this.modal = !this.modal;
    },
    //Botones
    btnCrear() {
      this.name = document.getElementById("name").value;
      this.origin = document.getElementById("origin").value;
      this.ingredient = document.getElementById("nameIngredient").value;
      this.calories = document.getElementById("calories").value;

      if (this.name == "" || this.origin == "" || this.ingredient == 0) {
        Swal.fire({
          type: "info",
          title: "Datos incompletos",
        });
      } else {
        this.crearPizza();
        const Toast = Swal.mixin({
          toast: true,
          position: "top-end",
          showConfirmButton: false,
          timer: 3000,
        });
        Toast.fire({
          type: "success",
          title: "Pizza Agregada!",
        });
      }
    },
    btnEditar: async function(id, name, origin) {
      await Swal.fire({
        title: "Editar Pizza",
        html:
          '<div class="form-group"><div class="row"><label class="col-sm-3 col-form-label">Nombre: </label><div class="col-sm-7"><input id="name" value="' +
          name +
          '" type="text" class="form-control"></div></div><div class="row"><label class="col-sm-3 col-form-label">Origin: </label><div class="col-sm-7"><input id="origin" value="' +
          origin +
          '" type="text" class="form-control"></div></div></div>',
        focusConfirm: false,
        showCancelButton: true,
      }).then((result) => {
        if (result.value) {
          this.name = document.getElementById("name").value;
          this.origin = document.getElementById("origin").value;
          console.log(name);
          this.editarPizza(id, this.name, this.origin);
          Swal.fire(
            "¡Actualizada!",
            "La pizza ha sido actualizada.",
            "success"
          );
        }
      });
    },
    btnEliminar: function(id, name) {
      Swal.fire({
        title: "¿Está seguro de eliminar la: " + name + " ?",
        type: "warning",
        showCancelButton: true,
        confirmButtonColor: "#d33",
        cancelButtonColor: "#3085d6",
        confirmButtonText: "Eliminar",
      }).then((result) => {
        if (result.value) {
          this.eliminarPizza(id);
          //y mostramos un msj sobre la eliminación
          Swal.fire("¡Eliminado!", "La pizza ha sido eliminada.", "success");
        }
      });
    },
    //cerrar modal

    //listar pizzas
    fetch() {
      let result = axiosInstance({
        method: metodo,
        url: url,
        data: {
          query: `
            query listPizzas{
              pizzas{
                id
                name
                origin
                ingredients{
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
    },
    //listar ingredientes
    listarIngredients() {
      let result = axiosInstance({
        method: metodo,
        url: url,
        data: {
          query: `
            query listIngredient{
              ingredients{
              id
                name
                calories
              }
            }
          `,
        },
      })
        .then((responsive) => {
          this.ingredients = responsive.data.data.ingredients;
          console.log(responsive.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    //Procedimiento CREAR.
    crearPizza: function() {
      let result = axiosInstance({
        method: metodo,
        url: url,
        data: {
          query: `
            mutation createPizza{
              createPizza(input:{
                name:"${this.name}"
                origin:"${this.origin}"
                ingredients:{
                  create:[
                    {name:"${this.ingredient}",calories:"${this.calories}"}
                  ]
                }
              }){
                id
                name
                origin
                ingredients{
                  name
                  calories
                }
              }
            }
          `,
        },
      }).then((response) => {
        this.fetch();
      });
      this.name = "";
      this.ingredient = "";
      this.origin = "";
      this.calories = "";
    },
    //Procedimiento EDITAR.
    editarPizza: function(id, name, origin) {
      let result = axiosInstance({
        method: metodo,
        url: url,
        data: {
          query: `
            mutation updatePizza{
              updatePizza(input:{
                id:${id}
                name:"${name}"
                origin:"${origin}"
              }){
                id
                name
                origin
                ingredients{
                  id
                  name
                  calories
                }
              }
            }
          `,
        },
      }).then((response) => {
        this.fetch();
      });
    },
    //Procedimiento BORRAR.
    eliminarPizza: function(id) {
      let result = axiosInstance({
        method: metodo,
        url: url,
        data: {
          query: `
           mutation deletePizza{
            deletePizza(id:${id}){
              id
              name
              origin
              ingredients{
                id
                name
                calories
              }
            }
          }
          `,
        },
      }).then((response) => {
        this.fetch();
      });
    },
  },
};
</script>
