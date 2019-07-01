<script>
  import users from "./users";
  import VirtualWrapper from "./VirtualWrapper.svelte";

  export let name;
</script>

<div style="position: absolute; top: 0; bottom: 0; left: 0; right: 0;">
  <VirtualWrapper items={users} wrapperHeight="100%" wrapperWidth="100%" />
</div>
