<template>
  <div class="text-center">
    <v-dialog v-model="dialog" max-width="500px">
      <template v-slot:activator="{ on }">
        <v-btn v-btn outlined class="my-3" color="primary" v-on="on">Create Task
          <v-icon right dark>queue</v-icon>
        </v-btn>
      </template>
      <v-card color="grey lighten-3">
        <v-container>
          <v-layout row wrap pa-3 justify-space-around>
            <h5 class="title">Creating Task For {{ this.courseCode }}</h5>
          </v-layout>
          <v-layout row wrap px-3 justify-space-around>
            <v-text-field label="Task Name"></v-text-field>
          </v-layout>
          <!-- <v-layout row wrap px-3 justify-space-around>
            <v-text-field label="Due Date"></v-text-field>
          </v-layout> -->
          <v-layout row wrap px-3 justify-space-around>
            <v-col cols="12" sm="6" md="4">
              <v-menu
                ref="menu"
                v-model="menu"
                :close-on-content-click="false"
                :return-value.sync="date"
                transition="scale-transition"
                offset-y
                min-width="290px"
              >
                <template v-slot:activator="{ on }">
                  <v-text-field
                    v-model="date"
                    label="Due Date"
                    prepend-icon="event"
                    readonly
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker v-model="date" no-title scrollable>
                  <v-spacer></v-spacer>
                  <v-btn text color="primary" @click="menu = false">Cancel</v-btn>
                  <v-btn text color="primary" @click="$refs.menu.save(date)">OK</v-btn>
                </v-date-picker>
              </v-menu>
            </v-col>
          </v-layout>
        </v-container>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn large text color="primary" @click="dialog = false">Submit</v-btn>
          <v-btn large text color="error" @click="dialog = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    courseCode: String
  },
  data() {
    return {
      dialog: false,
      date: new Date().toISOString().substr(0, 10),
      menu: false,
      score: 0
    };
  },

    computed: {
      //use the fixed date for formal
    fixedDate: function(){
      var newDate ="";
      newDate += this.date.substr(8,10) + '/';
      newDate += this.date.substr(5,2) + '/';
      newDate += this.date.substr(0,4);
      return newDate;
    },

  },
};
</script>