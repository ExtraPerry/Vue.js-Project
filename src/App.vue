<script>
export default {
  data: function () {
    return {
      date: null,
      montant: null,
      description: null,
      transactions: [],
    };
  },
  methods: {
    ajouter: function () {
      this.transactions
        .push({
          date: this.date,
          montant: this.montant,
          description: this.description,
        });
        ["date", "montant", "description"].forEach(
          (attr) => (this[attr] = null)
        );
    },
  },
};
</script>

<style></style>

<template>
  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Montant</th>
        <th>Description</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="transaction in transactions">
        <td>
          {{ transaction.date }}
        </td>
        <td>
          {{ transaction.montant }}
        </td>
        <td>
          {{ transaction.description }}
        </td>
      </tr>
    </tbody>
  </table>
  <header>
    <div>
      Date : <input type="date" v-model="date" /> <br />
      Montant : <input type="number" v-model="montant" /> <br />
      Description : <input type="text" v-model="description" /> <br />
      <button v-on:click="ajouter">Enregistrer</button>
    </div>
  </header>
</template>