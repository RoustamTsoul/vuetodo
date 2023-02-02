<template>
  <div class="header-container">
    <div class="logo">To-Do List</div>
        <form @submit.prevent="addTask" class="form">
            <input type="text" v-model="valueInput">
            <button class="btn">Add a new task</button>
        </form>
    </div>
</template>

<script>
export default {
    data(){
        return{
            valueInput:'',
        }
    },

    emits:[
        'task-add'
    ],

    methods:{
        addTask(){
            if(this.valueInput === ''){
                return
            }
            
            this.$emit('task-add',  this.valueInput )

            this.valueInput = '';
        }
    }
}
</script>

<style scoped>
.header-container{
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.header-container .logo {
    width: 100px;
    line-height: 50px;
    color: #ddd;
    font-size: 24px;
    cursor: pointer;
    
}

.header-container .form {
    width: 60%;
    display: flex;
    justify-content: space-between;
}
  
.header-container .form input {
    width: calc(100% - 145px);
    height: 40px;
    text-indent: 10px;
    border: 1px solid #fff;
    border-radius: 5px;
    border-radius: 0;
    box-sizing: border-box;
    outline: none;
    transition: 0.2s border;
}
  
.header-container .form input:focus {
    border: 1px solid #12c0dd;
}
  
.btn {
    background-color: #12c0dd;
    border: 1px solid #12c0dd;
    color: #fff;
    font-weight: 700;
    text-transform: uppercase;
    padding: 10px 15px;
    font-size: 12px;
    height: 40px;
    outline: none;
    transition: 0.2s;
}
  
.btn:hover {
    background-color: #0dd6f8;
    border-color: #0dd6f8;
}
</style>