<template lang="pug">
    modal(
      title="Registration" 
      @close="$emit('close')"
      @switchModal="$emit('switchModal')"
    )
      .div(slot="body")
        form(@submit.prevent="SubmitForm") 
          .form-item(:class="{errorInput: $v.name.$error}")
            label name
            p.error-text(v-if="!$v.name.required") failed is required !
            p.error-text(v-if="!$v.name.minLength") name must have at least {{ $v.name.$params.minLength.min}} !
            input(
              v-model="name" 
              :class="{error: $v.name.$error}"
              @change="$v.name.$touch()"
            )

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
          
          .form-item(:class="{errorInput: $v.repeatPassword.$error}")
            label repeat password
            p.error-text(v-if="!$v.repeatPassword.sameAsPassword") passwords must be identical.

            input(
              type="password"
              v-model="repeatPassword"
              :class="{error: $v.email.repeatPassword}"
              @change="$v.repeatPassword.$touch()"  
            )

          button.btn.btnPrimary() submit

          .modal-footer(@click="switchModal") to Authorisation
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import modal from '@/components/modal.vue';

export default {
  components: {
    modal
  },
  data() {
    return {
      name: '',
      email: '',
      password: '',
      repeatPassword: ''
    };
  },
  props: {},
  computed: {},
  methods: {
    SubmitForm() {
      this.$v.$touch();
      if(!this.$v.$invalid) {
        console.log({
          name: this.name,
          email: this.email,
          password: this.password,
          repeatPassword: this.repeatPassword
        })

        this.name = '';
        this.email = '';
        this.$v.$reset();
        this.$emit('close')
      }
    },
    switchModal(){
      this.name = '';
      this.email = '';
      this.password = '';
      this.repeatPassword = '';


      this.$v.$reset();
      this.$emit('switchModal')
    }
  },
  validations: {
    name: {
      required,
      minLength: minLength(4)
    },
    email: {
      required,
      email
    },
    password: {
      required,
      minLength: minLength(6)
    },
    repeatPassword: {
      sameAsPassword: sameAs('password')
    }
  },
  watch: {
    email: function() {
      this.$emit('showV2', this.$v)
    },
    password: function() {
      this.$emit('showV2', this.$v)
    },
    name: function() {
      this.$emit('showV2', this.$v)
    },
    repeatPassword:function() {
      this.$emit('showV2', this.$v)
    },
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