<template>
  <div id="employee-form">
    <form @submit.prevent="handleSubmit" >
      <label>Employee name</label>
      <input v-model="employee.name" /><br>
      <label>Employee Email</label>
      <input v-model="employee.email" /><br>
      <button >Add Employee</button>
    </form>
  </div>
</template>

<script>


  export default {
    name: 'employee-form',
    data() {
      return {
        employee: {
          name: '',
          email: ''
        },
      }
    },
    
    methods:{

        handleSubmit(){
            console.log('Testing...........');
            this.$emit('add:employee', this.employee)
    },
},
}

  
</script>


<style scoped>
    form{
        margin-bottom: 2rem;
    }
</style>
