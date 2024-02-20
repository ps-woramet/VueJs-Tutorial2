<template>
  <div>
    {{message}}
    <PropChildren propName="this is prop1" :propSalary='salary1' />
    <PropChildren propName="this is prop2" :propSalary='salary2' />
    <PropChildren propName="this is prop3" :propSalary='salary3' />

  </div>
  
</template>

<script>
import PropChildren from './PropChildren.vue'

export default {
    name: 'PropParent',
    data(){
        return{
            message: 'this is list data component',
            salary1: 100,
            salary2: 120,
            salary3: 130,
        }
    },
    components:{
        PropChildren
    }
}
</script>