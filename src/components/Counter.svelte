<script lang="ts">
  import { createEventDispatcher } from "svelte";

  export let name: string;
  export let count: number;

  const dispatch = createEventDispatcher();

  const addPoint = () => {
    if (count < 100) {
      count += 1;
    }
  };
  const removePoint = () => {
    if (count > 0) {
      count -= 1;
    }
  };
  const resetPoint = () => (count = 0);
  const deleteCounter = () => {
    dispatch("remove");
  };
</script>

<div class="card">
  <input class="input" type="text" placeholder="new" bind:value={name} />
  <div class="h2">{count}</div>
  <button class="add" on:click={addPoint}>+</button>
  <button class="remove" on:click={removePoint}>-</button>
  <button class="reset" on:click={resetPoint}>0</button>
  <button class="delete" on:click={deleteCounter}>X</button>
</div>

<style>
  .input {
    background-color: white;
    border-radius: 5px;
  }
  .add {
    background-color: #f56565;
    border-radius: 5px;
  }
  .remove {
    background-color: #4299e1;
    border-radius: 5px;
  }
  .reset {
    background-color: #ecc94b;
    border-radius: 5px;
  }
  .delete {
    background-color: white;
    border-radius: 5px;
  }
  .h2 {
    margin-right: 5%;
    margin-left: 5%;
    width: 10%;
  }
  button {
    color: #333;
    padding: 8px;
    border-radius: 5x;
    width: 10%;
    display: flex;
    font-size: 20px;
    align-items: center;
    justify-content: center;
  }

  .card {
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    background-color: skyblue;
    border-radius: 10px;
    margin-right: auto;
    margin-left: auto;
    width: 90%;
  }
  input {
    width: 30%;
  }
</style>
