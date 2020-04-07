<template>
  <b-row align-h="center">
    <b-col cols="12">

      <b-table-simple hover responsive>
        <b-tbody>
          <b-tr v-for="item in items" :key="item.id">
            <b-th>Title</b-th>
                <b-td>{{ item.title }}</b-td>
          </b-tr>
        <b-tr>
            <b-th>code</b-th>
                <b-td> {{ item.code }} </b-td>
            </b-tr>
          <b-tr>
            <b-th>description</b-th>
                <b-td> {{ item.description }}</b-td>
        </b-tr>
      <b-tr>
            <b-th>points</b-th>>
              <b-td> {{ item.points }} </b-td>
            </b-tr>
        <b-tr>
            <b-th>level</b-th>
                <b-td>{{ item.level }} </b-td>
          </b-tr>

        <b-tr>
            <b-td><router-link :to="`/courses/edit/${item.id}`">Edit</router-link></b-td>
              <b-td>  <button v-on:click="deleteCourse(item)">Delete</button></b-td>
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
    axios.get('/api/courses', {
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
    deleteCourse(item) {
    const CourseIndex = this.list.indexOf(item);

    this.list.splice(CourseIndex,1);
    }
  }
}
</script>
<style>
</style>
