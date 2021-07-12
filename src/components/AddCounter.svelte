<script lang="ts">
    import { createEventDispatcher } from 'svelte'

const dispatch = createEventDispatcher();

function addNewCounter(e:any){
    e.preventDefault();
    dispatch("addcounter");
}
	
</script>

<main>
<button class="add" on:click={addNewCounter}>new counter</button>	
</main>

<style>
	.add{
        background-color: #68d391;
        width: 80%;
    }
</style>