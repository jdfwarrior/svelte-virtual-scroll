<script>
  export let item;
  export let index;
</script>

<style>
  .virtual-row {
    position: absolute;
    height: 25px;
    vertical-align: middle;
    display: grid;
    grid-template-columns: 100px 200px 200px 200px 300px;
    text-align: left;
    width: 100%;
  }
  .virtual-row.odd {
    background: #f8f8f8;
  }
</style>

<div
  class="virtual-row"
  style="top: {(item.id - 1) * 25}px;"
  class:odd={item.id % 2 !== 0}>
  <div>{item.id}</div>
  <div>{item.first_name}</div>
  <div>{item.last_name}</div>
  <div>{item.ip_address}</div>
  <div>{item.email}</div>
</div>
