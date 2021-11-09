<template>
    <div class="TodoApp">
        <div class="openForm" v-if="toggle == true">
            <VForm :tasks="tasks"></VForm>
        </div>
        <VTask v-for="task in tasks" :key="task.id" :task="task"  @delete="onDelete"></VTask>
        <div class="btnOpenClose" @click="openForm()"><i class="fas fa-plus"></i></div>
    </div>
    
</template>



<script>
import VForm from './components/VForm.vue'
import VTask from './components/VTask.vue'
export default{
    data(){
        return {
            tasks: [],
            toggle: false
        }
    },

    components: {
        VForm,
        VTask
    },

    methods: {
        saveData(){

        },

        onDelete(index){
            const id = this.tasks.findIndex((task) => task.id === index)
            this.tasks.splice(id, 1)
        },
        openForm(){
            this.toggle = !this.toggle
        }
    }
}
</script>




<style scoped>

    .TodoApp{
        width: 100%;
    }

   .btnOpenClose{
       position: absolute;
       cursor: pointer;
       margin-left: 90%;
   }

   .btnOpenClose i{
       color: #fff;
       background-color: #000;
       font-size: 45px;
       padding: 15px;
       border-radius: 50%;
   }

   .openForm{
       position: relative;
   }
</style>