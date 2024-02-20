<template>
  <div>
    this is Dynamic Children Prop
    <ul>
        <li>
            <div v-for="(item, index) in propGroupName" :key="index">
                -id {{index}} / name {{item.name}} / salary {{item.salary}}
            </div>
        </li>
    </ul>
  </div>
</template>

<script>
export default {
    name: 'DynamicPropChildren',
    props: ["propGroupName"]
}
</script>

<style>

</style>