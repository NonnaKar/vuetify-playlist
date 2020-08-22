<template>
  <div class="text-center">
    <v-dialog
      v-model="dialog"
      max-width="600"
    >
      <template v-slot:activator="{ on, attrs }">
        <v-btn
          class="success"
          text
          v-bind="attrs"
          v-on="on"
        >
          Add a New Project
        </v-btn>
      </template>

      <v-card>
        <v-card-title class="headline grey lighten-2">
          Privacy Policy
        </v-card-title>

        <v-card-text>
            <v-form class="px-3">
                <v-text-field label="Title" v-model="title" prepend-icon="mdi-folder"></v-text-field>
                <v-textarea label="Information" v-model="content" prepend-icon="mdi-pencil"></v-textarea>
                
                <v-menu>
                    <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                        :value="formattedDate"
                        clearable
                        label="Due date"
                        prepend-icon="mdi-calendar-range"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        ></v-text-field>
                    </template>
                    <v-date-picker v-model="due"></v-date-picker>
                </v-menu>

                <v-btn text class="success mt-3" @click="submit">Add Project</v-btn>
            </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import format from 'date-fns/format'
import parseISO from 'date-fns/parseISO'

export default {
    name: 'Popup',
    data() {
        return {
            title: '',
            content: '',
            due: null
        }
    },
    methods: {
        submit(){
            console.log(this.title, this.content)
        }
    },
    computed: {
        formattedDate(){
            return this.due ? format(parseISO(this.due), 'do MMM yyyy') : ''
        },
    }
}
</script>