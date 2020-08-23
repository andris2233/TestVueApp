<template>
    <form class="row" @submit.prevent="onSubmit">
        <input type="text" placeholder="Введите название дела" v-model="title">
        <button type="submit"><i class="material-icons">add</i></button>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods:{
        onSubmit(){
            if(this.title.trim()){
                const newTodo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }

                this.$emit('create-todo', newTodo);
                this.title = '';
            }
        }
    }
}
</script>

<style scoped>
.row{
    display: flex;
    align-items: stretch;
    margin: 0;
    padding: 0;
}

input{
    margin-right: 5px;
    border: 2px solid white;
    border-radius: 6px;
    background: #3BA8C6;
    box-shadow: inset 0 0 5px #1B6B81;
    padding: 5px;
    width: 220px;
    transition: all .3s ease;
    outline: none;
}

input:focus{
    background: white;
    box-shadow: inset 0 0 5px 1px #dadada;
}

button{
    border: 0;
    border-radius: 50%;
    background: white;
    color:#1B6B81;
    outline: none;
    font-weight: bold;
    transition: all .2s ease;
    width: 28px;
    height: 28px;
    display: flex;
    align-items: center;
    justify-content: center;
}

button:hover{
    box-shadow: 0 0 8px #1B6B81;
}

button:active{
    transform: scale(0.9);
    box-shadow: 0 0 3px #1B6B81;
}
</style>