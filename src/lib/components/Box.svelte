<script>

 export let values = ["",false,false,false, "style"];



//Put some logic here regarding the type of box
//1. Blank  2. Tile 3. Default
 function determineStyle(){
    if (values[4] == "red"){
        return "bg-red-600";
    }
    else if(values[4] == "green"){
        return "bg-green-600";
    }
    else if(values[4] == "orange"){
        return "bg-orange-600";
    }
    else{
        return          "bg-blue-600"
    }
    
 }
</script>

<div class="{values[0] == "" ? "" : ""} {determineStyle()} rounded-2xl relative flex items-center justify-center w-20 h-20 border-black border-2">
    
    {#if values[1]}
    <img class ="absolute left-auto top-0 h-5" src="upArrow.svg" alt="up">
    {/if}

    {#if values[2]}
    <img class ="absolute left-0 top-0 h-5" src="diagArrow.svg" alt="diag">
    {/if}

    {#if values[3]}
    <img class ="absolute left-0 top-auto h-5" src="leftArrow.svg" alt="left">
    {/if}

    <h1 class="text-center text-2xl">{values[0]}</h1>
</div>