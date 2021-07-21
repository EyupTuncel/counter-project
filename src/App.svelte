<script lang="ts">
  import CounterAddButton from "./components/CounterAddButton.svelte";
  import Counter from "./components/Counter.svelte";

  function getNewCounter() {
    return { name: "new", count: 0, id: newid };
  }

  let counters: { name: string; count: number; id: number }[] = [
    getNewCounter(),
  ];
  $: listTitles = counters.map((counter) => counter.name);
  let total: Number;

  $: total = counters.reduce((total, counter) => total + counter.count, 0);

  $: newid = counters.length ? Math.max(...counters.map((c) => c.id)) + 1 : 0;
  const addCounter = (e: any) => {
    const newCounter = getNewCounter();
    counters = [...counters, newCounter];
  };

  function removeCounter(counterId: number) {
    counters = counters.filter((counter) => counter.id !== counterId);
  }
</script>

<main>
  <div class="new">
    <h1>Multiple Counter</h1>

    {#if counters.length}
      {#each counters as counter}
        <Counter
          bind:name={counter.name}
          bind:count={counter.count}
          bind:id={counter.id}
          on:remove={() => removeCounter(counter.id)}
        />
      {/each}
    {/if}
    <div class="info">TITLE LIST:{listTitles}</div>
    <div class="info">SUM OF COUNT:{total}</div>
    <div>
      <CounterAddButton on:click={addCounter} />
    </div>
  </div>
</main>

<style>
  h1 {
    font-size: 4rem;
    display: block;
  }
  main {
    text-align: center;
    padding: 10px;
    margin: 0px;
  }
  .info {
    display: block;
    margin: 20px;
    text-align: center;
    font-size: 20px;
  }

  @media (min-width: 640px) {
    main {
      max-width: none;
    }
  }
</style>
