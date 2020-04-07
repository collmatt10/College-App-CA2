<template>
  <div>
  <b-navbar toggleable="sm" type="dark" variant="dark">
    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
    <b-collapse id="nav-collapse" is-nav>
    <b-navbar-nav>
      <!-- <router-link to="/">Home</router-link> -->
      <b-nav-item to="/">Home</b-nav-item>
      <b-nav-item-dropdown text="Courses" left>
        <b-dropdown-item to="/courses">View All</b-dropdown-item>
        <b-dropdown-item to="/courses/create">Create</b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown text="Enrolements" >
        <b-dropdown-item to="/enrolments">View All</b-dropdown-item>
        <b-dropdown-item to="/enrolments/create">Create</b-dropdown-item>
      </b-nav-item-dropdown>

      <b-nav-item-dropdown text="Lecturers" >
        <b-dropdown-item to="/lecturers">View All</b-dropdown-item>
        <b-dropdown-item to="/lecturers/create">Create</b-dropdown-item>
      </b-nav-item-dropdown>
    </b-navbar-nav>

    <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">
          <b-nav-item to="/register">Register</b-nav-item>
        <b-nav-item-dropdown right>
          <!-- Using 'button-content' slot -->
          <template v-slot:button-content>
            <em>User</em>
          </template>
          <!-- View user by id -->
          <router-link :to="`/users/1`">Profile</router-link>
          <b-dropdown-item @click="logout">Log Out</b-dropdown-item>
        </b-nav-item-dropdown>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
</div>
</template>
<script>
export default {
  name: "myNavbar",
  methods: {
logout() {
  let token = localStorage.getItem('token');
  axios.get('/api/logout', {
    headers: { Authorization: "Bearer " + token}
  })
  .then(function (response) {
     console.log(response);
  })
  .catch(function (error) {
     console.log(error);
  })
  localStorage.removeItem('token');
  this.$router.push({
    name: 'home'
  });
}
 }
};
</script>
<style>
.navbar {
  margin-bottom: 40px;
}
</style>
