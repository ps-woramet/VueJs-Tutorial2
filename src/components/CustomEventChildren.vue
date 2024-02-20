<template>
  <div>
    this is Custom Event Children
    <div v-for="(item, index) in propGroupFruit" :key="index">
        <div id="container">
            <div>{{item.name}}</div>
            <transition name="fade">
                <div v-show="item.show">-id {{item.id}} / name {{item.name}} / price {{item.price}}</div>
            </transition>
            <button @click="showDescription(item.id)">show detail</button>
            <button @click="deleteData(item.id)">Delete data</button>
        </div>
    </div>
  </div>
</template>

<script>
export default {
    name: 'CustomEventChildren',
    props: ["propGroupFruit"],
    methods:{
        showDescription(id){
            console.log(id);
            //send id to parent with emit
            this.$emit('newShowFromChildren', id);
        },
        deleteData(id){
            console.log(id);
            //send id to parent with emit
            this.$emit('deleteFromChildren', id);
        }
    }
}   
</script>

<style>
    #container{
        border: solid black 1px;
        margin: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 0.5rem;
        flex-direction: column;
        padding: 1rem;
    }
    .fade-enter-from{
        opacity: 0;
    }
    .fade-enter-active{
        transition: all 0.5s linear;
    }
</style>