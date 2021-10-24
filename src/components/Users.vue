<template>
    <div class="all-users">
      <div class="all-users__header">
        <p class="all-user__title">Получить всех пользователей:</p>
        <button class="all-users__btn" v-on:click="getUsers">Получить</button>
      </div>
      <UserList v-bind:usersList="usersList"/>
    </div>
</template>

<script>
import UserList from '@/components/UserList'
export default ({
    data(){
        return {
          usersList:[]
        }
    },
    components: {
      UserList
    },
    methods: {
      getUsers: async function(){
        const tokenStr = JSON.parse(localStorage.getItem('token')).token
        const response = await fetch('http://localhost:5000/api/users', {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json;charset=utf-8',
                "Authorization": `Bearer ${tokenStr}`
            }
        })
        const data = await response.json()
        this.usersList = data
      }
    }
})
</script>

<style scoped>
.all-user__title{
  margin-right: 20px;
}

.all-users__btn {
    background-color: rgba(84, 0, 163, 0.432);
}
</style>