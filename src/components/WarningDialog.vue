<template>
    <v-dialog v-model="internalDialog">
      <v-card>
        <v-card-title>Warning</v-card-title>
        <v-card-text>Are you sure!</v-card-text>
        <v-card-actions>
                <v-btn text @click="confirm">Cancel</v-btn>
            </v-card-actions>
      </v-card>
      
    </v-dialog>
  </template>
  
  <script>
  export default {
    props: {
      modelValue: {
        type: Boolean,
        default: false
      }
    },
    emits: ['update:modelValue'],
    computed: {
      internalDialog: {
        get() {
          return this.modelValue;
        },
        set(value) {
          this.$emit('update:modelValue', value);
        }
      }
    },
    methods:{
        confirm(){
            this.internalDialog = false
        }
    }
  }
  </script>
  