<script>
    import Box from "./Box.svelte";

    export let table = [[]];
    
    export function y(){
      console.log("YEA");
    }
    
</script>

<table>
    {#each table as r}
    <tr>
      {#each r as v}
        <td><Box values={v}/></td>
      {/each}
    </tr>

    {/each}
  </table>