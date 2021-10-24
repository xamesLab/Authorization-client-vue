<template>
    <div class="get-user">
      <p class="get-user__title">Найти пользователя по ID:</p>
      <div class="get-user__search">
            <input type="text" placeholder="id:" v-model="id">
            <button class="get-user__btn" v-on:click="getUser">Найти</button>
        </div>
      <div class="get-user__res">{{userFromId}}{{error}}</div>
    </div>
</template>

<script>
export default ({
    data(){
        return {
            userFromId: '',
            id: '',
            error: "--"
        }
    },
    methods: {
        getUser: async function(){
            if(this.id==='') this.id = '0'
            const tokenStr = JSON.parse(localStorage.getItem('token')).token
            const response = await fetch(`http://localhost:5000/api//user/${this.id}`, {
            method: 'GET',
            headers: {
                'Content-Type': 'application/json;charset=utf-8',
                "Authorization": `Bearer ${tokenStr}`
            },
            });
            const data = await response.json()
            if(data.message){
                this.userFromId = ''
                this.error = data.message
            } else {
                this.error = ''
                this.userFromId = data[0].name}
        }
    }
})
</script>

<style scoped>
.get-user__res {
    display: flex;
    justify-content: flex-end;
    flex: 1 1 auto;
}

.get-user__btn {
    margin-left: 10px;
    background-color: rgba(84, 0, 163, 0.432);
}

.get-user__title {
    margin-right: 20px;
}
</style>