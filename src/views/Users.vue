<template>
    <div>
        <h1>Desde componente user</h1>
        <!-- <button class="btn btn-primary" @click="mostrarLoading({titulo: 'Accediendo información del usuario', color: 'success'})">Activar</button>
        <button class="btn btn-danger" @click="ocultarLoading"></button> -->
        <v-btn color="success" @click="mostrarLoading({titulo: 'Accediendo información del usuario', color: 'success'})">Activar</v-btn>
        <v-btn color="error" @click="ocultarLoading">Desactivar</v-btn>
        <FormUsers></FormUsers>
        <TableUsers></TableUsers>
    </div>
</template>
<script>
import FormUsers from '@/components/FormUsers.vue'
import TableUsers from '@/components/TableUsers.vue'
import { mapMutations } from 'vuex'
export default {
    name: 'Users',
    components:{
        FormUsers,
        TableUsers
    },
    methods:{
        ...mapMutations(['mostrarLoading', 'ocultarLoading']),
    }
}
</script>