<template>
    <div id="employee-Table">
        <p v-if="employees.length === 0 " class="empty-table">
             NO Data </p>
        <table>
            <thead>
                <tr>
                    <th>name</th>
                    <th>email</th>
                    <th>Edit</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="employee in employees" :key="employee.id">
                  
                    <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.name">
                    </td>
                    <td v-else>{{employee.name}}</td>
                    <td v-if="editing === employee.id">
                        <input type="text" v-model="employee.email">
                    </td>
                    <td v-else>{{employee.email}}</td>
                    <td v-if="editing === employee.id">
                        <button v-on:click="editemployee(employee.id)">Save</button>
                        <button v-on:click="cencelEdit(employee)">Cancel</button>
                    </td>
                    <td v-else>
                        <button v-on:click="editMode(employee)">Edit</button>
                        <button v-on:click="$emit('del-employee', employee.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'employee-Table',
    data() {
        return {
            editing: null,
        }
    },
    methods: {
        editMode(employee){
            this.cachedEmployee = Object.assign({},employee)
            this. editing = employee.id
        },
        cencelEdit(employee){
            Object.assign(employee, this.cachedEmployee)
            this.editing = null
        },
        editemployee(employee){
            if(employee.name === '' || employee.email === '') return
            this.$emit('edit:employee', employee.id, employee)
            this.editing = null
        },
    },
    props:{
        employees: Array
    }
}
</script>

<style >
    
</style>