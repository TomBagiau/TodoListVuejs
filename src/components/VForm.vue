<template>
    <div class="form form-container absolute w-screen h-screen">
        <div class="form-container_overlay absolute w-screen h-screen bg-gray-800 bg-opacity-40"></div>
        <form @submit.prevent="onSubmit" class="relative flex flex-col justify-center items-center	mx-auto h-screen">
          <input
            class="todo_input todo_input-title my-2 w-full h-14 p-4"
            name="title"
            type="text"
            placeholder="Titre"
            v-model="form.title"
            required
          />

          <input
            class="todo_input todo_input-place my-2 w-full h-14 p-4"
            name="place"
            type="text"
            placeholder="Lieu"
            v-model="form.place"
          />

          <input
            class="todo_input todo_input-time my-2 w-full h-14 p-4"
            name="time"
            type="date"
            placeholder="Heure"
            v-model="form.time"
          />

          <textarea
            class="todo_input todo_input-description my-2 w-full h-14 p-4"
            name="description"
            type="text"
            placeholder="Description"
            v-model="form.description"
          ></textarea>

          <button type="submit" class="bg-blue-600">Valider</button>
        </form>
    </div>
</template>


<script>
export default {
    props: ['tasks'], //infos du parents à l'enfant
    data(){
        return {
            id: 0,
            form: {
                title: null,
                place: null,
                time: null,
                description: null,
                priority: null
            }
        }
    }, 


    mounted(){
        console.log(this.tasks);
    },

    methods: {
        onSubmit(event){
            console.log(this.form);
            const task = {
                ...this.form,
                id: this.id
            }

            this.tasks.push(task)

            this.$emit('submit')
            //reset form
            Object.keys(this.form).forEach(key => {
                this.form[key] = null
            })

            this.id++
        }
    }
}
</script>

<style scoped>
    form input,
    form textarea{
        width: 50%;
        border: none;
        border-bottom: 2px solid #3265e3;
        background: transparent;
        color: #fff;
        font-size: 22px;
    }

    form input::placeholder,
    form textarea::placeholder{
        color: #fff;
    }

    form input:focus,
    form textarea:focus{
        outline:none;
    }

    button{
        color: #fff;
        font-size: 20px;
        padding: 15px;
        border-radius: 20px;
        width: 15%;
    }
</style>