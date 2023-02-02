<template>
<div class="ToDo-container">
    <h2>
    <span>To Do</span>
    <span class="task-num">{{ needDoList.length}}</span>
    </h2>
    <ul class="task-list">
        <li v-for="(task, index) in needDoList" :key="task">
            <div>
                <input type="checkbox" v-on:change="moveTaskToDone(index)">
                <span>{{task}}</span>
            </div>
            <button class="btn-remove" v-on:click="removeTaskFromNeedDoList(index)">Remove</button>
        </li>
    </ul>
    <h2>
    <span>Done</span>
    <span class="task-num">{{ completeList.length }}</span>
    </h2>
    <ul class="task-list complete-list">
        <li v-for="(task, index) in completeList" :key="task"> 
            <div>
                <input type="checkbox" v-on:change="moveTaskBack"    checked>
                <span>{{task}}</span>
            </div>
            <button class="btn-remove" v-on:click="removeTaskFromCompleteList(index)">Remove</button>
            
        </li>
    </ul>
</div>
</template>

<script>

// пропсы(список задач)
export default {
    props:{
        needDoList:{
            type:Array,
            required:true 
            },    
    },
    

    data(){
        return{
            completeList:[],
        }
    },

    emits:[
        'remove-task',
        'add-task'
    ],

    methods:{

        moveTaskToDone(index){
            const task = this.needDoList[index];
            this.removeTaskFromNeedDoList(index);
            this.completeList.push(task);
        },

        moveTaskBack(index){
            const task = this.completeList[index];
            this.removeTaskFromCompleteList(index);
            this.$emit('add-task', task);
        },

        removeTaskFromNeedDoList(index){
            this.$emit('remove-task', index )

        },

        removeTaskFromCompleteList(index){
         this.completeList.splice(index, 1)  //TODO: make sure that is reactive
        }
    }
}
</script>

<style scoped>
h2{
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding-bottom: 20px;
    margin: 25px 0;
    border-bottom: 1px solid #bfbfbf;
}

h2 .mask-num{
    border-radius: 20px;
    border: 2px solid #2a2f36;
    color: #2a2f36;
    font-size: 14px;
    font-weight: 700;
    padding: 5px 10px;
}

.task-list li {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 32px;
    line-height: 32px;
    margin-bottom: 10px;
    border-radius: 3px;
    background-color: #fff;
}
  
.task-list.complete-list li {
    border-left-color: #999;
    opacity: .5;
}
.task-list {
    padding-left: 0;
}
  
input[type="checkbox"] + span {
    padding-left: 10px;
}
  
.btn-remove {
    border: 1px solid #2a2f36;
    font-size: 12px;
    border: 2px solid #2a2f36;
    background-color: #333333;
    color: #fff;
    font-weight: 700;
    text-transform: uppercase;
    padding: 5px 10px;
    font-size: 12px;
    outline: none;
    transition: 0.2s;
}
  
.btn-remove:hover {
    background-color: #535151;
    border-color: #535151;
}
  
input[type="checkbox"]:checked,
input[type="checkbox"]:not(:checked){
    position: absolute;
    z-index: 1;
    opacity: 0;
    width: 20px;
    height: 20px;
    margin-top: 6px;
}
input[type="checkbox"]:checked + span,
input[type="checkbox"]:not(:checked) + span{
    position: relative;
    padding-left: 35px;
    cursor:pointer;
}
input[type="checkbox"]:checked + span::before{
    content:'';
    position: absolute;
    width: 16px;
    height: 16px;
    left:0;
    top:calc(50% - 10px);
    background-color: transparent;
    border-radius: 2px;
    border: 2px solid #4fc1de;
}
input[type="checkbox"]:checked + span::after{
     content:'';
     position: absolute;
     width: 12px;
     height: 12px;
     transition: all .2s ease;
     opacity: 1;
     left: 4px;
     top: calc(50% - 6px);
     background-color: #4fc1de;
}
input[type="checkbox"]:not(:checked) + span::before{
    content:'';
    position: absolute;
    width: 16px;
    height: 16px;
    left:0;
    top:calc(50% - 10px);
    background-color: transparent;
    border-radius: 2px;
    border: 2px solid #5d575f;
}
input[type="checkbox"]:not(:checked) + span::after{
    content:'';
    position: absolute;
    width: 12px;
    height: 12px;
    transition: all .2s ease;
    opacity: 0;
    left: 4px;
    top: calc(50% - 6px);
    background-color: #7d25a9;
}
</style>