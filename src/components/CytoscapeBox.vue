<template>
  <div
    id="cy-container"
    style="width: 800px; height: 600px; border: 1px solid black"
  ></div>
</template>

<script>
import cytoscape from "cytoscape";

export default {
  name: "CytoscapeBox",
  props: {
    elements: Array,
  },
  data() {
    return {
      selectedNodes: [], 
    };
  },
  watch: {
    elements: {
      handler(elements) {
        this.cy.json({ elements });
      },
      deep: true,
    },
  },
  mounted() {
    this.cy = cytoscape({
      container: document.getElementById("cy-container"),
      elements: this.elements,
      style: [
        {
          selector: "node[name]",
          style: {
            shape: "rectangle", 
            width: "150px",
            height: "50px",
            "background-color": "data(color)",
            label: "data(name)",
            "text-valign": "center",
            "font-size": "14px",
            color: "#000",
          },
        },
        {
          selector: "edge",
          style: {
            "curve-style": "bezier",
            "target-arrow-shape": "triangle", 
            "line-color": "#000",
            "target-arrow-color": "#000",
            width: 2,
          },
        },
      ],
      layout: {
        name: "preset",
      },
    });

    this.cy.on("tap", "node", (event) => {
      const node = event.target;
      this.handleNodeClick(node);
    });
  },
  methods: {
    handleNodeClick(node) {
      this.selectedNodes.push(node.id());

      if (this.selectedNodes.length === 2) {
        const source = this.selectedNodes[0];
        const target = this.selectedNodes[1];

        this.cy.add({
          group: "edges",
          data: { source: source, target: target },
        });

        this.selectedNodes = [];
      }
    },
  },
};
</script>
