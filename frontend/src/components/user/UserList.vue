<template>
  <div>
    <div class="lead text-left">
      <strong v-if="users.results">Total de usuários: {{ users.results.length }}</strong>
    </div>
    <div>
      <table class="table table-condensed">
        <thead>
          <tr>
            <th>ID</th>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Email</th>
            <th>Username</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in users.results" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.first_name }}</td>
            <td>{{ item.last_name }}</td>
            <td>{{ item.email }}</td>
            <td>{{ item.email }}</td>
            <td>
              <font-awesome-icon icon="edit" class="link" @click="editItem(item)"/>
              <font-awesome-icon icon="trash" class="no" @click="deleteItem(item)"/>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <b-modal
      :visible="isVisible"
      title="Editar"
      @ok.prevent="saveItem"
      @hidden="clearModal"
      cancel-title="Cancelar"
      ok-title="Salvar"
    >
      <form class="myform text-left">
        <div class="form-group">
          <label>Email</label>
          <input class="form-control" type="email" v-model="editingItem.email">
        </div>
        <div class="form-group">
          <label>Primeiro Nome</label>
          <input class="form-control" type="text" v-model="editingItem.first_name">
        </div>
        <div class="form-group">
          <label>Sobrenome</label>
          <input class="form-control" type="text" v-model="editingItem.last_name">
        </div>
      </form>
    </b-modal>
  </div>
</template>

<script>
import { eventBus } from '../../main';

const endpoint = 'Insira seu endpoint aqui'
const token = process.env.VUE_APP_TOKEN

// https://github.com/axios/axios
import axios from 'axios'

export default {
  name: 'UserList',
  data() {
    return {
      users: [],
      isVisible: false,
      editingItem: {
        email: '',
        first_name: '',
        last_name: ''
      }
    }
  },
  created() {
    this.getUsers();

    var vm = this;
    // recebendo dados de outros componentes
    eventBus.$on('submit', function(response) {
      vm.users.results.push(response);
    })
  },
  methods: {
    getUsers: async function() {
      console.log(token)
      axios.get(endpoint + '/api/users/').then((response) => {
        this.users = response.data;
      })
    },
    clearModal() {
      this.isVisible = false;
      this.editingItem = {
        email: '',
        first_name: '',
        last_name: ''
      };
    },
    editItem(item) {
      this.isVisible = true;
      this.editingItem = { ...item };
    },
    saveItem() {
      const data = { ...this.editingItem };
      axios.put(endpoint + '/api/users/' + data.id + '/', data, {
        headers: { Authorization: 'Token ' + token }
      }).then(() => {
        this.isVisible = false;
        this.getUsers();
      })
    },
    deleteItem(item) {
      axios.delete(endpoint + '/api/users/' + item.id + '/', {
        headers: { Authorization: 'Token ' + token }
      }).then(() => {
        var idx = this.users.results.indexOf(item)
        this.users.results.splice(idx, 1)
      })
    }
  }
}
</script>

<style>
  .link {
    color: #0366d6
  }
  .no {
    color: red;
    margin-left: 10px;
  }
</style>