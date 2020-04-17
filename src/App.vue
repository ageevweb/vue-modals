<template lang="pug">
  .wrapper
    header
      .navbar
        .container
          .navbar-content
            .logo Modals
            ul.navbar-list
              li.navbar-item(v-for="link in links" :key="link.title")
                router-link( :to="link.url" :title="link.title" class="navbar-link") {{link.title}}

    router-view

    footer

</template>



<script>

export default {
  
  data() {
    return {
      links: [
        {title: 'Home', url:'/'},
        {title: 'Lesson', url:'/lesson'},
        {title: 'HomeWork', url:'/homework'}
      ]
    }
  },

  computed: {
   
  },

  methods: {
    
  }

}
</script>

<style lang="scss">
  
  .navbar-link{
    &.router-link-exact-active{
      color: #5247e7
    }
  }

  .container {
    padding: 0 15px;
  }
</style>
