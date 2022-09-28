<script>
    export default {    //Data variables.
      data: function () {
        return {
          nextId: 0,
          date: null,
          price: null,
          description: null,
          transactions: [],
          errorMsg: null,
        };
      },

      methods: {    //Methods to call.
        ajouter: function () {
            if(this.date && this.price && this.description){
                this.transactions.push({
                    id: this.nextId,
                    date: this.date,
                    price: this.price,
                    description: this.description,
                });

                ["date", "price", "description"].forEach(
                    (attr) => (this[attr] = null)
                );
                this.errorMsg = "";
                this.nextId++;
            }else{
                this.errormsg = "No field should be left empty.";
            }
        },

        supprimer: function(transactionId) {
            this.transactions.splice(transactionId, 1);
        },

        formatDate: function(date) {
        return new Intl.DateTimeFormat('fr-FR').format(new Date(date));
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
      <!----->
      <tbody>   <!-- Generated table elements, using v-for -->

        <tr v-for="transaction, idx in transactions" :key="transaction.id">
            <td>
                {{ formatDate(transaction.date) }}
            </td>
            <td>
                {{ transaction.price }}
            </td>
            <td>
                {{ transaction.description }}
            </td>
            <td>
                <button v-on:click="supprimer(idx)">Supprimer</button>
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

    <span v-if="errorMsg">{{this.errorMsg}}</span>

</template>

<style>
    table, th, td {
        border: 1px solid black;
    }
</style>