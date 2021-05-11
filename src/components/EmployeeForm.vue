<template>
    <div id='employee-form'>
        <form @submit.prevent="handleSubmit">
            <label for="">employee name</label>
            <input
                ref="first"
                type="text" 
                v-model="getNewEmployee.name"
                :class="{'has-error':submitting && invalidName}"
                @focus="clearStatus"
                @keypress="clearStatus"
            >
            <label for="">employee email</label>
            <input v-model="getNewEmployee.email" type="text"
                :class="{'has-error':submitting && invalidEmail}"
                 @focus="clearStatus"

            >
            <button>Add Employee</button>
            <br/>
            <p v-if="error && submitting" class="error-message">
                Please fill out all required fiels
            </p>
            <p v-if="success" class="success-message">
                Employee successfully added
            </p>
        </form>
    </div>
</template>

<script>
export default {
    name:'employee-form',
    data() {
        return {
            submitting: false,
            error: false,
            success: false,
            getNewEmployee:{
                name:'',
                email:''
            }
        }
    },
    methods: {
        handleSubmit(){
            this.submitting = true
            this.clearStatus()

            if (this.invalidName || this.invalidEmail){
                this.error = true
                return
            }

              this.$emit('add:employeeTest', this.getNewEmployee)
              this.$refs.first.focus();

              this.getNewEmployee = {
                  name: '',
                  email: ''
              }
              this.error =false
              this.success =true
              this.submitting = false
        },
        clearStatus(){
            this.success = false
            this.error = false
        }

    },
    computed:{
        invalidName(){
            return this.getNewEmployee.name === ''
        },
        invalidEmail(){
            return this.getNewEmployee.email === ''
        }
    }

}
</script>
<style scoped>

    form{
        margin-bottom: 2rem;
    }

    [class*='-message']{
        font-weight: bold;
    }
    .error-message{
        color: tomato;
    }
    .success-message{
        color: yellowgreen;
    }
</style>