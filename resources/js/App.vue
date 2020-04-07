<template>
  <div>
    <MyNavbar />
    <b-container>
      <router-view />
    </b-container>
  </div>
</template>
<script>
import MyNavbar from './components/MyNavbar'

export default {
  name: 'app',
  components: {
    MyNavbar
  },

  methods: {
    deleteCourse(id) {
      let app = this;
      let token = localStorage.getItem('token');
      axios.delete(`/api/courses/${id}`, {
        headers: { Authorization: "Bearer " + token}
      })
      .then(function (response){
        console.log(response);
        app.getCourses();
      })
    },

  deleteEnrolement(id) {
    let app = this;
    let token = localStorage.getItem('token');
    axios.delete(`/api/enrolments/${id}`, {
      headers: { Authorization: "Bearer " + token}
    })
    .then(function (response){
      console.log(response.data);
      app.getEnrolements();
    });
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
},
  data() {
    return {

    }
   }
  }
</script>
<style>
</style>
