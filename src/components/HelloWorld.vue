<template>
  <div class="container">
    <h1>Formulaire de Vente</h1>
    <form @submit.prevent="addVent">
      <div class="row col-md-5">
        <label for="reference" class="form-label">Reference :</label>
        <input type="text" class="form-control" id="reference" v-model="reference">
      </div>
      <div class="row col-md-5">
        <label for="designation" class="form-label">Designation :</label>
        <input type="text" class="form-control" id="designation" v-model="designation">
      </div>
      <div class="row col-md-5">
        <label for="quantite" class="form-label">Quantite :</label>
        <input type="number" class="form-control" id="quantite" v-model="quantite">
      </div>
      <div class="row col-md-5">
        <label for="prix" class="form-label">Prix :</label>
        <input type="number" class="form-control" id="prix" v-model="prix">
      </div>
      <button type="submit" class="btn btn-primary" id="ajout">Ajouter</button>
    </form>

    <table class="table">
      <thead>
        <tr>
          <th>Reference</th>
          <th>Designation</th>
          <th>Quantite</th>
          <th>Prix</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(list, index) in lists" :key="index">
          <td>{{ list.reference }}</td>
          <td>{{ list.designation }}</td>
          <td>{{ list.quantite }}</td>
          <td>{{ list.prix }}</td>
        </tr>
      </tbody>
    </table>
    <p v-if="message" :class="error ? 'red' : 'green'">{{ message }}</p>
  </div>
</template>

<script setup>
import { ref } from "vue";

const reference = ref('');
const designation = ref('');
const quantite = ref(null);
const prix = ref(null);
const lists = ref([]);
const message = ref();
let error = false;

function addVent() {
  if (reference.value === '' || designation.value === '' || quantite.value === null || prix.value === null) {
    // alert("Vous ne pouvez pas ajouter une tâche vide");
    error = true;
    message.value="Vous ne pouvez pas ajouter une tâche vide";
  } else {
    error = false;
    lists.value.push({
      reference: reference.value,
      designation: designation.value,
      quantite: quantite.value,
      prix: prix.value
    });
    reference.value = '';
    designation.value = '';
    quantite.value = null;
    prix.value = null;
    message.value="Les champs ont été ajouter avec sucsé";
  }
}
</script>

<style>
table.table {
  border: 1px solid black;
  border-collapse: collapse;
  width: 40%;
  margin-top: 20px;
}

table.table th,
table.table td {
  border: 1px solid black;
  padding: 8px;
  text-align: left;
}
#ajout{
  width: 40%;
  margin-top: 20px;
}
.red{
  color: red;
}
.green{
  color: green;
}
</style>
