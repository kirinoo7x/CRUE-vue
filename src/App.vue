<template>
  <div id="app" class="small-container">
    <h1>Employee</h1>
    <employee-form @add:employeeTest="newDataEmployee" />

    <employee-Table 
    v-bind:employees="employees"  
    @del-employee="delEmployee"
    @edit-employee="editEmployee"
    />
    
    <ul>
      <li><router-link to="/">home</router-link></li>
      <li><router-link to="/demo1">demo1</router-link></li>
    </ul>
    <router-view></router-view>
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  </div>
</template>

<script>
import EmployeeTable from '@/components/EmployeeTable'
import EmployeeForm from '@/components/EmployeeForm'
import axios from 'axios'

// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    EmployeeTable,
    EmployeeForm
  },
  data() {
    return {
      employees: []
    }
  },
  methods: {
    newDataEmployee(getNewEmployee){
      const lastId = this.employees.length > 0 ? this.employees[this.employees.length - 1].id :0;
      const id = lastId + 1;
      const newIddata = {...getNewEmployee, id}
      this.employees = [...this.employees, newIddata]
      console.log(this.employees);
    },
    delEmployee(id){
      console.log('id is',id);
      this.employees = this.employees.filter(employee => employee.id !== id)
    },
    editEmployee(id, updateEmployee){
      this.employee = this.employee.map(employee => employee.id === id ? updateEmployee : employee)
    }    
  },
    created(){
        axios.get('https://jsonplaceholder.typicode.com/comments?_limit=5')
             .then(response => this.employees = response.data)
             .catch(error => console.log(error))    
         
    }
}
</script>

<style>
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px; */
}

   button{
        background-color: #009435;
        border: 1px solid#a2e9bb;
        padding: .8rem;
    }
    button:hover,
    button:active,
    button:focus{
      background-color: #009435;
      border: 1px solid #009435;
      color: aliceblue;
    }

.small-container{
  width: 720px;
}
table {
  font-family: Arial, Helvetica, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even){background-color: #f2f2f2;}

table tr:hover {background-color: #ddd;}

table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: left;
  background-color: #4CAF50;
  color: white;
}
</style>
