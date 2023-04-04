<script>

//Put some logic here regarding the type of box
//1. Blank  2. Tile 3. Default

 export let values = ["",false,false,false];

</script>

<div class="relative flex items-center justify-center w-20 h-20 border-black border-2">
    <img class ="absolute left-0 top-0 h-5" src="diagArrow.svg" alt="diag">
    <img class ="absolute left-auto top-0 h-5" src="upArrow.svg" alt="up">
    <img class ="absolute left-0 top-auto h-5" src="leftArrow.svg" alt="left">
    <h1 class="text-center text-2xl">{values[0]}</h1>
</div>