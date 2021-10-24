<template>
    <div class="modal" v-bind:class="{active: modalActive}">
        <div class="modal__auth">
            <div class="modal__title">
                <h2>Вход</h2>
            </div>
            <div class="modal__toogle">
                <button v-bind:class="{activeBtn: form==='LOGIN'}" v-on:click='toLogin'>Вход</button>
                <button v-bind:class="{activeBtn: form==='SIGN'}" v-on:click='toSignup'>Регистрация</button>
            </div>
            <login v-if="form==='LOGIN'" @closeModal="closeModal"/>
            <Signup v-if="form==='SIGN'" @closeModal="closeModal"/>
        </div>
    </div>
</template>
<script>
import Login from '../components/Login.vue'
import Signup from '../components/Signup.vue'
export default {
  components: { Login, Signup },
    data(){
        return {
            form: 'LOGIN',
            modalActive: true
        }
    },
    methods: {
        isAuth() {
            this.$emit('auth')
        },
        closeModal(){
            this.modalActive = false
            this.isAuth()
            },
        toSignup(){this.form = 'SIGN'},
        toLogin(){this.form = 'LOGIN'}
    }
    
}
</script>

<style scoped>
    .modal {
        display: none;
        align-items: center;
        justify-content: center;
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.39);
        z-index: 100;
    }

    .active {
        display: flex;
    }

    .activeBtn {
        background-color: rgba(70, 0, 70, 0.452);
    }

    .modal__auth {
        width: 500px;
        background-color: white;
        z-index: 101;
        padding: 0 0 1.5rem 0;
    }

    .modal__title {
        height: 50px;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: rgba(76, 0, 130, 0.9);
        color: rgb(196, 196, 196);
    }

    .modal__toogle {
        width: 100%;
        display: flex;
        justify-content: space-around;
        padding: 1rem 1rem 1.5rem ;
    }

    .modal__toogle>button {
        padding: 0.3rem 0;
        width: 40%;
    }
</style>
