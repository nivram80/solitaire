<script>
  export let size = "large";
</script>

<svg
  class={`diamond ${size}`}
  version="1.1"
  xmlns="http://www.w3.org/2000/svg"
  width="56"
  height="56"
  fill="red"
  viewBox="0 0 32 32">
  <title>diamonds</title>
  <path d="M16 0l-10 16 10 16 10-16z" />
</svg>

<style>
  .small {
    width: 12px;
    height: 12px;
  }

  .large {
    width: 56px;
    height: 56px;
  }
</style>