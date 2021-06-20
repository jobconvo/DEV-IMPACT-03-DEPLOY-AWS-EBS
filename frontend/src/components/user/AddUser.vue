<template>
  <div>
    <h2>Adicionar Usuários</h2>
    <form @submit.prevent="saveUser" @on:keyup.enter="submit" class="myform text-left">
      <!-- <div class="form-group">
        <label>@Usuário</label>
        <input class="form-control" type="text" v-model="user.username">
      </div> -->
      <div class="form-group">
        <label>Email</label>
        <input class="form-control" type="email" v-model="user.email">
      </div>
      <div class="form-group">
        <label>Primeiro Nome</label>
        <input class="form-control" type="text" v-model="user.first_name">
      </div>
      <div class="form-group">
        <label>Sobrenome</label>
        <input class="form-control" type="text" v-model="user.last_name">
      </div>
      <div class="form-group">
        <label>Senha</label>
        <input class="form-control" type="password" v-model="user.password">
      </div>
      <button type="submit" class="btn btn-sm btn-success">Confirmar</button>
    </form>
  </div>
</template>

<script>
import { eventBus } from '../../main';

const endpoint = 'http://127.0.0.1:8000'

// https://github.com/axios/axios
import axios from 'axios'


export default {
  name: 'AddUser',
  data() {
    return {
      user: {
        email: "",
        first_name: "",
        last_name: "",
        password: "",
      },
    }
  },
  methods: {
    saveUser() {

      var data = {
        email: this.user.email,
        first_name: this.user.first_name,
        last_name: this.user.last_name,
        password: this.user.password,
      };

      axios.post(endpoint + '/api/users/', data, {
        headers: { Authorization: 'Token 2071314e58a47390b04990ac8f81e0d2090290a3' }
      }).then((response) => {
        // enviando dados para outros components
        eventBus.$emit('submit', response.data);

      })
    },
  }
}
</script>

<style>
  .myform {
    background-color: #f9f9f9;
    border: 1px dashed #ddd;
    padding: 20px 15px;
    margin: 10px 0;
  }
</style>
