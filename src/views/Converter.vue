<template>
  <div class="converter">
    <div class="container">
      <h3>КОНВЕРТЕР ВАЛЮТ</h3>
      <form class="currency_form" action="">
        <div class="input-wrap">
          <label for="inner_currency">Міняю</label>
          <select
            name=""
            id="currency_choice"
            class="currency_choice"
            v-model="choiceCurrency"
          >
            <option v-bind:key="currency" v-for="currency in currencies">
              {{ currency.ccy }}
            </option>
          </select>
          <input
            v-bind:value="innerCurrency"
            @input="innerCurrencyMetod"
            class="currency_input"
            type="number"
            id="inner_currency"
            name="inner_currency"
            placeholder="0"
          />
        </div>
        <div class="input-wrap">
          <label for="outer_currency">Отримую</label>
          <input
            v-bind:value="outerCurrency"
            class="currency_input"
            type="text"
            id="outer_currency"
            name="outer_currency"
            placeholder="0.00"
          />
        </div>
      </form>
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
.container {
  max-width: 600px;
  margin: 0 auto;
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

