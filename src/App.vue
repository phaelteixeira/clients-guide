<template>
  <div id="app">
    <h3>Cadastro: </h3> <br>
    <input type="text" v-model="nomeField" placeholder="nome" @mouseenter="error = false"> <br>
    <small v-if="error" id="nomeError">Nome inválido.</small> <br v-if="error">
    <input type="email" v-model="emailField" placeholder="email"> <br>
    <input type="number" v-model="idadeField" placeholder="idade"> <br>
    <button type="button" @click="cadastrarUsuario()">Cadastrar</button>    
    <hr>
    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h3>{{ index + 1 }}</h3>
      <Cliente :cliente="cliente" @meDelete='deletarUsuario'/>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Cliente from './components/Cliente.vue';

export default {
  name: 'App',
  components : {
    Cliente
  },
  data(){
    return{
      error: false,
      nomeField: '',
      emailField: '',
      idadeField: '',
      clientes : [
        {
          id: 1,
          nome: 'Raphael Teixeira',
          email: 'teixeira@raphael.com',
          idade: 23
        },
        {
          id: 2,
          nome: 'Michael Jordan',
          email: 'michael@jordan.com',
          idade: 46
        },
        {
          id: 3,
          nome: 'Nino Shuchter',
          email: 'nino@scott.com',
          idade: 36
        },
        {
          id: 4,
          nome: 'Henrique Avancini',
          email: 'avancini@caloi.com',
          idade: 38
        },
        {
          id: 5,
          nome: 'Alan Hatley',
          email: 'alan@cannodale.com',
          idade: 36
        }
      ]
    }
  },
  methods: {
    cadastrarUsuario: function() {
      if (this.nome == '' || this.nome == ' ' || this.nome == undefined) {
        this.error = true;
      } else {
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()});
        this.nomeField = '';
        this.emailField = '';
        this.idadeField = 0;
        this.error = false;
      }
    },
    deletarUsuario: function ($event) {
      let id = $event.clienteData;
      let arr = this.clientes.filter( cliente => cliente.id != id);
      this.clientes = arr;
    }
  },
  computed: {
    orderClientes: function () { 
      return _.orderBy(this.clientes,['nome'],['ASC']);
    }
  }
}
</script>

<style>
 #nomeError {
  color: red;
 }
</style>
