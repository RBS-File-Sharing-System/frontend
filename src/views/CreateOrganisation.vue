<template>
    <v-container>
      <v-row justify="center" align="center">
        <v-col cols="12" md="6">
          <v-card class="elevation-2">
            <!-- Centering the title -->
            <v-card-title class="text-h5 justify-center">
              Create Organization
            </v-card-title>
  
            <v-form v-model="formValid" @submit.prevent="submitForm">
              <v-card-text>
                <!-- Applying outlined variant and dense property to all text fields -->
                <v-text-field
                  v-model="form.orgName"
                  label="Organization Name"
                  variant="outlined"
                  density="compact"
                  required
                  :rules="[v => !!v || 'Organization name is required']"
                />
                <v-text-field
                  v-model="form.email"
                  label="Email"
                  variant="outlined"
                  density="compact"
                  required
                  type="email"
                  :rules="[v => !!v || 'Email is required']"
                />
                <v-text-field
                  v-model="form.username"
                  label="Username"
                  variant="outlined"
                  density="compact"
                  required
                  :rules="[v => !!v || 'Username is required']"
                />
                <v-text-field
                  v-model="form.password"
                  label="Password"
                  variant="outlined"
                  density="compact"
                  required
                  type="password"
                  :rules="[v => !!v || 'Password is required']"
                />
                <v-text-field
                  v-model="form.age"
                  label="Age"
                  variant="outlined"
                  density="compact"
                  required
                />
                <v-textarea
                  v-model="form.address"
                  label="Address"
                  variant="outlined"
                  density="compact"
                  rows="2"
                />
              </v-card-text>
  
              <!-- Centering buttons inside card -->
              <v-card-actions class="justify-center">
                <v-btn color="primary" :disabled="!formValid" type="submit">
                  Submit
                </v-btn>
                <v-btn text @click="resetForm">
                  Reset
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    name: 'CreateOrganization',
    data() {
      return {
        formValid: false,
        form: {
          orgName: '',
          email: '',
          username: '',
          password: '',
          age: '',
          address: ''
        }
      }
    },
    methods: {
      submitForm() {
        // Here, you can make an API call or perform any action on the form submission
        console.log('Form submitted:', this.form)
        alert('Organization created successfully!')
        this.resetForm()
      },
      resetForm() {
        this.form = {
          orgName: '',
          email: '',
          username: '',
          password: '',
          age: '',
          address: ''
        }
        this.formValid = false
      }
    }
  }
  </script>
  
  <style scoped>
  .v-card {
    margin-top: 50px;
  }
  </style>
  