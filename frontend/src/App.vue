<template>
  <div id="app">
    <h1>CRUD Usuários</h1>
    <br><br>
    <div class="row justify-content-md-center">
      <div class="col-md-4">
        <AddUser />
      </div>
      <div class="col-md-7">
        <UserList />
      </div>
    </div><!-- row -->
  </div>
</template>

<script>
import AddUser from './components/user/AddUser.vue'
import UserList from './components/user/UserList.vue'

export default {
  name: 'App',
  components: {
    UserList,
    AddUser
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
