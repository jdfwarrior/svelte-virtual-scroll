<script>
  import { onMount } from "svelte";
  import VirtualRow from "./VirtualRow.svelte";

  export let wrapperHeight = "500px";
  export let wrapperWidth = "1000px";
  export let items = [];

  let scrollTop = 0;
  let rendered = items;
  let innerHeight = 0;
  let ele;

  // auto updates the slice when scrollTop changes
  $: updateSlice(scrollTop);
  // auto updates innerHeight when the length of the data changes
  $: innerHeight = `${items.length * 25}px`;
  // auto updates the slice when ele becomes defined
  $: if (ele) updateSlice();

  function updateSlice() {
    const height = ele ? parseInt(ele.clientHeight) : 100;
    const init = scrollTop / 25;
    const end = Math.ceil((scrollTop + height) / 25);
    rendered = items.slice(init, end + 15);
  }

  function updateScroll($event) {
    scrollTop = $event.target.scrollTop;
  }
</script>

<style>
  .virtual-wrapper {
    overflow-y: scroll;
    margin: 0 auto;
  }
  .inner-wrapper {
    overflow: hidden;
    position: relative;
    width: 100%;
  }
</style>

<div
  class="virtual-wrapper"
  on:scroll={updateScroll}
  style="height: {wrapperHeight}; width: {wrapperWidth}"
  bind:this={ele}>
  <div class="inner-wrapper" style="height: {innerHeight}">
    {#each rendered as item, index}
      <VirtualRow {item} {index} />
    {/each}
  </div>
</div>
