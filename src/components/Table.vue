<template>
  <div>
    <v-data-table
        :headers="headers"
        :items="desserts"
        class="elevation-1"
        >
        <template v-slot:items="props">
            <td class="text-xs-right">{{ props.item.c_digo_dane_del_departamento }}</td>
            <td class="text-xs-right">{{ props.item.c_digo_dane_del_municipio }}</td>
            <td class="text-xs-right">{{ props.item.departamento }}</td>
            <td class="text-xs-right">{{ props.item.municipio }}</td>
            <td class="text-xs-right">{{ props.item.iron }}</td>
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
            text: 'Cod_departamento',
            align: 'left',
            sortable: false,
            value: 'c_digo_dane_del_departamento'
          },
          { text: 'Cod_municipio', value: 'c_digo_dane_del_municipio' },
          { text: 'Departamento', value: 'departamento' },
          { text: 'Municipio', value: 'municipio' },
          { text: 'Región', value: 'region' },
        ],
        desserts: []
      }
    },
    methods:{
      ...mapMutations(['mostrarLoading', 'ocultarLoading']),
      
      async dataTable(){
        console.log("joder");
        console.log(process.env);
        
        
        try {
          this.mostrarLoading({titulo: 'Accediendo a divipol', color: 'warning'})
          let datos = await axios.get('https://www.datos.gov.co/resource/xdk5-pm3f.json')
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