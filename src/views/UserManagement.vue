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
                    <v-switch v-model="item.is_active" @change="toggleIsActive(item)" :label="'Active'"
                        :color="'primary'" />
                </template>
            </v-data-table>
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
export default {
    name: "MyDataTable",
    data() {
        return {
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
                { title: 'Password', key: 'password' },
                { title: 'Email', key: 'email' },
                { title: 'Age', key: 'age' },
                { title: 'Address', key: 'address' },
                { title: 'Is Active', key: 'is_active' },
                { title: 'Last Login', key: 'last_login' },
                { title: 'Assigned Roles', key: 'assigned_roles' },
                { title: 'Action', key: 'actions' }

            ],
            items: [
                {
                    user_name: "john_doe",
                    password: "••••••••",
                    email: "john@example.com",
                    age: 30,
                    address: "123 Main St, Springfield",
                    is_active: true,
                    last_login: "2025-04-13 14:30:00",
                    assigned_roles: "Admin, Editor",
                    // will be handled in the slot
                    user_id: 2
                },
                {
                    user_name: "mario",
                    password: "••••••••",
                    email: "mario@example.com",
                    age: 30,
                    address: "123 Main St, Springfield",
                    is_active: true,
                    last_login: "2025-04-13 14:30:00",
                    assigned_roles: "Admin, Editor",
                    user_id: 1
                    // will be handled in the slot
                }
            ] // comma was missing here
        };
    },
    methods: {
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
        toggleIsActive(item){
            console.log(item)
            // item.is_active = !item.is_active 
        }
    }
};
</script>