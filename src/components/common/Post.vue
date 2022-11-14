<template>
  <div>
    <h1>List</h1>
    <input type="text" v-model="todoName" @keyup.enter="addTodo">
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Salary</th>
          <th scope="col">Age</th>
        </tr>
      </thead>
      <tbody>

        <tr v-for="item in list" :key="item.id">
          <th scope="row">{{ item.id }}</th>
          <td>{{ item.employee_name }}</td>
          <td>{{ item.employee_salary }}</td>
          <td>{{ item.employee_age }}</td>
        </tr>

      </tbody>
    </table>


  </div>
</template>
  
<script>
import axios from "axios";


export default {
  // eslint-disable-next-line
  name: "Post",
  data() {
    return {
      list: [],
      todoName: ''
    };
  },
  created() {
    axios.get('http://dummy.restapiexample.com/api/v1/employees')
      .then(response => {
        this.list = response.data.data
        console.log(response.data.data)
      })
      .catch(error => {
        console.log(error);
      })
  },
  methods: {
    addTodo() {
      axios.post('http://dummy.restapiexample.com/api/v1/employees', { employee_name: this.todoName })
        .then((response) => {
          this.list = [...this.list, response.data.data]
          console.log(response.data.data)
        })
        this.todoName=""
    }
  },
  
};
</script>
  
<style scoped>
h1 {
  text-decoration: underline;
}

li {
  color: white;
}
</style>