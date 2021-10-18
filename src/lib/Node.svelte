<script>
  import { transform } from "@babel/standalone";
  import { graph } from "./stores.js";
  import { connection_list } from "./stores.js";

  export let id;

  let input = 0;
  let expr;
  $: output = transform(expr, {}).code;

  $: graph.update((val) => {
    if (output) {
      val[id] = {
        output: output,
      };
    }
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
  | expr: <input bind:value={expr} />
  <!--  | add: <input type="number" bind:value={adder} />
--> -> {output}
</div>
