<script>
    import Table from "./Table.svelte";

    export let mat = [[1,1],[1,1]];
</script>


<div class="overflow-x-auto">
    <table class="table table-compact w-full">
        <thead>
            <tr>
              <th></th> 
              <th>Name</th> 
              <th>Job</th> 
              <th>company</th> 
              <th>location</th> 
              <th>Last Login</th> 
              <th>Favorite Color</th>
            </tr>
        </thead> 
        <tbody>
        {#each mat as row}
        <tr>
        {#each row as val}
        <th>{val}</th>
        {/each}
        </tr>
        {/each}
        </tbody>
    </table>
</div>
