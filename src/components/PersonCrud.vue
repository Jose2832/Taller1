<template>
  <div class="q-pa-md">
    <!-- Formulario de registro -->
    <q-card class="q-mb-md">
      <q-card-section>
        <q-input
          v-model="newPerson.name"
          label="Nombre"
          outlined
          dense
        ></q-input>
        <q-input
          v-model="newPerson.lastName"
          label="Apellido"
          outlined
          dense
        ></q-input>
        <q-input
          v-model="newPerson.age"
          label="Edad"
          outlined
          dense
          type="number"
        ></q-input>
      </q-card-section>
      <q-card-actions>
        <q-btn color="primary" label="Registrar" @click="addPerson"></q-btn>
      </q-card-actions>
    </q-card>

    <!-- Lista de personas -->
    <q-card v-if="people.length > 0">
      <q-card-section class="text-h6">Lista de Personas</q-card-section>
      <q-card-section>
        <q-list bordered separator>
          <q-item v-for="(person, index) in people" :key="index">
            <q-item-section>
              <q-item-label
                >{ { person.name }} {{ person.lastName }},
                {{ person.age }}
              </q-item-label>
            </q-item-section>
            <q-item-section side>
              <q-btn
                @click="editPerson(index)"
                color="primary"
                icon="edit"
                flat
                dense
              ></q-btn>
              <q-btn
                @click="deletePerson(index)"
                color="negative"
                icon="delete"
                flat
                dense
              ></q-btn>
            </q-item-section>
          </q-item>
        </q-list>
      </q-card-section>
    </q-card>
    <q-card v-else>
      <q-card-section class="text-h6"
        >No hay personas registradas.</q-card-section
      >
    </q-card>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newPerson: {
        name: "",
        lastName: "",
        age: "",
      },
      editIndex: null,
      people: [],
    };
  },
  methods: {
    addPerson() {
      if (
        this.newPerson.name.trim() !== "" &&
        this.newPerson.lastName.trim() !== "" &&
        this.newPerson.age.trim() !== ""
      ) {
        this.people.push({ ...this.newPerson });
        this.resetForm();
      }
    },
    editPerson(index) {
      this.editIndex = index;
      this.newPerson = { ...this.people[index] };
    },
    updatePerson() {
      if (
        this.newPerson.name.trim() !== "" &&
        this.newPerson.lastName.trim() !== "" &&
        this.newPerson.age.trim() !== ""
      ) {
        this.people.splice(this.editIndex, 1, { ...this.newPerson });
        this.resetForm();
      }
    },
    deletePerson(index) {
      if (confirm("¿Estás seguro de que deseas eliminar esta persona?")) {
        this.people.splice(index, 1);
      }
    },
    resetForm() {
      this.newPerson = {
        name: "",
        lastName: "",
        age: "",
      };
      this.editIndex = null;
    },
  },
};
</script>

<style scoped>
.q-pa-md {
  padding: 16px;
}
.q-mb-md {
  margin-bottom: 16px;
}
</style>
