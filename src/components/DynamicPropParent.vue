<template>
    <div id="dynamicprops">
        this is Dynamic Prop Parent
        <DynamicPropChildren :propGroupName="groupName" />
    </div>
</template>

<script>
import DynamicPropChildren from './DynamicPropChildren.vue'

export default {
    name: "DynamicPropParent",
    components:{
        DynamicPropChildren
    },
    data(){
        return{
            groupName: [
                {name: 'this is value1', salary: '100'},
                {name: 'this is value2', salary: '200'},
                {name: 'this is value3', salary: '300'},
                {name: 'this is value4', salary: '400'},
            ]
        }
    }
}
</script>

<style scoped>
    #dynamicprops{
        border: 1px solid #000;;
    }
</style>