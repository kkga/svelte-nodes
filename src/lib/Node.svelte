<script>
  import { graph } from "./stores.js";
  import { connection_list } from "./stores.js";

  export let id;

  let input = 0;
  $: output = input + adder;

  let adder = 0;

  $: graph.update((val) => {
    val[id] = {
      output: output,
    };
    return val;
  });

  graph.subscribe((_value) => {
    $connection_list.forEach((conn) => {
      if (conn.to === id) {
        if ($graph[conn.from] != undefined) {
          input = $graph[conn.from].output;
        }
      }
    });
  });
</script>

<div style="border: 1px solid; margin: 1rem;">
  <span>
    id: {id}
    | input: {input}
  </span>
  | add: <input type="number" bind:value={adder} />
  -> {output}
</div>
