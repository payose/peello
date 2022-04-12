<template>
  <v-app>
    <v-toolbar
      color="deep-purple accent-4"
      dark
    >
      <v-toolbar-title>Peello - task manager</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn outlined @click="signout">
        logout
      </v-btn>

    </v-toolbar>

    <v-main>
        <Nuxt />
    </v-main>
  </v-app>
</template>


<script>
    export default {
        name: 'DefaultLayout',
        data () {
            return {
            }
        },

        methods:{
            signout(){
                this.$fire.auth.signOut()
                .then((user) => $nuxt.$router.push('/auth/signin'))
                .catch(function (error) {
                    alert('logout error')
                })
            }
        }
    }
</script>
