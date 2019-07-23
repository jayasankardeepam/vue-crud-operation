<template>
  <div id="app" class="small-container">
    <h1>Employees</h1>
 <employee-form @add:employee="addEmployee" />    
<employee-table :employees="employees" @edit:employee="editEmployee" @delete:employee="deleteEmployee" />


  </div>
</template>

<script>
import EmployeeForm from '@/components/EmployeeForm.vue'
import EmployeeTable from '@/components/EmployeeTable.vue'

  // export default {
  //   name: 'app',
  //   components: {
  //     EmployeeTable,EmployeeForm
  //   },


export default {
  name: 'app',
  components: {
    EmployeeTable,
    EmployeeForm,
  },
  data() {
    return {
      employees: [],
    }
  },

  mounted() {
    this.getEmployees()
  },



methods:{

//           addEmployee(employee) {
//           const lastId =
//           this.employees.length > 0
//           ? this.employees[this.employees.length - 1].id
//           : 0;
//           const id = lastId + 1;
//           const newEmployee = { ...employee, id };
//           console.log('kugsakgdkasjgdhjasgfffffffff',newEmployee)
//           this.employees = [...this.employees, newEmployee];
// },
//   deleteEmployee(id) {
//     this.employees = this.employees.filter(
//       employee => employee.id !== id
//     )
//   },

//   editEmployee(id,editEmployee){
//     this.employees = this.employees.map(employee => employee.id === id ? editEmployee : employee)
//   },

async getEmployees() {
  try {
    const response = await fetch('http://localhost:4000/students/');
    const data = await response.json();
    this.employees = data.data;
  } catch (error) {
    console.error(error)
  }
},

async addEmployee(employee) {
  try {
    const response = await fetch('http://localhost:4000/students/', {
      method: 'POST',
      body: JSON.stringify(employee),
      headers: { 'Content-type': 'application/json; charset=UTF-8' },
    })
    const data = await response.json()
    this.employees = [...this.employees, data]
  } catch (error) {
    console.error(error)
  }
},
async editEmployee(id,employee) {
  try {
    const response = await fetch(`http://localhost:4000/students/${id}`, {
      method: 'PUT',
      body: JSON.stringify(employee),
      headers: { 'Content-type': 'application/json; charset=UTF-8' },
    })
    const data = await response.json()
    this.employees = this.employees.map(employee => (employee.id === id ? data : employee))
  } catch (error) {
    console.error(error)
  }
},
async deleteEmployee(id) {
  console.log('delete')
  try {
    await fetch(`http://localhost:4000/students/${id}`, {
      method: "DELETE"
    });
    console.log('delkjhgfds');
    this.employees = this.employees.filter(employee => employee.id !== id);
  } catch (error) {
    console.error(error);
  }
}
 },


    // data() {
    //   return{
    //     employees:[
    //       {
    //       id:1,
    //       name:'sankar',
    //       email:'sankar@gmail.com'

    //     },

    //     {
    //       id:2,
    //       name:'soundar',
    //       email:'soundar@gmail.com'
          
    //     },

    //     {
    //       id:3,
    //       name:'sankar',
    //       email:'sankar@gmail.com'
          
    //     }
    //     ]
    //   }
    // }
  }
</script>



<style>
  button {
    background: #009435;
    border: 1px solid #009435;
  }

  .small-container {
    max-width: 680px;
  }
</style>
