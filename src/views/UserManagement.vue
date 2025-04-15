<template>
    <v-container>
        <v-card>
            <v-data-table :headers="headers" :items="items">
                <template #top>
                    <v-toolbar flat>
                        <v-toolbar-title>Users</v-toolbar-title>
                        <v-spacer></v-spacer>
                        <v-btn color="primary" @click="createUser" icon>
                            <v-icon>mdi-plus</v-icon>
                        </v-btn>
                    </v-toolbar>
                </template>
                <template #[`item.actions`]="{ item }">
                    <v-icon @click="updateUser(item)">mdi-pencil</v-icon>
                    <v-icon color="red" @click="deleteItem(item)">mdi-delete</v-icon>
                </template>
                <template #[`item.is_active`]="{ item }">
                    <v-switch v-model="item.is_active" @change="toggleIsActive(item)" :color="'primary'" />
                </template>
                <template #[`item.is_admin`]="{ item }">
                    <v-switch v-model="item.is_admin" @change="toggleIsAdmin(item)" :color="'primary'" />
                </template>


                <!-- is_admin -->
            </v-data-table>
            <WarningDialog :modelValue="WarningDialogStatus"/>
            <v-dialog v-model="dialog" max-width="500px">
                <v-card>
                    <v-card-title class="text-h5">Add New User</v-card-title>
                    <v-card-text>
                        <v-form>
                            <v-text-field label="Username" v-model="editedItem.userName" variant="outlined"
                                density="compact"></v-text-field>
                            <v-text-field label="Password" v-model="editedItem.password" variant="outlined"
                                density="compact"></v-text-field>
                            <v-text-field label="Email" v-model="editedItem.email" variant="outlined"
                                density="compact"></v-text-field>
                            <v-switch label="isActive" v-model="editedItem.isActive" variant="outlined"
                                density="compact" color="primary"></v-switch>
                        </v-form>

                    </v-card-text>
                    <v-card-actions>
                        <v-spacer />
                        <v-btn text @click="dialog = false">Cancel</v-btn>
                        <v-btn color="primary" @click="addUser">Add</v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
        </v-card>
    </v-container>
</template>

<script>
import { BackendURL } from '../../public/config.js'
import WarningDialog from '@/components/WarningDialog.vue';
import axios from 'axios'
export default {
    name: "MyDataTable",
    components:{
        WarningDialog
    },
    data() {
        return {
            WarningDialogStatus:false,
            // message :'sumit ',
            // status:true,
            // modelValue:true,
            // loading:false,

            dialog: false,
            editedItem: {
                userName: null,
                password: null,
                email: null,
                isActive: false,
                user_id: null
            },
            headers: [
                { title: 'User Name', key: 'user_name' },
                { title: 'Email', key: 'email' },
                { title: 'Active', key: 'is_active' },
                { title: 'Admin', key: 'is_admin' },
                { title: 'Last Login', key: 'last_login' },
                { title: 'Assigned Roles', key: 'assigned_roles' },
                { title: 'Action', key: 'actions' },


            ],
            items: [] // comma was missing here
        };
    },
    mounted() {
        this.getUsersData()
    },
    methods: {
        async getUsersData() {
            const config = {
                method: "GET",
                url: `${BackendURL}/api/users/getUsers`,
                headers: {
                    Authorization: `Bearer ${sessionStorage.getItem('token')}`,
                },
            };
            try {
                const response = await axios(config);
                console.log("responseresponse", response)
                if (response.data.status){
                    this.items = response.data.users
                }
            } catch (error) {
                window.alert('Internal Serval Error')
            }


        },
        // you can fetch data here later
        updateUser(item) {
            console.log(item)
            this.editedItem.userName = item.user_name
            this.editedItem.password = item.password
            this.editedItem.email = item.email
            this.editedItem.isActive = item.is_active
            this.editedItem.user_id = item.user_id
            this.dialog = true
        },
        createUser() {
            this.editedItem.userName = null
            this.editedItem.password = null
            this.editedItem.email = null
            this.editedItem.isActive = false
            this.editedItem.user_id = null
            this.dialog = true
        },

        async addUser(){
            let data = {
                email:this.editedItem.email,
                user_name:this.editedItem.userName,
                password:this.editedItem.password,
                is_active:this.editedItem.isActive
            }
            const config = {
                method: "POST",
                url: `${BackendURL}/api/users/createUser`,
                headers: {
                    Authorization: `Bearer ${sessionStorage.getItem('token')}`,
                },
                data:data
            };
            try {
                const response = await axios(config);
                console.log("responseresponse", response)
               
            } catch (error) {
                window.alert('Internal Serval Error')
            }
            finally{
                this.dialog = false
                this.getUsersData()
            }

        },

        toggleIsActive(item) {
            console.log(item)
            this.WarningDialogStatus = true
        },
        toggleIsAdmin(item) {
            console.log(item)
        },
        
    }
};
</script>