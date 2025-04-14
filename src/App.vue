<template>
  <v-app>
    <v-main>
      <CreateOrganisation />
    </v-main>
  </v-app>
</template>

<script>
// Import the CreateOrganization component
import CreateOrganisation from './views/CreateOrganisation.vue'

export default {
  name: 'App',
  components: {
    CreateOrganisation
  }
}
</script>

<style>
/* Global styles can go here */
</style>
