<template>
  <v-dialog max-width="600px">
    <template v-slot:activator="{ on }">
      <v-btn text class="success" v-on="on">Add new project</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <h2 class="grey--text">Add a New Project</h2>
      </v-card-title>
      <v-card-text>
        <v-form class="px-3" ref="form">
          <v-text-field label="Title" v-model="title" prepend-icon="folder" :rules="inputRules"></v-text-field>
          <v-textarea label="Information" v-model="content" prepend-icon="edit" :rules="inputRules"></v-textarea>

          <v-menu 
            ref="menu"
            v-model="menu"
            :close-on-content-click="false"
            :return-value.sync="due"
            transition="scale-transition"
            offset-y>
          <template v-slot:activator="{ on }">
            <v-text-field 
                :rules="inputRules"
              :value="due"
              label="Due date"
              prepend-icon="event"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="due">
            <v-spacer></v-spacer>
            <v-btn text color="primary" @click="$refs.menu.save(due)">OK</v-btn>
          </v-date-picker>
        </v-menu>
            <v-spacer></v-spacer>
            <v-btn text class="success mx-0 mt-3" @click="submit">Add project</v-btn>            
          
        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>

export default {
  data() {
    return {
      title: "",
      content: "",
      due: null,
      menu: false,
      inputRules: [
          v => (v && v.length >= 3) || 'Minumum lenght is 3 characters'
      ]
    };
  },
  methods: {
    submit() {
        if (this.$refs.form.validate()) {
            this.$refs.form.reset()
            this.$refs.form.resetValidation()
        }
    }
  }
};
</script>