<template>
  <div>
    <cytoscape-box :elements="elements"></cytoscape-box>
    <button @click="showModal = true">Add Box</button>
    <add-box-modal v-if="showModal" @add-box="addBox"></add-box-modal>
  </div>
</template>

<script>
import CytoscapeBox from "./components/CytoscapeBox.vue";
import AddBoxModal from "./components/AddBoxModal.vue";

export default {
  name: "App",
  components: {
    CytoscapeBox,
    AddBoxModal,
  },
  data() {
    return {
      showModal: false,
      elements: [],
    };
  },
  methods: {
    addBox(box) {
      this.showModal = false;
      const colorMap = {
        name: "#f8cecc",
        account: "#dae8fc",
        financials: "#d5e8d4",
        address: "#f8e7e7",
      };
      const newBox = {
        group: "nodes",
        data: { id: box.name, name: box.name, color: colorMap[box.type] },
        position: { x: 400, y: 300 },
      };
      console.log(newBox);
      this.elements.push(newBox);
    },
  },
};
</script>
