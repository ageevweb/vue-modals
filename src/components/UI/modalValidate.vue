<template lang="pug">
    modal(
      title="third modal (validate)" 
      @close="$emit('close')"
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

          button.btn.btnPrimary() submit
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
      name: '',
      email: '',
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
          email: this.email
        })

        this.name = '';
        this.email = '';
        this.$v.$reset();
        this.$emit('close')
      }
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
