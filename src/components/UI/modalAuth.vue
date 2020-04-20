<template lang="pug">
    modal(
      title="Authorisation" 
      @close="$emit('close')"
      @switchModal="$emit('switchModal')"
    )
      .div(slot="body")
        form(@submit.prevent="SubmitForm") 
  
          .form-item(:class="{errorInput: $v.email.$error}")
            label email
            p.error-text(v-if="!$v.email.required") failed is required !
            p.error-text(v-if="!$v.email.email") email is not correct !
            input(
              v-model="email"
              :class="{error: $v.email.$error}"
              @change="$v.email.$touch()"  
            )

          .form-item(:class="{errorInput: $v.password.$error}")
            label password
            p.error-text(v-if="!$v.password.required") failed is required !
            p.error-text(v-if="!$v.password.minLength") password must have at least {{ $v.password.$params.minLength.min}} !
            input(
              type="password"
              v-model="password" 
              :class="{error: $v.password.$error}"
              @change="$v.password.$touch()"
            )

          button.btn.btnPrimary() submit

          .modal-footer(@click="switchModal") to Registration
</template>

<script>
import { required, minLength, email } from 'vuelidate/lib/validators'
import modal from '@/components/modal.vue';

export default {
  components: {
    modal
  },
  data() {
    return {
      email: '',
      password: ''
    };
  },
  props: {},
  computed: {},
  methods: {
    SubmitForm() {
      this.$v.$touch();
      if(!this.$v.$invalid) {
        console.log({
          email: this.email,
          password: this.password
        })

        this.password = '';
        this.email = '';
        this.$v.$reset();
        this.$emit('close')
      }
    },
    switchModal(){
      this.password = '';
      this.email = '';
      this.$v.$reset();
      this.$emit('switchModal')
    }
    
  },
  validations: {
    password: {
      required,
      minLength: minLength(6)
    },
    email: {
      required,
      email
    }
  },

  watch: {
    email: function() {
      this.$emit('showV', this.$v)
    },
    password: function() {
      this.$emit('showV', this.$v)
    }

  },
  mounted() {},
};

</script>



<style lang="scss">
  .form-item .error-text{
    display: none;
    margin-bottom: 8px;
    color: rgb(241, 66, 66);
  }
  .form-item{
    &.errorInput .error-text{
      display: block;
    }
  } 
  input.error{
    border: 2px solid rgb(241, 66, 66);
  }

</style>