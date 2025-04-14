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

export default {
  name: 'App',
  components: {
    UserManagement
  }
}
</script>

<style>
/* Global styles can go here */
</style>
