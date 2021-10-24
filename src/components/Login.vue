<template>
    <form @submit.prevent="login">
        <p>Форма входа</p>
        <input placeholder="login" type="text" v-model="name">
        <input placeholder="password" type="password" v-model="pass">
        <button type="submit">Войти</button>
        <div class="modal__error">{{error}}</div>
    </form>
</template>

<script>

export default ({
    data(){
        return {
            name: '',
            pass: '',
            error: ''
        }
    },
    methods: {
        res() {
            this.$emit('closeModal')
        },

        login: async function(){
            let user = {
            name: this.name,
            pass: this.pass
            };

            let response = await fetch('http://localhost:5000/api/login', {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json;charset=utf-8'
            },
            body: JSON.stringify(user)
            });
            const data = await response.json()
            if(data.message){this.error = data.message}
            if(data.token){
                localStorage.setItem('token', JSON.stringify(data));

                this.name = ''
                this.pass = ''

                this.res()}
        }
    }
})
</script>


<style scoped>
form {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
}

form>p,form>input {
    margin-bottom: 10px;
}

form>button {
    padding: 0.2rem 1.5rem;
    margin-top: 10px;
}

</style>