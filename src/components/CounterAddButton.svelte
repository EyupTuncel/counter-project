<script lang="ts">
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function addNewCounter(e: any) {
    e.preventDefault();
    dispatch("addcounter");
  }
</script>

<button class="add" on:click>new counter</button>

<style>
  .add {
    background-color: #68d391;
    width: 80%;
  }
</style>
