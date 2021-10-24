<template>
    <div class="profile">
      <p class="profile__title">Текущий пользователь:</p>
      <div class="profile__name">{{name}}</div>
    </div>
</template>

<script>
export default ({
    data(){
        return {
            name: (JSON.parse(localStorage.getItem('token')))?.name?.prop ||'user'
        }
    },

    methods: {
    }
})
</script>