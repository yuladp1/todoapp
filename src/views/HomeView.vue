<!-- eslint-disable prettier/prettier -->
<template>
  <div class="pa-6">
    <h1>Todo List</h1>
    <v-text-field
      v-model="newTitle"
      @click:append="appendItem"
      @keyup.enter="appendItem"
      outlined
      clearable
      hide-detailes
      label="Enter task:"
      append-icon="mdi-plus"
    ></v-text-field>
    <div v-for="task in tasks" :key="task.id">
      <v-list subheader flat>
        <v-list-item @click="doneTask(task.id)">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox :input-value="task.done" color="primary"></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title> {{ task.taskname }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-action>
              <v-btn icon @click.stop="deleteTask(task.id)">
                <v-icon color="grey lighten-1">mdi-delete</v-icon>
              </v-btn>
            </v-list-item-action>
          </template>
        </v-list-item>
      </v-list>
      <v-divider inset></v-divider>
    </div>
    // eslint-disable-next-line prettier/prettier
    <v-icon v-if="tasks.length == 0" large color="green"> mdi-check-bold </v-icon>
  </div>
</template>

<script>
export default {
  name: "Home-view",
  data() {
    return {
      tasks: [
        { id: "1", taskname: "Task one", done: false },
        { id: "2", taskname: "Task Two", done: true },
        { id: "3", taskname: "task Three", done: false },
      ],
      newTitle: "",
    };
  },
  methods: {
    doneTask(id) {
      let task = this.tasks.filter((task) => task.id === id)[0];
      task.done = !task.done;
    },
    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },
    appendItem() {
      let newTask = {
        id: Date.now(),
        taskname: this.newTitle,
        done: false,
      };
      this.tasks.push(newTask);
    },
  },
};
</script>
