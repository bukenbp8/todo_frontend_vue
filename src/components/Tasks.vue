<template>
  <v-container fill-height>
    <v-row class="justify-space-around fill-height">
      <v-flex sm3>
        <OptionBar />
      </v-flex>
      <v-flex sm8>
        <v-card>
          <v-toolbar color="blue" dark>
            <EditListTitle :listTitle="listTitle" />
            <v-spacer></v-spacer>
            <v-btn icon>
              <v-icon>search</v-icon>
            </v-btn>
          </v-toolbar>
          <v-list two-line>
            <template v-for="(task, key) in TASKS">
              <Task v-bind:key="key" :task="task" :index="key" />
            </template>
          </v-list>
          <v-divider></v-divider>
          <v-card-actions>
            <v-layout>
              <v-flex>
                <NewTask />
              </v-flex>
            </v-layout>
          </v-card-actions>
        </v-card>
      </v-flex>
    </v-row>

    <Notification />
  </v-container>
</template>

<script>
import Task from "./Task";
import NewTask from "./NewTask";
import EditListTitle from "./EditListTitle";
import OptionBar from "./OptionBar";
import Notification from "./Nofification";
export default {
  name: "tasks",
  components: { Task, NewTask, EditListTitle, OptionBar, Notification },
  data: () => ({}),
  computed: {
    listTitle() {
      return this.$store.getters.LIST_TITLE(this.$route.params.id);
    },
    TASKS() {
      return this.$store.getters.TASKS(this.$route.params.id);
    }
  },
  async mounted() {
    await this.$store.dispatch("GET_TASKS", this.$route.params.id);
  }
};
</script>

<style>
</style>