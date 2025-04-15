<template>
  <v-app>
    <v-main>
      <UserManagement />
    </v-main>
  </v-app>
</template>

<script>
// Import the CreateOrganization component
// import CreateOrganisation from './views/CreateOrganisation.vue'
import UserManagement from './views/UserManagement.vue'
// import RoleManagement from './views/RoleManagement.vue';
export default {
  name: 'App',
  components: {
    UserManagement,
    // RoleManagement
  },
  mounted(){
    sessionStorage.setItem('token','eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJmcmVzaCI6ZmFsc2UsImlhdCI6MTc0NDcxNTcyNSwianRpIjoiNmNjYWZhY2YtNDdkNi00YjljLThiZmUtM2Q3ZDI3ZmRmYzQ1IiwidHlwZSI6ImFjY2VzcyIsInN1YiI6InN1bWl0IiwibmJmIjoxNzQ0NzE1NzI1LCJleHAiOjE3NDQ3MjI5MjUsInN0YXR1cyI6dHJ1ZSwibWVzc2FnZSI6IkxvZ2luIHN1Y2Nlc3NmdWwiLCJ1c2VyX2lkIjoxLCJ1c2VyX25hbWUiOiJzdW1pdCIsImVtYWlsIjoic3VtaXRwYW5jaGJoYWkxOTk4QGdtYWlsLmNvbSIsIm9yZ19pZCI6MX0.74jhh4kuVhVyxMIjbXjtuXQrt0DzbcA1RwcTKlBtkng')
  }
}
</script>

<style>
/* Global styles can go here */
</style>
