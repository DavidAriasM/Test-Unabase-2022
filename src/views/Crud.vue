<template>
    <v-container>
        <CrearRegistro />
        <ListaJson :respuestaApi="respuestaApi"/>
    </v-container>
</template>
<script>
import ListaJson from '../components/ListaJson'
import CrearRegistro from '../components/CrearRegistro'
import Footer from '../components/Footer'
export default {
    components:{
        ListaJson, CrearRegistro, Footer
    },
    data() {
        return {
            respuestaApi: [],  
        } 
    },
    created(){
        try {
            fetch('https://jsonplaceholder.typicode.com/posts')
            .then((response) => response.json())
            .then((data) => {
                this.respuestaApi = data;
            });
        } catch (error) {
            console.log(error);
        }
    }
}
</script>