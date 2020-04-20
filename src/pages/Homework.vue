<template lang="pug">
  .wrapper-content.wrapper-content--fixed
    section
      .container
        h1 homework

        button.btn.btnPrimary(@click="modalAuth = true") authorisation
        modalAuth(
          v-show="modalAuth" 
          @showV="showV"
          @close="close"
          @switchModal="switchModal"
        )

        button.btn.btnPrimary(@click="modalRegistration = true") registration
        modalRegistration(
          @showV2="showV2"
          v-show="modalRegistration" 
          @close="close"
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
      modalRegistration: false,
      vuelidAuth: null,
      vuelidRegistr: null,

    };
  },
  props: {},
  computed: {},
  methods: {
    switchModal(){
      this.modalAuth = !this.modalAuth
      this.modalRegistration = ! this.modalRegistration
    },
    showV(v) {
      this.vuelidAuth = v;
    },
    showV2(v){
      this.vuelidRegistr = v;
    },

    close(){
      this.modalAuth = false;
      this.modalRegistration = false;

      if(this.vuelidAuth !== null ) {
        this.vuelidAuth.email.$model = '';
        this.vuelidAuth.password.$model = '';
        this.vuelidAuth.$reset();
      }

      if(this.vuelidRegistr !== null ) {
        this.vuelidRegistr.email.$model = '';
        this.vuelidRegistr.password.$model = '';
        this.vuelidRegistr.repeatPassword.$model = '';
        this.vuelidRegistr.name.$model = '';
        this.vuelidRegistr.$reset();
      }
    },
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
  margin: 5px;
}
</style>
