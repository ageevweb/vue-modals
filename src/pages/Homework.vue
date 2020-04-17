<template lang="pug">
  .wrapper-content.wrapper-content--fixed
    section
      .container
        h1 homework

        button.btn.btnPrimary(@click="modalAuth = true") authorisation
        modalAuth(v-show="modalAuth" @close="modalAuth = false")

        button.btn.btnPrimary(@click="modalRegistration = true") registration
        modalRegistration(v-show="modalRegistration" @close="modalRegistration = false")

</template>


<script>

import modalRegistration from '@/components/UI/modalRegistration';
import modalAuth from '@/components/UI/modalAuth';

export default {
  components: {
    modalRegistration,
    modalAuth
  },
  data() {
    return {
      modalAuth: false,
      modalRegistration: false
    };
  },
  props: {},
  computed: {},
  methods: {},
  watch: {},
  mounted() {},
};
</script>

<style lang="scss">

h1{
  font-size: 30px !important;
}
.btn{
  margin-right: 30px;
  margin-top: 30px;
}
</style>
