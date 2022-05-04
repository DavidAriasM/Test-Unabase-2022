<template>
    <v-form @submit.prevent="agregar(user)">
        <h2>Agregar nueva fila</h2>
        <v-container>
        <v-row class="text-center">
            <v-col cols="12" md="3">
            <v-text-field v-model="user.userId" label="Id de Usuario" required ></v-text-field>
            </v-col>
            <v-col cols="12" md="3">
            <v-text-field v-model="user.title" label="Titulo" required ></v-text-field>
            </v-col>
            <v-col cols="12" md="3">
            <v-text-field v-model="user.body" label="Cuerpo de detalle" required></v-text-field>
            </v-col>
            <v-col cols="12" md="3" xs=""><v-btn elevation="2" type="submit">Agregar</v-btn></v-col>
        </v-row>
        </v-container>
        <div>
            <v-alert v-if="alerta" type="success" dismissible @input="alerta = false">
                Post Ingresado satisfactoriamente
            </v-alert>
        </div>
    </v-form>
</template>
<script>
export default {
    data() {
        return {
            user: {
                id: '',
                userId: '',
                title: '',
                body: ''
            },
            alerta: false
        }
    },
    methods:{
        agregar: function(user) {
         try {
             fetch('https://jsonplaceholder.typicode.com/posts', {
                method: 'POST',
                body: JSON.stringify({
                    title: user.title,
                    body: user.body,
                    userId: parseInt(user.userId),
                }),
                headers: {
                    'Content-type': 'application/json; charset=UTF-8',
                },
                })
                .then((response) => response.json())
                .then((data) => {
                    console.log('Respuesta de Api: ',data)
                    this.mostrarAlerta()
                });
            } catch (error) {
                console.log(error);
            }
        },
        mostrarAlerta: function(){
            this.alerta = true
        }
    }
}
</script>