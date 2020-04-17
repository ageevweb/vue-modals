<template lang="pug">
    modal(
      title="authorisation" 
      @close="$emit('close')"
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
          password: this.password,
          email: this.email
        })

        this.password = '';
        this.email = '';
        this.$v.$reset();
        this.$emit('close')
      }
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
  watch: {},
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