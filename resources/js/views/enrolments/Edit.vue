<template>
  <b-row align-h="center">
    <b-col cols="8">
      <h3 v-if="!loggedIn">Please login to view this page.</h3>
      <b-card
        v-else
        title="Edit Enrolement"
        tag="article">


        <b-form class="createForm" @submit="onSubmit">
          <b-form-group class="my-input"
            id="input-group-1"
            label-for="input-1"
            label="Enter Date">
            <b-form-input
              id="input-1"
              v-model="enrolment.date"
              type="date"
              required
              placeholder="Enter Date">
            </b-form-input>
          </b-form-group>

          <b-form-group class="my-input"
            id="input-group-2"
            label-for="input-2"
            label="Enter Time">
            <b-form-input
              id="input-2"
              v-model="enrolment.time"
              type="time"
              required
              placeholder="Enter Time">
            </b-form-input>
          </b-form-group>

          <b-form-group class="my-input"
            id="input-group-3"
            label-for="input-3"
            label="Enter Status">

            <b-form-input
              id="input-3"
              v-model="enrolment.status"
              type="text"
              required
              placeholder="assigned, associate, interested or career_break.">
            </b-form-input>
          </b-form-group>

          <b-form-group class="my-input"
            id="input-group-4"
            label-for="input-4"
            label="Course">

            <b-form-select
            name='courses'
            v-model='enrolment.course'
            class='form-control'>

            <option placeholder="Select A Course"   v-for="course in courses" v-bind:value='course.id'> {{ course.title }} </option>
          </b-form-select>
          </b-form-group>

          <b-form-group class="my-input"
            id="input-group-5"
            label-for="input-5"
            label="Lecturer">

            <b-form-select
            name='courses'
            v-model='enrolment.lecturer'
            class='form-control'>

            <option placeholder="Select A Lecturer"  v-for="lecturer in lecturers" v-bind:value='lecturer.id'> {{ lecturer.name }} </option>
          </b-form-select>
          </b-form-group>

          <b-button class="my-button" type="submit" variant="primary">Submit</b-button>
        </b-form>
      </b-card>
    </b-col>
  </b-row>
</template>

<script>
  export default {
    data() {
      return {
        enrolment: {},
        show: true,
        loggedIn: false,
        courses:'',
        lecturers:''
      }
    },
    created() {

      if (localStorage.getItem('token')) {
        this.loggedIn = true;
      }
      else {
        this.loggedIn = false;
      }

      let app = this;
      let token = localStorage.getItem('token');
      axios.get(`/api/enrolments/${app.$route.params.id}`, {
        headers: { Authorization: "Bearer " + token }
      })
      .then(function (response) {
        app.enrolment = response.data.data;
      })
      .catch(function (error) {
        console.log(error);
      });
      this.getCourses();
      this.getLecturers();
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()

        let app = this;
        let token = localStorage.getItem('token');
        axios.put(`/api/enrolments/${app.$route.params.id}`, {
            date: app.enrolment.date,
            time: app.enrolment.time,
            status: app.enrolment.status,
            course_id: app.enrolment.course,
            lecturer_id: app.enrolment.lecturer,
        },
        {
          headers: { Authorization: "Bearer " + token }
        })
        .then(function (response) {
          app.$router.push('/enrolments');
        })
        .catch(function (error) {
          console.log(error);
        });
      },
      getCourses() {
        let app = this;
        let token = localStorage.getItem('token');
        axios.get('/api/courses', {
          headers: { Authorization: "Bearer " + token}
        })
        .then(function (response) {
           console.log(response.data);
           app.courses = response.data.data;
        })
        .catch(function (error) {
           console.log(error);
        })
      },
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
    }
  }
</script>
