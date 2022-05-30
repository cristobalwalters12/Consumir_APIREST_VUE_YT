<template>
    <div>
        <Header/>

            <div class="container izquierda">

                <button class="btn btn-primary" v-on:click="nuevo()" >Nuevo Condominio</button>
                <br><br>


                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID </th>
                        <th scope="col"> Nombre de Residente</th>
                        <th scope="col"> Telefono</th>
                        <th scope="col"> Condominio</th>
                      
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="residente in residentes" :key="residente.id" v-on:click="editar(residente.id)">
                        <th scope="row">{{ residente.id}}</th>
                        <td>{{ residente.nombreResidentes }}</td>
                        <td>{{ residente.telefono }}</td>
                        <td>{{ residente.condominio_id }}</td>
                     
                    </tr>
            
                </tbody>
                </table>

            </div>

        <Footer />
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Dashboard",
    data(){
        return {
            residentes:null,
          
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' + id);
            },
            nuevo(){
                this.$router.push('/nuevo');
            }
    },
    mounted:function(){
        let direccion = "http://127.0.0.1:8000/api/residentes/" ;
        axios.get(direccion).then( data =>{
            this.residentes = data.data;
        });
    }
}
</script>
<style  scoped>
    .izquierda{
        text-align: left;
    }
</style>