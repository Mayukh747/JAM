
<script>
  import Box from "$lib/components/Box.svelte";
    import Table from "$lib/components/Table.svelte";
  import { sequence } from "@sveltejs/kit/hooks";
  import { each } from "svelte/internal";
  const array = [[, 0], [-1, 3]]   

  // let headers = "If you do what you've always done you'll get what you've always gotten";
  // const words = headers.split(' ');

  let seqA = 'duck';
  let seqAOptimal = "";
  let seqBOptimal = "";
  let seqB = 'trump';
  let match = 1;
  let mismatch = -1;
  let gap = -2;

  let animationSpeed = 500;
  let renderTable = true;
  /**
   * @type {any[]}
   */
  let table = [[]];

  function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }

  /**
   * @param {string} s1
   * @param {string} s2
   */
  function initializeMatrix(s1, s2){

    //[score, up, diag, left, style, distance]
    table = Array.from({ length: s1.length+2 }, () => Array.from({ length: s2.length + 2 }, () => ["",false,false,false, "", 0]));

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

    //To make the top left 3 square visible
    table[0][0][0] = " ";
    table[0][1][0] = " ";
    table[1][0][0] = " ";

  }

  /**
   * @param {string} s1
   * @param {string} s2
   * @param {number} speed
   */
  async function needlemanWunsch(s1, s2, speed){
    initializeMatrix(s1,s2);

    //Solve all the cells in the table. 
    for(let idx = 2; idx < Math.min(table.length, table[0].length); idx++){
      //Row
      for(let col = idx; col < table[0].length; col++){
        
        // await new Promise(r => setTimeout(r, 100));
        // sleep(1000);
        // await sleep(1 * 1000);
        table[idx][col-1][4] = "green";
        table[idx-1][col-1][4] = "green";
        table[idx-1][col][4] = "green";
        solveCellNeedlemanWunsch(idx, col, speed);
        await sleep(speed);
        table[idx][col-1][4] = "blue";
        table[idx-1][col-1][4] = "blue";
        table[idx-1][col][4] = "blue";

      }
      //Col
      for(let row = idx + 1; row < table.length; row++){
        // solveCellNeedlemanWunsch(row, idx, speed);
        table[row][idx-1][4] = "green";
        table[row-1][idx][4] = "green";
        table[row-1][idx-1][4] = "green";
        solveCellNeedlemanWunsch(row, idx, speed);
        await sleep(speed);
        table[row][idx-1][4] = "blue";
        table[row-1][idx][4] = "blue";
        table[row-1][idx-1][4] = "blue";
      } 
    }

    //Perform Traceback for the optimal alignment
    let row_idx = table.length-1;
    let col_idx = table[0].length-1;
    while(row_idx != 1 || col_idx != 1){
      // console.log("yes");
      table[row_idx][col_idx][4] = "red";
      await new Promise(r => setTimeout(r, 100));

      //Choose Up
      if(col_idx == 1 || table[row_idx][col_idx][1]){
        row_idx--;
      }
      //Choose Left
      else if(row_idx == 1 || table[row_idx][col_idx][3]){
        col_idx--;
      }
      //Choose Diag
      else {
        row_idx--;
        col_idx--;
      }
    }


    //Now that the Traceback is complete, traverse the table and change the colors
  }

  /**
   * @param {number} row
   * @param {number} col
   * @param {number} speed
   */
  async function solveCellNeedlemanWunsch(row, col, speed){

    // console.log(gap + " " + typeof(gap));
    let topVal = Number(table[row-1][col][0]) + Number(gap);
    let diagVal = Number(table[row-1][col-1][0]) + (table[row][0][0]==table[0][col][0] ? Number(match) : Number(mismatch));
    let leftVal = Number(table[row][col-1][0]) + Number(gap);
    
    let cellScore = Math.max(topVal, diagVal, leftVal);
    

    table[row][col] = [cellScore.toString(), topVal==cellScore, diagVal==cellScore, leftVal==cellScore];

    

  }


  /**
   * Given a pwa table, find the alignment with the smallest distance
  */
 function getOptimalAlignment(row, col, ){

 }
  

</script>

  <!-- {@debug table} -->
<div class="bg-pink-300">
<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">What is your first nucleotide sequence?</span>
  </label>
  <input bind:value={seqA} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  <!-- </label>seqA = {seqA} -->
</div>


<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">What is your second nucleotide sequence?</span>
  </label>
  <input bind:value={seqB} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  <!-- </label>seqB = {seqB} -->
</div>


<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Match Score</span>
  </label>
  <input bind:value={match} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
  <!-- match = {match} -->
</div>


<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Mismatch Score</span>
  </label>
  <input bind:value={mismatch} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
  <!-- mismatch = {mismatch} -->
</div>


<div class="form-control w-full max-w-xs">
  <label class="label">
    <span class="label-text">Gap Score</span>
  </label>
  <input bind:value={gap} type="text" placeholder="Type here" class="input input-bordered w-full max-w-xs" />
  <label class="label">
  </label>
  <!-- gap = {gap} -->
</div>

<button  on:click={() => needlemanWunsch(seqA,seqB, animationSpeed)} class="btn btn-wide">Compute Optimal Alignment</button>


<br>
<!-- bruh this slider gay -->
<input bind:value={animationSpeed} type="range" min="100" max="1000"  class="range" step="250" />
<div class="w-full flex justify-between text-xs px-2">
  <span>|</span>
  <span>|</span>
  <span>|</span>
  <span>|</span>
  <span>|</span>
</div>
<!-- {animationSpeed} -->

<Table table={table}/>
</div>

