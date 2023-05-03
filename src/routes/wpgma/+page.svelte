<script>
    import DMatrix from "$lib/components/DMatrix.svelte";

    let dMatArr = [[1,2,3]]
</script>
<div class="carousel carousel-center mx-10 py-10 space-x-4 bg-neutral rounded-box">
    <div class="carousel-item w-1/2">
        <img src="jam.png" class="w-full" />
    </div> 
    <div class="carousel-item w-1/2">
        <img src="jam.png" class="w-full" />
    </div> 
    <div class="carousel-item w-1/2">
        <img src="jam.png" class="w-full" />
    </div> 
    <div class="carousel-item w-1/2">
        <DMatrix
        mat = {[[2,2],[2,3]]}/>
    </div> 
</div>

<DMatrix
mat = {[[2,2],[2,3]]}/>
