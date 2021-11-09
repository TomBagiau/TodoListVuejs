<template>
    <div class="form">
        <div class="form-container_overlay absolute w-screen h-screen bg-gray-400 bg-opacity-40"></div>
        <form @submit.prevent="onSubmit" class="relative">
          <input
            class="todo__input todo__input--title"
            name="title"
            type="text"
            placeholder="Titre"
            v-model="form.title"
            required
          />

          <input
            class="todo__input todo__input--place"
            name="place"
            type="text"
            placeholder="Lieu"
            v-model="form.place"
          />

          <input
            class="todo__input todo__input--time"
            name="time"
            type="date"
            placeholder="Heure"
            v-model="form.time"
          />

          <textarea
            class="todo__input todo__input--description"
            name="description"
            type="text"
            placeholder="Description"
            v-model="form.description"
          ></textarea>

          <button type="submit">Valider</button>
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

            this.id++
        }
    }
}
</script>

<style scoped>
    form{
        display: flex;
         flex-direction: column;
         width: 40%;
    }

    form input,
    form textarea{
        height: 4vh;
        margin-bottom: 40px;
        border: none;
        border-bottom: 1px solid #333;
        padding-left: 15px;
        font-size: 16px;
    }
    form input:focus,
    form textarea:focus{
        outline: none;
    }
    button{
        width: 50%;
        height: 30px;
        border: none;
        border-radius: 20px;
        color: #fff;
        background-color: #000;
        cursor: pointer;
    }
</style>