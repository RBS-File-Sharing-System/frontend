<template>
    <v-data-table :headers="headers" :items="items">
        <template #top>

            <v-toolbar flat>
                <v-toolbar-title>Users</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="CreateRole" icon>
                    <v-icon>mdi-plus</v-icon>
                </v-btn>
            </v-toolbar>
        </template>

        <template #[`item.actions`]="{ item }">
                    <v-icon @click="updateUser(item)">mdi-pencil</v-icon>
                    <v-icon color="red" @click="deleteItem(item)">mdi-delete</v-icon>
        </template>
    </v-data-table>
    <v-dialog v-model="dialog" max-width="500px">
        <v-card>
            <v-card-title class="text-h5">Role Management</v-card-title>
            <v-card-text>
                <v-form>
                    <v-text-field label="Username" v-model="editedItem.role_name" variant="outlined"
                        density="compact"></v-text-field>
                    <v-text-field label="Password" v-model="editedItem.description" variant="outlined"
                        density="compact"></v-text-field>
                </v-form>

            </v-card-text>
            <v-card-actions>
                <v-spacer />
                <v-btn text @click="dialog = false">Cancel</v-btn>
                <v-btn color="primary" @click="addUser">Add</v-btn>
            </v-card-actions>
        </v-card>
    </v-dialog>
</template>

<script>
export default {
    data() {
        return {
            dialog: false,
            editedItem: {
                description: null,
                role_name: null

            },
            headers: [
                { title: 'Role Name', key: 'role_name' },
                { title: 'Description', key: 'description' },
                { title: 'Action', key: 'actions' }

            ],
            items: [
                {
                    role_name: 'Admin',
                    description: 'Has full access to all resources.',
                }
            ],

        }
    },
    methods: {
        CreateRole() {
            this.editedItem.role_name = null
            this.editedItem.description = null
            this.dialog = true
        },
        updateUser(item){
            this.editedItem.role_name = item.role_name
            this.editedItem.description = item.description
            this.dialog = true

        }
    }
}
</script>