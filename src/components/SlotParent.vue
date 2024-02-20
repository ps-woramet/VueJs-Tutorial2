<template>
    <div>this is slot parent</div>
    <SlotTemplate>
        <template v-slot:header>hello this country</template>
        country1 from slot parent
    </SlotTemplate>
    <SlotTemplate>
        <template v-slot:header>hi this country</template>
        country2 from slot parent
    </SlotTemplate>
    <SlotTemplate>
        <template v-slot:header>bonjour this country</template>
        country3 from slot parent
    </SlotTemplate>
</template>

<script>
import SlotTemplate from './SlotTemplate.vue'

export default {
    name: 'SlotParent',
    components:{
        SlotTemplate
    }
}
</script>

<style>

</style>