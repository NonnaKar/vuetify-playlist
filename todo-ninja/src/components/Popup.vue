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
                
                <v-menu
                v-model="due"
                :close-on-content-click="false"
                max-width="290"
                >
                    <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                        :value="computedDateFormattedDatefns"
                        clearable
                        label="Due date"
                        prepend-icon="mdi-calendar-range"
                        readonly
                        v-bind="attrs"
                        v-on="on"
                        @click:clear="date = null"
                        ></v-text-field>
                    </template>
                    <v-date-picker
                        v-model="date"
                        @change="due = false"
                        ></v-date-picker>
                </v-menu>

                <v-btn text class="success mt-3" @click="submit">Add Project</v-btn>
            </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import { compareAsc, format } from 'date-fns'

export default {
    data() {
        return {
            title: '',
            content: '',
            date: compareAsc(new Date().toISOString().substr(0, 10)),
            due: false
        }
    },
    methods: {
        submit() {
            console.log(this.title, this.content)
        }
    },
    computed: {
        computedDateFormattedDatefns () {
            return this.date ? format(this.date, 'EEEE, MMMM do yyyy') : ''
        },
    }
}
</script>