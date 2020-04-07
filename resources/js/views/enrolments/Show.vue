<template>
  <b-row align-h="center">
    <b-col cols="12">

      <b-table-simple hover responsive>
        <b-tbody>
          <b-tr v-for="item in items" :key="item.id">
            <b-td>{{ item.date }}</b-td>
            <b-td>{{ item.time }}</b-td>
            <b-td>{{ item.status }}</b-td>
            <b-td><router-link :to="`/enrolements/edit/${item.id}`">Edit</router-link></b-td>
              <b-td>  <button v-on:click="deleteEnrolement(item)">Delete</button></b-td>
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
    axios.get('/api/enrolements', {
      headers: { Authorization: "Bearer " + token}
    })
    .then(function (response) {
       console.log(response.data);
       app.items = response.data.data;
    })
    .catch(function (error) {
       console.log(error);
    })
  },
  methods: {
    deleteEnrolement(item) {
    const EnrolmentIndex = this.list.indexOf(item);

    this.list.splice(EnrolmentIndex,1);
    }
  }
}
</script>
<style>
</style>
