<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    <v-container>
      <v-row class="text-center">
        <v-col cols="12">
          <p>App Crud usando JsonPlaceHolder</p>
        </v-col>
      </v-row>
    </v-container>
      
    </v-app-bar>
    
    <v-main>
      <router-view/>
    </v-main>
    <Footer />
  </v-app>
</template>

<script>
import Footer from './components/Footer'
export default {
  name: 'App',
  components:{
    Footer
  },
  data: () => ({
    //
  }),
};
</script>
