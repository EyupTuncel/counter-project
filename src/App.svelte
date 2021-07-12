<script lang="ts">
	 import AddCounter from './components/AddCounter.svelte'
    import Counter from './components/Counter.svelte'
    
	
	$: counters = [
	{
		name: 'new',
		value: 0,
		id: 0
	}
	];
	$: list = counters.map((counter)=>counter.name).join(',');
	$: gokei = counters.length ? counters.map(item => item.value).reduce((prev, next) => prev + next) : 0;
	$: newid = counters.length ? Math.max(...(counters.map((c)=>c.id))) + 1 : 0;
;

	const addCounter = (e:any) => {
		
		const newCounter = {
			name: 'new',
			value: 0,
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
	<h1 style="font-size: 4rem;display: block;    
    ">Multiple Counter</h1>
	
		{#if counters.length === 0}
		<p>カウンターはありません</p>
		{:else}
		{#each counters as counter }
			<Counter 
			bind:name={counter.name}
			bind:value={counter.value}
			id={counter.id}
			on:removecounter={removeCounter}/>
		{/each}
		{/if}
		<div class="info"><span>TITLE LIST:{list}</span></div>
		<div class="info"><span>SUM OF COUNT:{gokei}</span></div>
		<div>
			<AddCounter on:addcounter={addCounter} />
		</div>
	</div>

</main>

<style>
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