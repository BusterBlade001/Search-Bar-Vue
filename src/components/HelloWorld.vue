<template>
  Busqueda por número de documento
  <v-card
    class="mx-auto"
    color="grey-lighten-3"
    max-width="400"
  >
    <v-card-text>
      <v-text-field
        density="compact"
        variant="solo"
        label="Ingrese número de documento"
        single-line
        hide-details
        v-model="input"
        type="number"
        ></v-text-field>
      </v-card-text>
    </v-card>
  <v-card
  class="mx-auto"
  color="grey-lighten-3"
  max-width="400">
    <v-card-text>
        <ul v-for="code in filteredList()" :key="code">
          <p>{{ code }}</p>
        </ul>
        <ul v-if="input&&!filteredList().length">
          <p>No se encuentra resultado!</p>
        </ul>
    </v-card-text>
  </v-card>
</template>

<script setup>
import { ref } from "vue";
let input= ref("");
const codes = [ "| 2901 | 13 Feb 23 | ORDINARIO | SISS |", 
                "| 2901 | 13 Feb 23 | OFICIO | SISS |",
                "| 2901 | 13 Feb 23 | ACTA | SISS |",
                "| 0928 | 9 Feb 23 | ACTA | SISS |", 
                "| 10701 | 1 Feb 23 | ACTA | SISS |", 
                "| 29012023 | 4 Feb 23 | ORDINARIO | SISS |", 
                "| 09282022 | 6 Feb 23 | ACTA | SISS |", 
                "| 102 | 9 Feb 23 | OFICIO | SISS |"];
function filteredList() {
  return codes.filter((code) =>
    code.toLowerCase().includes(input.value.toLowerCase())
  );
}
</script>