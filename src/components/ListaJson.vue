<template>
    <v-row class="text-center">
            <v-col cols="12">
                <div>
                    <v-alert v-if="alerta" type="error" dismissible @input="alerta = false">
                        Se ha elimnado el registro exitosamente
                    </v-alert>
                </div>
                <h2>Resultados de consulta Api json</h2>
            </v-col>
            <v-simple-table dark>
                <template v-slot:default>
                <thead>
                    <tr>
                    <th class="text-center" >ID</th>
                    <th class="text-center">Id de usuario</th>
                    <th class="text-center">Titulo</th>
                    <th class="text-center">Cuespo de mensaje</th>
                    <th class="text-center">Editar</th>
                    <th class="text-center">Eliminar</th>
                    </tr>
                </thead>
                <tbody >
                    <tr v-for="(item, index) in respuestaApi" :key="index">
                        <td>{{item.id}}</td>
                        <td>{{item.userId}}</td>
                        <td>{{item.title}}</td>
                        <td>{{item.body}}</td>
                        <td><v-btn depressed small color="primary" :to="{ name:'Editar', params:{id: item.id}}"><v-icon>mdi-pencil</v-icon></v-btn></td>
                        <td><v-btn depressed small color="error" @click="eliminar(item.id)">Eliminar</v-btn></td>
                    </tr>
                </tbody>
                </template>
            </v-simple-table>
        </v-row>
</template>

<script>
export default {
    data() {
        return {
            alerta: false
        }
    },
    props: { respuestaApi: Array},
    methods:{
        eliminar: function(id){
            try {
                fetch(`https://jsonplaceholder.typicode.com/posts/${ id }`, {
                method: 'DELETE',
                });
                console.log(`Se ha eliminado el registro de ID: ${ id } de exitosamente`);
                this.mostrarAlert()
            } catch (error) {
                console.log(error);
            }
        },
        mostrarAlert: function(){
            this.alerta = true
        }
    }
}
</script>