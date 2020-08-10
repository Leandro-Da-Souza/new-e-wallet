<template>
  <div>
    <ActiveCard :card="activeCard" />
    <p class="cardstack">Card Stack</p>
    <ul class="stack-cards">
      <li
        class="stack-card-item"
        v-for="card in cards"
        :key="card.id"
        @click="displayCard(card)"
        :style="{backgroundColor: bgColor(card) }"
      >
        <section class="card">
          <div class="upper">
            <img :src="vendorSrc(card)" alt />
            <p>{{card.cardNumber | space}}</p>
            <img :src="chip(card)" alt />
          </div>
          <div class="lower">
            <span>VALID THRU</span>
            {{card.valid}}
            <p>{{card.cardName}}</p>
          </div>
        </section>
      </li>
    </ul>
  </div>
</template>

<script>
import ActiveCard from "./ActiveCard.vue";

export default {
  name: "cardStack",
  props: ["cards"],
  data() {
    return {
      isActiveCard: null,
    };
  },
  components: {
    ActiveCard,
  },
  computed: {
    activeCard() {
      if (this.isActiveCard === null) {
        return this.cards[0];
      } else {
        return this.isActiveCard;
      }
    },
  },
  methods: {
    displayCard(card) {
      this.isActiveCard = card;
      window.scrollTo(0, 0);
    },
    bgColor(card) {
      if (card.vendor === "bitcoin") {
        return "orange";
      } else if (card.vendor === "evilcorp") {
        return "darkred";
      } else if (card.vendor === "ninja bank") {
        return "gray";
      } else if (card.vendor === "blockchain") {
        return "blueviolet";
      }
      return "";
    },
    vendorSrc(card) {
      if (card.vendor === "bitcoin") {
        return require("../assets/vendor-bitcoin.svg");
      } else if (card.vendor === "evilcorp") {
        return require("../assets/vendor-evil.svg");
      } else if (card.vendor === "ninja bank") {
        return require("../assets/vendor-ninja.svg");
      } else if (card.vendor === "blockchain") {
        return require("../assets/vendor-blockchain.svg");
      }
      return "";
    },
    chip(card) {
      if (card.vendor === "evilcorp") {
        return require("../assets/chip-dark.svg");
      } else {
        return require("../assets/chip-light.svg");
      }
    },
  },
  filters: {
    space(str, after) {
      if (!str) {
        return false;
      }
      after = after || 4;
      var v = str.replace(/[^\dA-Z]/g, ""),
        reg = new RegExp(".{" + after + "}", "g");
      return v.replace(reg, function (a) {
        return a + " ";
      });
    },
  },
};
</script>

<style scoped>
ul li {
  list-style-type: none;
}

.stack-cards {
  /* position: relative; */
  margin: auto;
  height: 300px;
  display: flex;
  flex-direction: column;
  /* justify-content: center; */
  align-items: center;
  margin-right: 40px;
}
.stack-card-item {
  width: 50%;
  height: 100%;
  /* border: 1px solid #000; */
  /* position: relative; */
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  /* margin: 0 auto; */
  /* position: sticky; */
  top: 0.75;
  text-align: center;
  box-shadow: 0 10px 16px rgba(0, 0, 0, 0.75);
  margin-top: 10px;
}
.upper img {
  margin: 10px;
  height: 20px;
  width: 20px;
  /* position: sticky; */
}

.upper {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

.upper p,
.lower p {
  font-size: 20px;
}

.lower span {
  font-size: 10px;
}
.cardstack {
  text-align: center;
}
</style>