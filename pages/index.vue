<template>
    <div>
        <h1>peello - Kamban board project</h1>
        <v-btn @click="signout">clear</v-btn>

    </div>
</template>

<script>
export default {
  name: 'IndexPage',

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
