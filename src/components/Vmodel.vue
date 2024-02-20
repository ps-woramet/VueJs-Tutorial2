<template>
  <div>this is v-model</div>
  <div>two way data binding</div>
  <br>
  <div class="form-control">
      {{JSON.stringify(employee)}}
    <div>
        <label>name</label>
        <input type="text" v-model.trim="employee.name">
    </div>
    <div>
        <label>salary</label>
         <input type="text" v-model="employee.salary">
    </div>
    <select v-model="employee.age">
        <option value="20">20</option>
        <option value="21">21</option>
        <option value="22">22</option>
    </select>
    <div>
        <input type="radio" value='male' v-model="employee.gender">
        <label>male</label>
        <input type="radio" value='female' v-model="employee.gender">
        <label>female</label>
    </div>
    <div>
        <input type="checkbox" value="thai" v-model="employee.skill">
        <label>thai</label>
        <input type="checkbox" value="english" v-model="employee.skill">
        <label>english</label>
    </div>
  </div>
</template>

<script>
export default {
    name: 'Vmodel',
    data(){
        return{
            employee:{
                name:'woramet',
                salary: 1000,
                age: '20',
                gender: '',
                skill: []
            }
        }
    }
}
</script>

<style scoped>
    .form-control{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        gap: 2rem;
    }

</style>