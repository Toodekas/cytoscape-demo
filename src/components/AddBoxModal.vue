<template>
  <div class="modal">
    <h2>Add Box</h2>
    <input v-model="boxName" placeholder="Box Name" />
    <select v-model="boxType">
      <option value="name">Name</option>
      <option value="account">Account</option>
      <option value="financials">Financials</option>
      <option value="address">Address</option>
    </select>
    <button @click="addBox">Add Box</button>
  </div>
</template>

<script>
export default {
  name: "AddBoxModal",
  data() {
    return {
      boxName: "",
      boxType: "name",
    };
  },
  methods: {
    addBox() {
      this.$emit("add-box", { name: this.boxName, type: this.boxType });
      this.boxName = "";
      this.boxType = "name";
    },
  },
};
</script>
