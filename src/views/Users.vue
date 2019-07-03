<template>
    <div>
        <h1>Desde componente user</h1>
        <FormUsers></FormUsers>
    </div>
</template>
<script>
import FormUsers from '@/components/FormUsers.vue'
export default {
    name: 'Users',
    components:{
        FormUsers
    }
}
</script>