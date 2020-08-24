<template>
  <v-app>
    <v-app-bar app color="indigo" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2 mt-5"
          contain
          src="./assets/gopher.png"
          transition="scale-transition"
          width="80"
        />
      </div>
      <v-spacer>
        <v-toolbar-title>Todo</v-toolbar-title>
      </v-spacer>
      <v-btn icon @click.stop="dialog = true">
        <v-icon>mdi-plus</v-icon>
      </v-btn>
    </v-app-bar>
    <v-dialog v-model="dialog" max-width="500">
      <v-card>
        <v-card-title class="headline"
          >Agregue la descripcion de su tarea</v-card-title
        >

        <v-textarea
          v-model="tareaText"
          solo
          name="input-7-4"
          label="Solo textarea"
        ></v-textarea>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn color="green" text @click="dialog = false">
            Cancelar
          </v-btn>

          <v-btn
            color="green darken-1"
            text
            @click="guardarTarea(), (dialog = false)"
          >
            Guardar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <v-main>
      <Todo-list />
    </v-main>
  </v-app>
</template>

<script>
import Todo from "./components/todoList";

export default {
  name: "App",

  components: {
    "Todo-list": Todo,
  },

  data: () => ({
    api: "task",
    tareas: null,
    dialog: false,
    tareaText: "",
    headers: { header1: "application/x-www-form-urlencoded" },
  }),
  mounted() {},
  methods: {
    async guardarTarea() {
      const data = {
          task: `${this.tareaText}`,
        }
      try {
        await this.axios.post(this.api,data, {headers:{
        'Content-Type': 'application/x-www-form-urlencoded'}})
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
