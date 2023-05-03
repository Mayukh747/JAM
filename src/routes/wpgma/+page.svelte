<!-- <div class="tree">
	<ul>
		<li>
			<a href="#">1</a>
      
			<ul>
				<li>
					<a href="#">2</a>
					<ul>
            <li>
							<a href="#">2.1</a>
              
						</li>
						<li>
							<a href="#">2.2</a>
						</li>
					</ul>
				</li>
				<li>
					<a href="#">3</a>
					<ul>
						<ul>
            <li>
							<a href="#">3.1</a>
              <ul>
            <li>
							<a href="#">3.1.1</a>
						</li>
						<li>
							<a href="#">3.1.2</a>
						</li>
					</ul>
						</li>
						<li>
							<a href="#">3.2</a>
						</li>
					</ul>
					</ul>
				</li>
			</ul>


		</li>
	</ul>
</div> -->

<!-- <div class="bg-red-500">
	<div class="card w-96 glass">
		<figure><img src="jam.png" alt="car!"/></figure>
		<div class="card-body">
		  <h2 class="card-title">Life hack</h2>
		  <p>How to park your car at your garage?</p>
		  <div class="card-actions justify-end">
			<button class="btn btn-primary">Learn now!</button>
		  </div>
		</div>
	  </div>
</div> -->

<div class="hero min-h-screen bg-base-200">
	<div class="hero-content flex-col lg:flex-row-reverse">
	  <div class="text-center lg:text-left">
		<h1 class="text-5xl font-bold">BLAST 'em now!</h1>
		<p class="py-6">You give me accession #s, I give you fasta. It's an equivalent exchange.</p>
	</div>
	  <div class="card flex-shrink-0 w-full max-w-sm shadow-2xl bg-base-100">
		<div class="card-body">
		  <div class="form-control">
			<label class="label">
			  <span class="label-text">Accession #s</span>
			</label>
			<input type="text" placeholder="run me them #s" class="input input-bordered" />
		  </div>
		  <div class="form-control mt-6">
			<button class="btn btn-primary">Retrieve Sequences</button>
		  </div>
		</div>
	  </div>
	</div>
  </div>



<!-- <button on:click={() => fetchFastA(["AB282855","34577062","24475906"])}>FETCH</button>
<textarea placeholder="Bio" class="textarea textarea-bordered textarea-lg w-full max-w-xs" ></textarea> -->



<script>


/**
     * @param {string[] } [ids]
     */
async function fetchFastA(ids) {
	
  let stringIds = "";

  ids?.forEach(element => stringIds+= element + ",");
  stringIds = stringIds.substring(0, stringIds.length - 1);
  let results = [];

  const response = await fetch("https://eutils.ncbi.nlm.nih.gov/entrez/eutils/efetch.fcgi?db=nucleotide&id=" + stringIds + "&rettype=fasta&retmode=text");
  const text = await response.text();
  console.log(text);
}

</script>


<style>
  /*Now the CSS*/
* {margin: 0; padding: 0;}

.tree ul {
	padding-top: 20px; position: relative;
	
	transition: all 0.5s;
	-webkit-transition: all 0.5s;
	-moz-transition: all 0.5s;
}

.tree li {
	float: left; text-align: center;
	list-style-type: none;
	position: relative;
	padding: 20px 5px 0 5px;
	
	transition: all 0.5s;
	-webkit-transition: all 0.5s;
	-moz-transition: all 0.5s;
}

/*We will use ::before and ::after to draw the connectors*/

.tree li::before, .tree li::after{
	content: '';
	position: absolute; top: 0; right: 50%;
	border-top: 1px solid #ccc;
	width: 50%; height: 20px;
}
.tree li::after{
	right: auto; left: 50%;
	border-left: 1px solid #ccc;
}

/*We need to remove left-right connectors from elements without 
any siblings*/
.tree li:only-child::after, .tree li:only-child::before {
	display: none;
}

/*Remove space from the top of single children*/
.tree li:only-child{ padding-top: 0;}

/*Remove left connector from first child and 
right connector from last child*/
.tree li:first-child::before, .tree li:last-child::after{
	border: 0 none;
}
/*Adding back the vertical connector to the last nodes*/
.tree li:last-child::before{
	border-right: 1px solid #ccc;
	border-radius: 0 5px 0 0;
	-webkit-border-radius: 0 5px 0 0;
	-moz-border-radius: 0 5px 0 0;
}
.tree li:first-child::after{
	border-radius: 5px 0 0 0;
	-webkit-border-radius: 5px 0 0 0;
	-moz-border-radius: 5px 0 0 0;
}

/*Time to add downward connectors from parents*/
.tree ul ul::before{
	content: '';
	position: absolute; top: 0; left: 50%;
	border-left: 1px solid #ccc;
	width: 0; height: 20px;
}

.tree li a{
	border: 1px solid #ccc;
	padding: 5px 10px;
	text-decoration: none;
	color: #666;
	font-family: arial, verdana, tahoma;
	font-size: 11px;
	display: inline-block;
	
	border-radius: 5px;
	-webkit-border-radius: 5px;
	-moz-border-radius: 5px;
	
	transition: all 0.5s;
	-webkit-transition: all 0.5s;
	-moz-transition: all 0.5s;
}

/*Time for some hover effects*/
/*We will apply the hover effect the the lineage of the element also*/
.tree li a:hover, .tree li a:hover+ul li a {
	background: #c8e4f8; color: #000; border: 1px solid #94a0b4;
}
/*Connector styles on hover*/
.tree li a:hover+ul li::after, 
.tree li a:hover+ul li::before, 
.tree li a:hover+ul::before, 
.tree li a:hover+ul ul::before{
	border-color:  #94a0b4;
}
</style>