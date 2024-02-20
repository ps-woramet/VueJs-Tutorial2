<script>
import CustomEventParent from './components/CustomEventParent.vue'
import DynamicPropParent from './components/DynamicPropParent.vue'
import NewComponent from './components/NewComponent.vue'
import PropParent from './components/PropParent.vue'
import SlotParent from './components/SlotParent.vue'
import Vmodel from './components/Vmodel.vue'

export default{
  name: "App",
  components:{
    PropParent, NewComponent, DynamicPropParent, CustomEventParent, SlotParent, Vmodel
  }
}
</script>

<template>
 <div>
  <div>App Component</div>
    <NewComponent/>
    <PropParent/>
    <DynamicPropParent/>
    <CustomEventParent/>
    <SlotParent/>
    <Vmodel/>
 </div>
</template>

<style scoped>
</style>
