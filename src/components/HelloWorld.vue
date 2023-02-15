<template>
  Busqueda por número de documento

  <v-container class="mb-5">
    <v-row>
      <v-col>
        <v-text-field
          density="compact"
          variant="solo"
          label="Ingrese número de documento"
          single-line
          hide-details
          v-model="input1"
          type="number"
        ></v-text-field>
      </v-col>
      <v-col>
        <v-select
          density="compact"
          label="Select"
          :items="types"
          v-model="input2"
          clearable="true"
        ></v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col class="mx-auto">
        <div class="w-50 mx-auto">
          <ul v-for="code in filteredListUnificado()" :key="code">
            <p class="text-center">{{ code }}</p>
          </ul>
          <ul v-if="input1 && input2 && !filteredListUnificado().length">
            <p>No se encuentra resultado!</p>
          </ul>
        </div>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card class="mx-auto mb-5" color="grey-lighten-3" max-width="400">
          <v-card-text>
            <v-text-field
              density="compact"
              variant="solo"
              label="Ingrese número de documento"
              single-line
              hide-details
              v-model="input1"
              type="number"
            ></v-text-field>
          </v-card-text>
        </v-card>

        <v-card class="mx-auto mb-5" color="grey-lighten-3" max-width="400">
          <v-card-text>
            <ul v-for="code in filteredList()" :key="code">
              <p>{{ code }}</p>
            </ul>
            <ul v-if="input1 && !filteredList().length">
              <p>No se encuentra resultado!</p>
            </ul>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col>
        <v-card class="mx-auto mb-5" color="grey-lighten-3" max-width="400">
          <v-card-text>
            <v-select label="Select" :items="types" v-model="input2"></v-select>
          </v-card-text>
        </v-card>

        <v-card class="mx-auto mb-5" color="grey-lighten-3" max-width="400">
          <v-card-text>
            <ul v-for="code in filteredListTypes()" :key="code">
              <p>{{ code }}</p>
            </ul>
            <ul v-if="input2 && !filteredListTypes().length">
              <p>No se encuentra resultado!</p>
            </ul>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from "vue";
const input1 = ref("");
const input2 = ref("");
const types = ref(["ORDINARIO", "ACTA", "CARTA", "OFICIO"]);
const codes = ref([
  "| 2901 | 13 Feb 23 | ORDINARIO | SISS |",
  "| 2901 | 13 Feb 23 | OFICIO | SISS |",
  "| 2901 | 13 Feb 23 | ACTA | SISS |",
  "| 0928 | 9 Feb 23 | ACTA | SISS |",
  "| 10701 | 1 Feb 23 | ACTA | SISS |",
  "| 29012023 | 4 Feb 23 | ORDINARIO | SISS |",
  "| 09282022 | 6 Feb 23 | ACTA | SISS |",
  "| 102 | 9 Feb 23 | OFICIO | SISS |",
]);
function filteredList() {
  return codes.value.filter((code) =>
    code.toLowerCase().includes(input1.value.toLowerCase())
  );
}
function filteredListTypes() {
  return codes.value.filter((code) =>
    code.toLowerCase().includes(input2.value.toLowerCase())
  );
}
function filteredListUnificado() {
  if (input1.value != null && input2.value == "") {
    return codes.value.filter((code) =>
      code.toLowerCase().includes(input1.value.toLowerCase())
    );
  }

  if (input1.value == null && input2.value != "") {
    return codes.value.filter((code) =>
      code.toLowerCase().includes(input2.value.toLowerCase())
    );
  }

  if (input1.value != null && input2.value != "") {
    return codes.value.filter(
      (code) =>
        code.toLowerCase().includes(input1.value.toLowerCase()) &&
        code.toLowerCase().includes(input2.value.toLowerCase())
    );
  }

  return codes;
}
</script>
