<template>
    <div class="task cursor-pointer container mx-auto my-6 rounded px-6 py-4 flex justify-between items-center bg-blue-200" :class="{'task--completed': completed}" @click="onClick">
        <div class="task__check w-8 h-8 rounded bg-blue-600 mr-10 relative">
            <div class="checked absolute w-6 h-6 rounded bg-red-600  opacity-50 top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2" v-show="task.completed"></div>
        </div>

        <div class="task_content mr-auto">
             <h2 class="task_title font-black text-lg uppercase">{{ task.title }}</h2>
            <p class="task_place-time">{{ task.place }} - {{ task.time }}</p>
            <p class="task_description">{{ task.description }}</p>
        </div>

        <button class="task_delete" @click.stop="onDelete()"><i class="fas fa-trash-alt"></i></button>
    </div>
</template>


<script>
export default {
    props: ["task", "tasks"],

    data(){
        return {
            completed: false
        }
    },

    computed: {
    classes() {
      const c = {}
      c[`task--${this.currentClass}`] = true
      c[`opacity-60`] = this.task.completed
      return c
    }
  },

    methods: {
        onClick(){
            console.log('click');
            this.completed = !this.completed
        },

        onDelete(){
            this.$emit('delete', this.task.id)
        }
    },

    mounted(){

    }
}
</script>


<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300&display=swap');
    .task{
        border-radius: 10px;
        width: 30%;
        margin-left: 35%;
        font-family: 'Roboto', sans-serif;
        cursor: pointer;
        display: flex;
        margin-bottom: 30px;
    }
    .task:first-child{
        margin-top: 12%;
    }
    .task_content{
        display: flex;
        flex-direction: column;
    }
    h2{
        margin-left: 20px;
        margin-bottom: 0px;
        font-weight: 600;
        padding-top: 10px;
    }
    .task_place-time{
        margin-left: 20px;
        margin-top: 0px;
        margin-bottom: 15px;
        font-size: 10px;
        font-weight: 600;
        color: grey;
        width: 90%;
    }
    .task_description{
        margin-left: 20px;
        padding-bottom: 10px;
    }

    .task--completed{
        opacity: 0.5;
    }

    .task--completed .task_title{
        text-decoration: line-through;
    }

    .task_delete{
        display: flex;
        border: none;
        background-color: transparent;
        font-size: 20px;
        cursor: pointer;
        margin-top: 10px;
    }

    .task_content{
        width: 80%;
    }
</style>