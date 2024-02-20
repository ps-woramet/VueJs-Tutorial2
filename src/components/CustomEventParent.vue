<template>
    <div id="customEvent">
        this is Custom Event Parent
        <CustomEventChildren :propGroupFruit="groupFruit" @newShowFromChildren="toggleShowFunction" @deleteFromChildren="deleteFunction" />
    </div>
</template>

<script>
import CustomEventChildren from './CustomEventChildren.vue'

export default {
    name: "CustomEventParent",
    components:{
      CustomEventChildren
    },
    data(){
        return{
            groupFruit: [
                {id: 1, name: 'this is fruit1', price: '100',show:false},
                {id: 2, name: 'this is fruit2', price: '200',show:false},
                {id: 3, name: 'this is fruit3', price: '300',show:false},
                {id: 4, name: 'this is fruit4', price: '400',show:false},
            ]
        }
    },
    methods:{
      toggleShowFunction(idFromChildren){
        this.groupFruit = this.groupFruit.map((element) => {
          if(element.id === idFromChildren){
            return {...element, show:!element.show}
          }
          return element
        })
      },
      deleteFunction(idFromChildren){
        this.groupFruit = this.groupFruit.filter((element) => {
          return element.id !== idFromChildren
        })
        console.log('delete function parent');
      }
    }
}
</script>

<style scoped>
    #customEvent{
        border: 1px solid #000;;
    }
</style>