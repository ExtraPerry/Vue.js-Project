<script>
    export default {    //Data variables.
      data: function () {
        return {
          date: null,
          montant: null,
          description: null,
          transactions: [],
        };
      },

      methods: {    //Methods to call.
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

<template>

    <table> <!-- Generate a table element here -->

      <thead>   <!-- Title of columbs -->
        <tr>
          <th>Date</th>
          <th>Montant</th>
          <th>Description</th>
        </tr>
      </thead>

      <tbody>   <!-- Generated table elements, using v-for -->

        <tr v-for="transaction in transactions">
            <td>
                {{ new Intl.DateTimeFormat('fr-FR').format(new Date(transaction.date)) }}
            </td>
            <td>
                {{ transaction.montant }}
            </td>
            <td>
            {{ transaction.description }}
            </td>
        </tr>

      </tbody>

    </table>    <!-- End of Table -->

    <header> <!-- Input elements with button to add to the table. -->
      <div>
        Date : <input type="date" v-model="date" /> <br />
        Montant : <input type="number" v-model="montant" /> <br />
        Description : <input type="text" v-model="description" /> <br />
        <button v-on:click="ajouter">Enregistrer</button>
      </div>
    </header>

</template>

<style>
    table, th, td {
        border: 1px solid black;
    }
</style>