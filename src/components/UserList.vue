<template>
    <ul>
        <UserItem v-for="i of usersList" v-bind:key="i.id" v-bind:i="i" />
    </ul>
</template>

<script>
import UserItem from '@/components/UserItem'
export default {
    props: ['usersList'],
    components: {
        UserItem
    }
}
</script>