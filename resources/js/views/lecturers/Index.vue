<template>
  <b-row align-h="center">
    <b-col cols="12">

      <b-table-simple hover responsive>
        <b-thead>
          <b-tr>
            <b-th>Name</b-th>
            <b-th>Address</b-th>
            <b-th>Email</b-th>
            <b-th>Phone</b-th>
            <b-th>Actions</b-th>
          </b-tr>
        </b-thead>
        <b-tbody>
          <b-tr v-for="item in items" :key="item.id">
            <b-td>{{ item.name }}</b-td>
            <b-td>{{ item.address }}</b-td>
            <b-td>{{ item.email }}</b-td>
            <b-td>{{ item.phone }}</b-td>

            <b-td><router-link :to="`/lecturers/edit/${item.id}`">Edit</router-link></b-td>
              <b-td><button v-on:click="deleteLecturer(item.id)">Delete</button></b-td>
          </b-tr>
        </b-tbody>
      </b-table-simple>
    </b-col>
  </b-row>
</template>
<script>
export default {
  data() {
    return {
      items: []
    }
  },
  created(){
    let app = this;
    let token = localStorage.getItem('token');
    axios.get('/api/lecturers', {
      headers: { Authorization: "Bearer " + token}
    })
    .then(function (response) {
       console.log(response.data);
       app.items = response.data.data;
         app.getLecturers();
    })
    .catch(function (error) {
       console.log(error);
    })
  },
  methods: {
    getLecturers() {
      let app = this;
      let token = localStorage.getItem('token');
      axios.get('/api/lecturers', {
        headers: { Authorization: "Bearer " + token}
      })
      .then(function (response) {
         console.log(response.data);
         app.lecturers = response.data.data;
      })
      .catch(function (error) {
         console.log(error);
      })
    },
    deleteLecturer(id) {
      let app = this;
      let token = localStorage.getItem('token');
      axios.delete(`/api/lecturers/${id}`, {
        headers: { Authorization: "Bearer " + token}
      })
      .then(function (response){
        console.log(response.data);
        app.getLecturers();
      });
    }
  }
}
</script>
<style>
</style>
