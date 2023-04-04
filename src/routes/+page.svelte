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
import { each } from "svelte/internal";
    const array = [[, 0], [-1, 3]]   

    let headers = "If you do what you've always done you'll get what you've always gotten";
    const words = headers.split(' ');

    let seqA = '';
    let seqB = '';
    let renderTable = true;

    function initializeMatrix(s1,s2){
      /**
         * @type {any[]}
         */
      let mat = [];
      for(let row = 0; row < s1.length + 2; row++){
        /**
           * @type {any[]}
           */
        let arr = [];
        for(let col = 0; col < s2.length + 2; col++){
        
        }
        mat.append(arr);
      }
      return mat;
    }

    function needlemanWunsch(s1, s2){
      alert("alignmnet algo triggered!");
      // /**
      //    * @type {never[]}
      //    */
      // let mat = [];
      // for(let i: i < s2.length; i++){

      // }
      // return mat;
    }

  </script>

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

<button  class="btn btn-wide">Compute Optimal Alignment</button>

  <table>
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
  </table>



  {#if renderTable}
  <table>
    {#each array as r}
    <tr>
      {#each r as val}
        <td>{val}</td>
      {/each}
    </tr>
    {/each}
  </table>
  {/if}

  <Box values={["42",false,false,false]}/>