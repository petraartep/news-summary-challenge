<template>
<v-app light>
  <!--The SideMenu Component go here-->  
  <v-toolbar fixed app light clipped-left color="warning" class="elevation-2">

    <v-toolbar-side-icon class="white--text">
      
    </v-toolbar-side-icon>

    <v-toolbar-title class="white--text">News Summary App</v-toolbar-title>
  
    <v-spacer></v-spacer>

    <v-btn icon class="white--text" value="Home">
      <v-icon>home</v-icon>
    </v-btn>

    <v-btn icon class="white--text" value="Refresh Page" onClick="window.location.href=window.location.href">
      <v-icon>refresh</v-icon>
    </v-btn>



  </v-toolbar>
  




  <v-content>
    <v-container fluid>
      <MainContent :articles="articles"></MainContent> <!-- Add the component in the template -->
    </v-container>
   </v-content>
   <v-footer class="primary" app>
      <v-layout row wrap align-center>
        <v-flex xs12>
          <div class="white--text ml-3">
            Made by
            <a class="white--text" href="https://github.com/petraartep" target="_blank">Petra</a>
          </div>
        </v-flex>
      </v-layout>
    </v-footer>
  </v-app>



</template>

<script>

import axios from 'axios' //importing the axios a HTTP library to connects the app with the API
import MainContent from './components/MainContent.vue' 

export default {
  components: {
      MainContent
  },
    data () {
      return {
       drawer: false,
       api_key:'3e84f1dafcba4c869e3b2ee5773fcbe3',
       articles: [],
       errors: [] 
      }
    },
    created () {
      axios.get('https://newsapi.org/v2/top-headlines?sources=google-news&apiKey='+this.api_key)
        .then(response => {
          this.articles = response.data.articles
          console.log('data:')
          console.log(response.data.articles) 
        })
        .catch(e => {
          this.errors.push(e)
        })
     },
      methods: {
            setResource(source){             axios.get('https://newsapi.org/v2/top-headlines?sources='+source+'&apiKey='+this.api_key)
              .then(response => {
                this.articles = response.data.articles
                console.log(response.data)             
              })
              .catch(e => {
                this.errors.push(e)
              })

            }
         }
  }
</script>
