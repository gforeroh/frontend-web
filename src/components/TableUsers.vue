<template>
  <div>
    <v-data-table
        :headers="headers"
        :items="desserts"
        class="elevation-1"
        >
        <template v-slot:items="props">
            <td class="text-xs-right">{{ props.item.id }}</td>
            <td class="text-xs-right">{{ props.item.name }}</td>
            <td class="text-xs-right">{{ props.item.lastname }}</td>
            <td class="text-xs-right">{{ props.item.username }}</td>
            <td class="text-xs-right">{{ props.item.email }}</td>
            <td class="text-xs-right">{{ props.item.password }}</td>
        </template>
    </v-data-table>
    <v-btn color="primary" @click="dataTable()">Reload</v-btn>
  </div>
</template>
<script>
  import { mapMutations } from 'vuex'
  import axios from 'axios';
  export default {
    data () {
      return {
        headers: [
          {
            text: 'Id',
            align: 'left',
            sortable: true,
            value: 'id'
          },
          { text: 'Nombre', value: 'name' },
          { text: 'Apellido', value: 'lastname' },
          { text: 'Usuario', value: 'username' },
          { text: 'Email', value: 'email' },
          { text: 'Pass', value: 'password' },
        ],
        desserts: []
      }
    },
    methods:{
      ...mapMutations(['mostrarLoading', 'ocultarLoading']),
      
      async dataTable(){
        try {
          this.mostrarLoading({titulo: 'Accediendo a divipol', color: 'warning'})
          let datos = await axios.get(`${process.env.VUE_APP_API_WEB}/users`)
          this.desserts = await datos.data
        } catch (error) {
          console.log(error);
        } 
        finally {
          this.ocultarLoading()
        }
      }
    },
    created(){
      this.dataTable()
    }
  }
</script>