<script lang="ts">
	 import AddCounter from './components/CounterAddButton.svelte'
    import Counter from './components/Counter.svelte'
    
	function getNewCounter(){
		return {name:"new",count:0,id:newid}
	}
	const newCounter = getNewCounter();
	
	let counters: {name:string,count:number,id:number}[] = [
	{
		name: 'new',
		count: 0,
		id: 0
	}
	];
	$: list_titles = counters.map((counter)=>counter.name);
	$: total = counters.length ? counters.map(item => item.count).reduce((prev, next) => prev + next) : 0;
	$: newid = counters.length ? Math.max(...(counters.map((c)=>c.id))) + 1 : 0;
;

	const addCounter = (e:any) => {
		
		const newCounter = {
			name: 'new',
			count: 0,
			id: newid
		}
		counters = [...counters, newCounter];
	}

	const removeCounter = (e:any) => {
		counters = counters.filter((counter)=> counter.id !== e.detail)
	}
</script>

<main>
	<div class="new">
	<h1 >Multiple Counter</h1>
	
		{#if counters.length === 0}
		<p>カウンターはありません</p>
		{:else}
		{#each counters as counter }
			<Counter 
			bind:name={counter.name}
			bind:count={counter.count}
			id={counter.id}
			on:remove={removeCounter}/>
		{/each}
		{/if}
		<div class="info">TITLE LIST:{list_titles}</div>
		<div class="info">SUM OF COUNT:{total}</div>
		<div>
			<AddCounter on:addcounter={addCounter} />
		</div>
	</div>

</main>

<style>
	h1{
		font-size: 4rem;display: block;    
    
	}
	main{
		text-align: center;
		padding:10px;
		margin:0px
	}
	.info{
	display: block;
		margin:20px;
		text-align: center;
		font-size:20px;
	}
	
	@media(min-width: 640px){
		main{
			max-width: none;
		}
	}

</style>