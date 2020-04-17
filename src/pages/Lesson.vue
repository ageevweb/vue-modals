<template lang="pug">
  .wrapper-content.wrapper-content--fixed
    section
      .container
        h1 Lesson

        //- first modal
        .btn.btnPrimary(@click="firstModal = true") first modal
        modal(
          title="first modal" 
          v-show="firstModal"
          @close="firstModal = false"
        )
          .div(slot="body")
            p Text
            .btn.btnPrimary(@click="firstModal = false") well done

        //- second modal
        .btn.btnPrimary(@click="secondModal.show = true") second modal
        modal(
          title="second modal" 
          v-show="secondModal.show"
          @close="secondModal.show = false"
        )
          .div(slot="body")
            form(@submit.prevent="SubmitSecondForm") 
              label name
              input(v-model="secondModal.name" type="text" required)
              label email
              input(v-model="secondModal.email" type="email" required)
              button.btn.btnPrimary() submit


                //- third modal (validate)
        button.btn.btnPrimary(@click="modalValidate = true") third modal (validate)
        modalValidate(v-show="modalValidate" @close="modalValidate = false")

</template>

<script>
import modal from '@/components/modal';
import modalValidate from '@/components/UI/modalValidate';


export default {
  components: {
    modal,
    modalValidate
  },
  data() {
    return {
      firstModal: false,
      secondModal: {
        show: false,
        name: '',
        email: '',   
      },
      modalValidate: false
    };
  },
  props: {},
  computed: {},
  methods: {
    close() {
      this.firstModal = false;
    },
    SubmitSecondForm() {
      console.log({
        name: this.secondModal.name,
        email: this.secondModal.email
      });
      this.secondModal.name = '',
      this.secondModal.email = '',
      this.secondModal.show = false
    }
  },
  watch: {},
  mounted() {},
};

</script>>



<style lang="scss">

</style>
