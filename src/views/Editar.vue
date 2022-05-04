<template>
    <v-container>
        <v-row class="text-center">
            <v-col cols="12" md="12" xs="">
            <v-form @submit.prevent="actualizar(user)">
                <v-text-field
                    v-model="user.userId" label="Id de Usuario" required>
                </v-text-field>
                <v-text-field 
                    v-model="user.title" label="Titulo" required >
                </v-text-field>
                <v-text-field 
                    v-model="user.body" label="Cuerpo de detalle" required>
                </v-text-field>
                <v-btn color="success" class="mx-5 mt-5" type="submit">Actualizar</v-btn>
                <v-btn class="mr-4 mt-5" depressed color="primary" to="/">Volver</v-btn>
            </v-form>
            </v-col>
        </v-row>
    <div class="my-5">
        <v-alert v-if="alerta" type="success" dismissible @input="alerta = false">
            Post actualizado satisfactoriamente
        </v-alert>
    </div>
    </v-container>
</template>
<script>
export default {
    data() {
        return {
            respuestaApi: [],
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
        actualizar: function(user){
            try {
            fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`, {
            method: 'PUT',
            body: JSON.stringify({
                id: this.$route.params.id,
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
                console.log('Respuesta',data)
                this.mostrarAlerta()
                } );
            
            } catch (error) {
                console.log(error);
            }
        },
        mostrarAlerta: function(){
            this.alerta = true;
        }
    },
    created(){
         try {
            fetch(`https://jsonplaceholder.typicode.com/posts/${this.$route.params.id}`)
            .then((response) => response.json())
            .then((data) => {
                this.user = data;
                console.log(data);
            });
        } catch (error) {
            console.log(error);
        }
    }
}
</script>