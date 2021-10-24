<template>
  <div class="app">
    <header>
      <h1>Authentification</h1>
      <button v-on:click="logOut">Выход</button>
    </header>
    <div class="not-login" v-if="!isLogin">
      <h2>Требуется авторизация</h2>
    </div>
    <AuthForm v-if="!isLogin" @auth="login"/>
    <main>
      <CurrentUser v-if="isLogin" />
      <UserFromId v-if="isLogin" />
      <Users v-if="isLogin" />
    </main>
  </div>
</template>

<script>
import AuthForm from '@/components/AuthForm'
import Users from '@/components/Users'
import UserFromId from '@/components/UserFromId'
import CurrentUser from '@/components/CurrentUser'
export default {
  name: 'App',
  data(){
        return {
            isLogin: false || !!localStorage.getItem('token')
        }
    },
  components: {
    AuthForm,
    Users,
    UserFromId,
    CurrentUser
  },
  methods: {
    login(){
      this.isLogin = true
    },
    logOut(){
      localStorage.removeItem('token')
      this.isLogin = false},
    }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  border: none;
  outline: none;
}

ul {
  list-style: none;
}

input {
  border: 1px solid #777;
  height: 1.5rem;
  padding: 0.2rem;
}

input:focus {
  transform: scale(1.03);
}

button:hover {
  transform: scale(1.1);
}

header {
  height: 70px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 1.5rem;
  background-color: indigo;
  color: rgb(216, 216, 216);
}

button {
  padding: 0.3rem 1.5rem;
  cursor: pointer;
}

main {
  padding: 2rem 2.5rem;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
.app {
  max-width: 1170px;
  min-height: 100vh;
  margin: 0 auto;
  background-color: rgba(128, 128, 128, 0.2);
}

.not-login {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  padding: 2rem 0;
}

.modal__error {
  color: rgb(214, 0, 0);
  padding: 1rem 0 0 0;
  font-size: 0.8rem;
  height: 1.5rem;
}

.profile {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 0;
}

.get-user {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem 0;
}

.get-user__search>input {
  margin-right: 5px;
}

.all-users__header {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 1rem 0;
}
</style>
