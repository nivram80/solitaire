<script>
  import Heart from "./Heart.svelte";
  import Spade from "./Spade.svelte";
  import Diamond from "./Diamond.svelte";
  import Club from "./Club.svelte";

  export let suit;
  export let value;
</script>

<div class={`card ${suit}`}>
  <div class="value">
    {value}
    {#if suit === "heart"}
      <Heart size="small" />
    {:else if suit === "spade"}
      <Spade size="small" />
    {:else if suit === "diamond"}
      <Diamond size="small" />    
    {:else if suit === "club"}
      <Club size="small" />  
    {/if}
  </div>
  <div class="suit">
    {#if suit === "heart"}
      <Heart />
    {:else if suit === "spade"}
      <Spade />
    {:else if suit === "diamond"}
      <Diamond />    
    {:else if suit === "club"}
      <Club />  
    {/if}
  </div>
</div>

<style>
  .card {
    box-sizing: border-box;
    width: 80px;
    height: 120px;
    border-radius: 4px;
    box-shadow: 0 0 2px rgba(0, 0, 0, 0.5);
    padding: 4px 6px;
    background-color: #fffefe;
  }

  .heart .value, .diamond .value {
    color: #b50303;
  }

  .club .value, .spade .value {
    color: black
  }

  .value {
    text-transform: uppercase;
  }

  .suit {
    margin-top: 16px;
    text-align: center;
  }
</style>

