<template>
    <div class="TodoApp max-w-screen-xl">
        <button @click="toggleForm" class="fixed bottom-4 right-4 w-20 h-20 rounded-full bg-blue-600 text-white text-xl z-10 plusmois">{{ labelBtn }}</button>

    <transition name="fade">
      <VForm v-show="showForm" :tasks="tasks" @submit="toggleForm(null, false)"></VForm>
    </transition>

    <div class="tasks overflow-auto">
      <transition-group name="list" tag="div">
        <VTask v-for="task in tasks" :key="task.id" :task="task" @delete="onDelete"></VTask>
      </transition-group>
    </div>
    </div>
    
</template>



<script>
import VForm from './components/VForm.vue'
import VTask from './components/VTask.vue'
export default{
    data(){
        return {
            tasks: [],
            showForm: false,
        }
    },

    components: {
        VForm,
        VTask
    },

    computed: {
        labelBtn() {
            return this.showForm ? '-' : '+'
        }
    },

    mounted() {
    const tasks = localStorage.getItem('todo')
    if (tasks) {
      this.tasks = JSON.parse(tasks)
    }
  },

  watch: {
    tasks: {
      handler: (val, oldVal) => {
        localStorage.setItem('todo', JSON.stringify(val))
      },
      deep: true
    }
  },

    methods: {
        onDelete(index){
            const id = this.tasks.findIndex((task) => task.id === index)
            this.tasks.splice(id, 1)
        },

        toggleForm(event, value){
            if(value !== undefined){
                this.showForm.value
            } else {
                this.showForm = !this.showForm
            }
        }
    },
}
</script>




<style scoped>

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to{
  opacity: 0;
}
.list-enter-active {
  transition: all 1s;
}
.list-leave-active {
  transition: all 1s;
}
.list-enter{
  opacity: 0;
  transform: translateY(30px);
}
.list-leave-to{
  opacity: 0;
  transform: translateY(-30px);
}
.plusmois{
  font-size: 60px;
}

</style>