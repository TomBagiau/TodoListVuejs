<template>
    <div class="task" :class="{'task--completed': completed}" @click="onClick">
        <div class="task_content">
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
        border: 1px solid #333;
        border-radius: 10px;
        width: 30%;
        margin-left: 35%;
        font-family: 'Roboto', sans-serif;
        cursor: pointer;
        display: flex;
        margin-bottom: 30px;
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