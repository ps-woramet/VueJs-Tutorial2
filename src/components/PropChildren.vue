<template>
<div>
    {{message}}
    {{propName}}
    {{propSalary}}
</div>
</template>

<script>
export default {
    name: 'PropChildren',
    data(){
        return{
            message: 'ข้อมูล พนักงาน'
        }
    },
    props:["propName", "propSalary"],
    props:{
        propName:{
            type: String,
            required: true
        },
        propSalary:{
            type:Number,
            default: 1000
        }
    }
}
</script>

<style scoped>
    div{
        color: red;
    }
</style>