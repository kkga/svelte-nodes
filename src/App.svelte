<script>
  import Node from "./lib/Node.svelte";
  import { graph } from "./lib/stores.js";
  import { connection_list } from "./lib/stores.js";

  function connect_nodes(node_a, node_b) {
    const connection = { from: node_a, to: node_b };
    connection_list.update((val) => [...val, connection]);
  }

  let nodes = [
    { id: 1, name: "apple" },
    { id: 2, name: "banana" },
    { id: 3, name: "carrot" },
    { id: 4, name: "doughnut" },
    { id: 5, name: "egg" },
  ];

  connect_nodes(1, 2);
  connect_nodes(2, 4);
</script>

{#each nodes as node (node.id)}
  <Node id={node.id} />
{/each}
