<template>
  <div class="wrapper">
    <h1>Conversor 🇧🇷 ⇢ 🇺🇸</h1>
    <v-form>
      <v-row justify="center" class="align-center">
        <v-col cols="12" md="12">
          <v-text-field
            label="Quantidade (R$)"
            type="number"
            focused
            v-model="real"
            required
            :rules="[(v) => !!v || 'Item is required']"
            placeholder="Digite o valor em Reais"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="12">
          <v-text-field
            label="Valor do Câmbio (R$)"
            type="number"
            mask="#.##"
            :rules="[(v) => !!v || 'Item is required']"
            required
            v-model="valorCambio"
            placeholder="Digite o valor atual do Dolar"
          ></v-text-field>
        </v-col>
        <v-col cols="12" md="12">
          <v-btn
            elevation="0"
            class="mr-3"
            color="teal-darken-1"
            @click="calcular()"
            >Calcular</v-btn
          >
          <v-btn elevation="0" color="teal-darken-0" @click="limpar()"
            >Limpar</v-btn
          >
        </v-col>
      </v-row>

      <v-row v-if="dolar" class="box">
        <v-col cols="12" md="12">
          <h3>Valor convertido</h3>
          Com R$ {{ real }} é possível comprar US$ {{ dolar }} dólares à R$
          {{ valorCambio }} cada
        </v-col>
      </v-row>
    </v-form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "CambioComponent",
  data() {
    return {
      real: undefined,
      dolar: undefined,
      valorCambio: undefined,
    };
  },
  mounted() {
    this.getDollarApi();
  },
  methods: {
    getDollarApi() {
      const api = axios.create({
        baseURL: "https://economia.awesomeapi.com.br/last/",
      });
      new Promise(() => {
        return api
          .get("USD-BRL")
          .then((response) => {
            let valor = response.data.USDBRL.bid;
            this.valorCambio = parseFloat(valor).toFixed(2);
          })
          .catch((error) => console.log(error));
      });
    },
    calcular() {
      this.dolar = this.real / this.valorCambio;
      this.dolar = parseFloat(this.dolar.toFixed(2));
    },
    limpar() {
      this.dolar = undefined;
      this.real = undefined;
      this.valorCambio = undefined;
    },
  },
};
</script>

<style scoped>
h1 {
  padding: 20px 0;
}
.wrapper {
  padding: 25px 0;
  width: 300px;
  margin: 0 auto;
}
.box {
  border: 1px solid #d7d7d7;
  background: #fafafa;
  padding: 20px;
  margin: 5px;
  border-radius: 8px;
}
</style>