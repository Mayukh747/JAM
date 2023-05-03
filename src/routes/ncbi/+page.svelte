<script>

    function get(){

    }


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
        

<textarea placeholder="Bio" class="textarea textarea-bordered textarea-lg w-full max-w-xs" ></textarea>