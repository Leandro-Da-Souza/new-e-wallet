<template>
  <div>
    <p class="active">Active Card</p>
    <section class="card" :style="{backgroundColor: bgColor}">
      <div class="upper">
        <img :src="vendorSrc" alt />
        <p>{{card.cardNumber | space}}</p>
        <img :src="chip" alt />
      </div>
      <div class="lower">
        <span>VALID THRU</span>
        {{card.valid}}
        <p>{{card.cardName}}</p>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  name: "activeCard",
  props: ["card"],
  methods: {},
  computed: {
    bgColor() {
      if (this.card.vendor === "bitcoin") {
        return "orange";
      } else if (this.card.vendor === "evilcorp") {
        return "darkred";
      } else if (this.card.vendor === "ninja bank") {
        return "gray";
      } else if (this.card.vendor === "blockchain") {
        return "blueviolet";
      }
      return "";
    },
    vendorSrc() {
      if (this.card.vendor === "bitcoin") {
        return require("../assets/vendor-bitcoin.svg");
      } else if (this.card.vendor === "evilcorp") {
        return require("../assets/vendor-evil.svg");
      } else if (this.card.vendor === "ninja bank") {
        return require("../assets/vendor-ninja.svg");
      } else if (this.card.vendor === "blockchain") {
        return require("../assets/vendor-blockchain.svg");
      }
      return "";
    },
    chip() {
      if (this.card.vendor === "evilcorp") {
        return require("../assets/chip-dark.svg");
      }
      return require("../assets/chip-light.svg");
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
.card {
  width: 45%;
  height: 220px;
  /* border: 1px solid #000; */
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 0 auto;
  text-align: center;
  box-shadow: 0 10px 16px rgba(0, 0, 0, 0.75);
}

.card img {
  width: 20px;
  height: 20px;
}

.active {
  text-align: center;
}

.upper {
  display: flex;
  width: 100%;
  justify-content: space-between;
}

.upper img {
  margin: 10px;
  margin-top: -20px;
  /* align-self: flex-start; */
}

.upper p,
.lower p {
  font-size: 20px;
}

.lower span {
  font-size: 10px;
}
</style>