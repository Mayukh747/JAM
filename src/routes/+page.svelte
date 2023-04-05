<!-- <h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p> -->

<!-- <h1 class=" text-cyan-400 text-3xl font-bold underline italic">
    Hello world!
</h1>
<button class="btn">Button</button>
  
  <style lang="postcss">
    :global(html) {
      background-color: theme(colors.gray.100);
    }
  </style> -->


  <script>
    import Box from "$lib/components/Box.svelte";
    import { sequence } from "@sveltejs/kit/hooks";
    import { each } from "svelte/internal";
    const array = [[, 0], [-1, 3]]   

    let headers = "If you do what you've always done you'll get what you've always gotten";
    const words = headers.split(' ');

    let seqA = '';
    let seqB = '';
    let renderTable = true;
    /**
     * @type {any[]}
     */
    let table = [];

    /**
     * @param {string} s1
     * @param {string} s2
     */
    function initializeMatrix(s1, s2){

      table = Array.from({ length: s1.length+2 }, () => Array.from({ length: s2.length + 2 }, () => ["",false,false, false]));

      table[1][1][0] = '0';
      let val = 0;
      for(let col = 0; col < s2.length; col++){
        table[0][col+2][0] = s2.charAt(col);
        val-=2;
        table[1][col+2][0] = val.toString();
      }
      val = 0;
      for(let row = 0; row < s1.length; row++){
        table[row+2][0][0] = s1.charAt(row);
        val-=2
        table[row+2][1][0] = val.toString();
      }
    }

    /**
     * @param {string} s1
     * @param {string} s2
     */
    function needlemanWunsch(s1, s2){
      initializeMatrix(s1,s2);

      for(let idx = 2; idx < Math.min(table.length, table[0].length); idx++){
        //Row
        for(let col = idx; col < table[0].length; col++){
          solveCellNeedlemanWunsch(idx, col);
          // table[idx][col] = ["3", false, false, false];
        }
        //Col
        for(let row = idx + 1; row < table.length; row++){
          solveCellNeedlemanWunsch(row, idx);
          // table[row][idx] = ["2", false, false, false];
        }
        
      }
    }

    /**
     * @param {number} row
     * @param {number} col
     */
    function solveCellNeedlemanWunsch(row, col){
      let topVal = table[row-1][col][0];
      let diagVal = table[row-1][col-1][0];
      let leftVal = table[row][col-1][0];

      let minVal = Math.min(topVal, diagVal, leftVal);

      table[row][col] = [minVal.toString(), topVal==minVal, diagVal==minVal, leftVal==minVal];
    }


  </script>

  <!-- {@debug table} -->

<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">What is your first nucleotide sequence?</span>
  </label>
  <input bind:value={seqA} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>seqA = {seqA}
</div>
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">What is your second nucleotide sequence?</span>
  </label>
  <input bind:value={seqB} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>seqB = {seqB}
</div>
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Match Score</span>
  </label>
  <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
</div>
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Mismatch Score</span>
  </label>
  <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
</div>
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Gap Score</span>
  </label>
  <input type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
</div>

<button  on:click={() => needlemanWunsch(seqA,seqB)} class="btn btn-wide">Compute Optimal Alignment</button>

<!-- <button  on:click={() => needlemanWunsch(seqA, seqB)} class="btn btn-wide">Compute Optimal Alignment</button> -->

  <!-- <table>
    {#each words as w}
    <th class=" border-black border-4">{w}</th>
    {/each}

    {#each array as r}
    <tr>
      {#each r as val}
        <td>{val}</td>
      {/each}
    </tr>
    {/each}
  </table> -->



  <!-- {#if renderTable}
  <table>
    {#each array as r}
    <tr>
      {#each r as val}
        <td>{val}</td>
      {/each}
    </tr>
    {/each}
  </table>
  {/if} -->


  <table>
    {#each table as r}
    <tr>
      {#each r as v}
        <td><Box values={v}/></td>
      {/each}
    </tr>

    {/each}
  </table>
  

  <!-- <Box values={["42",false,false,false]}/> -->