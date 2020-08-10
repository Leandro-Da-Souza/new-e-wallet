<template>
  <div>
    <form @submit.prevent="addCard">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" name="name" id="name" placeholder="Name" v-model="newCard.cardName" />
      </div>
      <div class="form-group">
        <label for="number">Number</label>
        <input
          type="text"
          name="number"
          id="number"
          placeholder="Number"
          v-model="newCard.cardNumber"
          maxlength="16"
        />
      </div>
      <div class="form-group">
        <label for="valid">Valid Thru</label>
        <input
          type="text"
          name
          id="valid"
          maxlength="5"
          v-model="newCard.valid"
          @keyup="insertHyphen($event)"
        />
      </div>
      <div class="form-group">
        <label for="ccv">CCV</label>
        <input type="text" name id maxlength="3" />
      </div>
      <div class="form-group">
        <label for="vendor">Vendor</label>
        <select id="vendor" v-model="newCard.vendor">
          <option value="bitcoin">Bitcoin</option>
          <option value="evilcorp">Evilcorp</option>
          <option value="ninja bank">Ninja Bank</option>
          <option value="blockchain">Blockchain</option>
        </select>
      </div>
      <div class="form-group">
        <button>Add</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "addCard",
  data() {
    return {
      newCard: {
        cardNumber: null,
        cardName: null,
        valid: null,
        ccv: null,
        vendor: null,
      },
    };
  },
  methods: {
    addCard() {
      this.$emit("addCard", this.newCard);
      this.$router.push("/");
    },
    insertHyphen(e) {
      console.log(e);
      var unicode = e.keyCode ? e.keyCode : e.charCode;
      if (unicode != 8) {
        // this avoids backspace to spoil your logic
        var textval = document.getElementById("valid").value;
        if (
          textval.length == 3 &&
          textval.charAt(1) != "-" &&
          textval.charAt(2) != "-"
        ) {
          // this case arises when backspace is used
          textval = textval.substring(0, 2) + "-" + textval.substring(2, 3);
          document.getElementById("valid").value = textval;
        } else if (textval.length == 2 && textval.charAt(1) != "-") {
          // normal case
          textval = textval + "-";
          document.getElementById("valid").value = textval;
        }
      } else if (
        unicode == 46 &&
        textval.length >= 3 &&
        textval.charAt(1) != "-" &&
        textval.charAt(2) != "-"
      ) {
        textval = textval.substring(0, 2) + "-" + textval.substring(2);
        document.getElementById("valid").value = textval;
      }
    },
  },
};
</script>

<style>
</style>