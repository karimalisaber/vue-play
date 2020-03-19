<template>
<div class="signup-wrapper">
    <h2>Simple Form Validation</h2>
    <form @submit.prevent="handleSubmit">
        <div class="form-group">
            <label for="firstName">First Name</label>
            <input type="text" v-model.trim="$v.user.firstName.$model" id="firstName" name="firstName" class="form-control" 
            :class="{ 'is-invalid': $v.user.firstName.$error, 'is-valid': !$v.user.firstName.$error && $v.user.firstName.$dirty }" />
            <div class="invalid-feedback">
                <span v-if= "!$v.user.firstName.required"> First Name is required </span>
                <span v-if= "!$v.user.firstName.minLength"> First Name must have at least {{$v.user.firstName.$params.minLength.min}} letters </span>
                <span v-if= "!$v.user.firstName.maxLength"> First Name must have at most {{$v.user.firstName.$params.maxLength.max}} letters </span>
            </div>
        </div>

        <div class="form-group">
            <label for="lastName">Last Name</label>
            <input type="text" v-model.trim="$v.user.lastName.$model" id="lastName" name="lastName" class="form-control" 
            :class="{ 'is-invalid': $v.user.lastName.$error, 'is-valid': !$v.user.lastName.$error && $v.user.lastName.$dirty }" />
            <div class="invalid-feedback">
                <span v-if= "!$v.user.lastName.required"> Last Name is required </span>
                <span v-if= "!$v.user.lastName.minLength"> Last Name must have at least {{$v.user.lastName.$params.minLength.min}} letters </span>
                <span v-if= "!$v.user.lastName.maxLength"> Last Name must have at most {{$v.user.lastName.$params.maxLength.max}} letters </span>
            </div>
        </div>

        <div class="form-group">
            <label for="email">email</label>
            <input type="email" v-model.trim="$v.user.email.$model" id="email" name="email" class="form-control" 
            :class="{ 'is-invalid': $v.user.email.$error, 'is-valid': !$v.user.email.$error && $v.user.email.$dirty }" />
            <div class="invalid-feedback">
                <span v-if= "!$v.user.email.required"> Email is required </span>
                <span v-if= "!$v.user.email.email"> You must enter a valid email </span>
            </div>
        </div>

        
        <div class="form-group">
            <label for="password">password</label>
            <input type="password" v-model.trim="$v.user.password.$model" id="password" name="password" class="form-control" 
            :class="{ 'is-invalid': $v.user.password.$error, 'is-valid': !$v.user.password.$error && $v.user.password.$dirty }" />
            <div class="invalid-feedback">
                <span v-if= "!$v.user.password.required"> password is required </span>
                <span v-if= "!$v.user.password.minLength"> password must have at least {{$v.user.password.$params.minLength.min}} letters </span>
            </div>
        </div>

        <div class="form-group">
            <label for="confirmPassword">confirmPassword</label>
            <input type="password" v-model.trim="$v.user.confirmPassword.$model" id="confirmPassword" name="confirmPassword" class="form-control" 
            :class="{ 'is-invalid': $v.user.confirmPassword.$error, 'is-valid': !$v.user.confirmPassword.$error && $v.user.confirmPassword.$dirty }" />
            <div class="invalid-feedback">
                <span v-if= "!$v.user.confirmPassword.required"> confirmPassword is required </span>
                <span v-if= "!$v.user.confirmPassword.sameAs && $v.user.confirmPassword.required"> passwords must be Identicall </span>
            </div>
        </div>
        <button type="submit" class="btn btn-top btn-new">Sign Up</button>

    </form>
</div>
</template>

<script>
import { required, email, minLength, maxLength, sameAs } from "vuelidate/lib/validators";
import Router from '../router';

export default {
    name: "app",
    data() {
        return {
            user: {
                firstName: "",
                lastName: "",
                email: "",
                password: "",
                confirmPassword: ""
            },
            submitted: false
        };
    },
    validations: {
        user: {
            firstName: {
                required,
                minLength: minLength(3),
                maxLength: maxLength(10)
            },
            lastName: {
                required,
                minLength: minLength(3),
                maxLength: maxLength(10)
            },
            email: {
                required,
                email
            },
            password: {
                required,
                minLength: minLength(6)
            },
            confirmPassword: {
                required,
                sameAsPassword: sameAs('password')
            }
        }
    },
    methods: {
        handleSubmit(e) {
            this.submitted = true;

            // stop here if form is invalid
            this.$v.$touch();
            if (this.$v.$invalid) {
                return;
            }
            
            Router.push({ path: 'data-grid', query: { name: `${this.user.firstName} ${this.user.lastName}`, email: this.user.email  } })
        }
    }
};
</script>

<style scoped> 
    .signup-wrapper{
    border: 1px solid #f2f2f2;
    width: 50%;
    margin: auto;
    min-width: 400px;
    padding: 50px;
    background-color: white;
    box-shadow: 0 1px 6px rgba(57,73,76,.35);
}

h2{
    margin-bottom: 25px;
    text-align: center
}

h4{
    font-size: 20px;
    line-height: 30px;
    padding: 0 0 14px 0;
    font-weight: 500;
}

label{
    font-size: 14px;
    color: #191919;
    font-family: "Hind", sans-serif;
    font-weight: 500;
    padding-bottom: 4px;
    letter-spacing: 0.02em;
}

.btn-new{ 
    background: transparent;
    color: #2879fe;
    border: 2px solid #2879fe;
    height: 40px;
    margin-top: 25px;
    padding-left: 29px;
    padding-right: 29px;
    transition: all .5s;
}

.btn-new:hover{
    background-color: blue;
    color: white;
}

@media(max-width: 576px){
    .btn-top.btn-new{
        font-size: 12px;
    }
}

@media(max-width: 350px){
.signup-wrapper{
        width: 100%;
        min-width: 100px;
        padding: 40px 15px;
}
    
}
</style> 