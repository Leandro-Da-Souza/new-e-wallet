<template>
  <div id="app">
    <div class="nav">
      <router-link to="/" tag="button">Card Stack</router-link>
      <router-link to="addCard" tag="button">Add Card</router-link>
    </div>
    <router-view :cards="cards" @addCard="addCard"></router-view>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      cards: [
        {
          cardNumber: "1234567891234567",
          cardName: "Leandro Da Souza",
          valid: "12-29",
          ccv: 742,
          vendor: "bitcoin",
        },
        {
          cardNumber: "1234567891234567",
          cardName: "Leandro Da Souza",
          valid: "12-29",
          ccv: 742,
          vendor: "blockchain",
        },
        {
          cardNumber: "1234567891234567",
          cardName: "Leandro Da Souza",
          valid: "12-29",
          ccv: 742,
          vendor: "ninja bank",
        },
        {
          cardNumber: "1234567891234567",
          cardName: "Leandro Da Souza",
          valid: "12-29",
          ccv: 742,
          vendor: "evilcorp",
        },
      ],
    };
  },
  methods: {
    addCard(newCard) {
      console.log(newCard);
      this.cards.push(newCard);
    },
    addId() {
      let id = 0;
      this.cards.forEach((card) => {
        card.id = id++;
      });
    },
  },
  created() {
    this.addId();
  },
  updated() {
    this.addId();
  },
};
</script>

<style>
</style>
