<template>
  <div id="card">

    template Slot
    <br>
    <slot name="header"></slot>
    <br>
    <slot></slot>
  </div>
</template>

<script>
export default {
    name: 'SlotTemplate'
}
</script>

<style>
 #card{
    border: solid red 1px;
    padding: 1rem;
    margin: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
 }

</style>