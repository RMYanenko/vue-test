<template>
  <div class="container">
    <h1>КУРС ВАЛЮТ</h1>
    <div class="currency-list">
      <table>
        <thead>
          <tr>
            <th colspan="2">Валюти</th>
            <th>Купівля</th>
            <th>Продаж</th>
          </tr>
        </thead>
        <tbody>
          <tr v-bind:key="currency" v-for="currency in currencies">
            <td class="currency-ccy">
              {{ currency.ccy }}
            </td>
            <td>{{ currency.base_ccy }}</td>
            <td>{{ currency.buy }}</td>
            <td>{{ currency.sale }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      currencies: [],
      choiceCurrency: "USD",
      innerCurrency: "",
      outerCurrency: "",
    };
  },
  methods: {
    fetchCurrencies() {
      fetch("https://api.privatbank.ua/p24api/pubinfo?exchange&json&coursid=11")
        .then((response) => response.json())
        .then((data) => (this.currencies = data));
    },
    innerCurrencyMetod(event) {
      let num = event.target.value;
      this.innerCurrency = num;
      this.outerCurrency = num * 2;
    },
  },
  mounted() {
    this.fetchCurrencies();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

.currency-ccy {
  font-weight: 600;
}

.currency-list {
  table {
    width: 100%;
    thead {
      background-color: #fafafa;
      th {
        border-bottom: 1px solid #eeeff3;
        padding: 10px;
      }
    }
    td {
      border-bottom: 1px solid #eeeff3;
      padding: 5px;
    }
  }
}

.currency_input {
  width: 50%;
  padding: 5px;
  margin: 5px;
}

.currency_form {
  display: flex;
  justify-content: space-between;
}

.currency_choice {
  padding: 5px;
  margin: 5px;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
