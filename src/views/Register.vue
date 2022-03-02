<template>
    <div class="auth-page">
        <div class="container page">
            <div class="row">
                <div class="col-md-6 offset-md-3 col-xs-12">
                    <h1 class="text-xs-center">Sign Up</h1>
                    <p class="text-xs-center">
                        <router-link :to="{name: 'login'}">
                            Need and account?
                        </router-link>
                    </p>
                    <app-validation-errors v-if="validationErrors" :validation-errors="validationErrors"></app-validation-errors>
                    <form @submit.prevent = "onSubmit">
                        <fieldset class="form-group">
                            <input v-model="username" placeholder="Username" type="text" class="form-control form-control-lg"/>
                        </fieldset>
                        <fieldset class="form-group">
                            <input v-model="email" placeholder="Email" type="text" class="form-control form-control-lg"/>
                        </fieldset>
                        <fieldset class="form-group">
                            <input v-model="password" placeholder="Password" type="password" class="form-control form-control-lg"/>
                        </fieldset>
                        <button class="btn btn-lg btn-primary pull-xs-right" :disabled="isSubmitting">
                            Sign Up
                        </button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import AppValidationErrors from '@/components/ValidationErrors.vue'
import { actionTypes } from '@/store/modules/auth'
export default {
    name: 'AppRegister',
    components: {
        AppValidationErrors
    },
    data() {
        return {
            email: '',
            password: '',
            username: ''
        }
    },
    computed: {
      isSubmitting() {
          return this.$store.state.auth.isSubmitting
      },
      validationErrors(){
           return this.$store.state.auth.validationErrors
      }
    },
    methods: {
     onSubmit() {
         console.log('onSubmit');
         this.$store.dispatch(actionTypes.register, {
             email: this.email,
             username: this.username,
             password: this.password,
         }).then(() => {
             this.$router.push({name: 'home'})
         })
     }
    }
}
</script>
