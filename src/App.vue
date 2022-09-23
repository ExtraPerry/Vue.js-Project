<script>
    export default {    //Data variables.
      data: function () {
        return {
          date: null,
          price: null,
          description: null,
          transactions: [],
        };
      },

      methods: {    //Methods to call.
        ajouter: function () {
            if(this.date != null && this.price != null && this.description != null){
                this.transactions.push({
                    date: this.date,
                    price: this.price,
                    description: this.description,
                });

                ["date", "price", "description"].forEach(
                    (attr) => (this[attr] = null)
                );
            }else{
                this.errormsg = "No field should be left empty.";
            }
        },
      },
    };
</script>

<template>

    <table> <!-- Generate a table element here -->

      <thead>   <!-- Title of columbs -->
        <tr>
          <th>Date</th>
          <th>Price</th>
          <th>Description</th>
        </tr>
      </thead>

      <tbody>   <!-- Generated table elements, using v-for -->

        <tr v-for="transaction in transactions">
            <td>
                {{ new Intl.DateTimeFormat('fr-FR').format(new Date(transaction.date)) }}
            </td>
            <td>
                {{ transaction.price }}
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
        Price : <input type="number" v-model="price" /> <br />
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