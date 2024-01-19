<template>
  <header :class="{ top: true }">
    <h2>Vue</h2>
    <h5 :class="{numClass1: true}" >Login name: Suresh</h5></header>
    <div>
    <div :class="{ top: true }" >
      <input type="text" v-model="searchItem" placeholder="Search..." />
<ul v-if="searchItem.length > 0">
<li v-for="item in filteredItems" :key="item.id">  
{{ item.name }} - {{ item.Gender }}
-{{ item.Designation }}-{{ item.dateOfJoining }}

</li>
</ul>
    <p v-else>No employee found.</p>
  </div>

  <div :class="{ top1: true }">
  <div>
    <form @submit.prevent="addEmployee">
      <label for="name">Name:</label>
      <input v-model="newEmployee.name" type="text" id="name" />

      <label :class="{ details1: true }" for="age">Age:</label>
      <input v-model.number="newEmployee.age" type="number" id="age" />

      <label :class="{ details1: true }" for="dateOfJoining">Date Of Joining:</label>
      <input v-model="newEmployee.dateOfJoining" type="text" id="dateOfJoining" />

      <label :class="{ details1: true }" for="Gender">Gender:</label>
      <select v-model="newEmployee.Gender" id="Gender">
        <option value="Male">Male</option>
        <option value="Female">Female</option>
      </select>
      <label :class="{ details1: true }"  for="Designation">Designation:</label>
      <select v-model="newEmployee.Designation" id="Designation">
        <option value="Manager">Manager</option>
        <option value="Staff">Staff</option>
      </select>
</form></div><div >
    <button @click="addEmployee" :class="{add1: true}">Add Employee</button>
    <table >
      <thead>
        <tr >
          <th >Id</th>
          <th  >Name</th>
          <th >Age</th>
          <th >Date Of Joining</th>
          <th >Gender</th>
          <th >Designation</th>
          <th >action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(employee, index) in employees"  :key="index" >
          <td >{{ index + 1 }}</td>
          <td  >{{ employee.name }}</td>
          <td  >{{ employee.age }}</td>
          <td  >{{ employee.dateOfJoining }}</td>
          <td  >{{ employee.Gender }}</td>
          <td  >{{ employee.Designation }}</td> 
          <td  ><button @click="editEmployee(index)">edit</button>
            <button @click="deleteEmployee(index)" :class="{ delete1: true}">delete</button></td>
        </tr>
      </tbody>
    </table>
 </div> 
</div></div>
</template>
<script setup>
import { ref,computed } from 'vue';
    const employees = ref([]);
    const newEmployee = ref({
      name: '',
      age: 0,
      dateOfJoining: new Date().toLocaleDateString(),
      Gender: 'Male',
      Designation: 'Staff',
    });
    const addEmployee = () => {
      employees.value.push({ ...newEmployee.value });
      
      newEmployee.value = {
        name: '',
        age: 0,
        dateOfJoining: new Date().toLocaleDateString(),
        Gender: 'Male',
        Designation: 'Staff',
      };
    };
  const search = ref('')
  
  const deleteEmployee = (index) => {
      employees.value.splice(index,1);
    };
    const editEmployee = (index) => {
      employees.value[index] = newEmployee.value;
    };  
    const searchItem = ref("");


const filteredItems = computed(() => {

return employees.value.filter((item) => {

return item.name.toLowerCase().includes(searchItem.value.toLowerCase());

});

});

</script>
<style>
.numClass1{  
  margin-right: 100px;
  border: solid;
  }
  .top {
display: flex;
justify-content: space-between;
border : 1px solid black;

}
.details {
  padding-left: 100px;
  margin: 50px;
  padding:9px
}
.details1 {
  padding-left: 50px;
  padding:9px
}
.top1 {

border : 1px solid black;
padding:9px
}
.delete1{
  margin-left: 5px;
}
.add1 {
  margin:10px;
  display: flex;
  
}
table, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>

