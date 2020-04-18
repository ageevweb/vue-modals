<template lang="pug">
  .wrapper-content.wrapper-content--fixed
    section
      .container
        h1 homework

        button.btn.btnPrimary(@click="modalAuth = true") authorisation
        modalAuth(
          v-show="modalAuth" 
          @close="modalAuth = false" 
          @switchModal="switchModal"
        )

        button.btn.btnPrimary(@click="modalRegistration = true") registration
        modalRegistration(
          v-show="modalRegistration" 
          @close="modalRegistration = false"
          @switchModal="switchModal"
        )

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
  methods: {
    switchModal(){
      this.modalAuth = !this.modalAuth
      this.modalRegistration = ! this.modalRegistration
    }
  },
  watch: {},
  mounted() {},
};
</script>

<style lang="scss">

.modal-footer{
  margin-top: 20px;
  border-top: 1px solid #DCDFE6;
  padding-top: 10px;
  cursor: pointer;
  text-decoration: underline;
}

h1{
  font-size: 30px !important;
}
.btn{
  // margin-top: 30px;
}
</style>
