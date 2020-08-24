<template>
  <div>
    <v-container fluid>
      <div v-if="tareas === null" class="mt-5">
        <v-alert type="warning">
          No hay tareas.
        </v-alert>
      </div>
    </v-container>

    <v-card
      v-for="(tarea, index) in tareas"
      :key="index"
      class="mx-auto mt-2"
      max-width="660"
      max-height="300"
      :color="tarea.status ? 'green lighten-3' : '#E1F5FE'"
      shaped
    >
      <v-container fluid v-if="tareas != null">
        <v-row justify="space-between">
          <v-col cols="auto">
            <v-list-item-title class="headline mb-1">{{
              tarea.task
            }}</v-list-item-title>
          </v-col>
          <v-card-actions>
            <v-spacer></v-spacer>

            <v-btn icon>
              <v-icon color="red" @click="eliminarTarea(tarea._id)"
                >mdi-delete</v-icon
              >
            </v-btn>

            <v-btn icon>
              <v-icon color="green">mdi-checkbox-marked-circle</v-icon>
            </v-btn>
          </v-card-actions>
        </v-row>
      </v-container>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    api: "delete/task/",
    tareas : null
  }),
  mounted(){
      this.getTareas()
  },
  methods: {
       async getTareas() {
      try {
       const response = await this.axios.get("/task");
         this.tareas = response.data
      } catch (error) {
        console.log(error);
      }
    },
    async eliminarTarea(id) {
      try {
        await this.axios.delete(`${this.api}${id}`);
        this.getTareas()
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style></style>
