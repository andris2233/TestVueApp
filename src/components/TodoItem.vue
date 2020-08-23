<template>
    <li v-on:click="todo.completed=!todo.completed" v-bind:class="{deleted:deleted}">
        <div>
            <strong>{{index + 1}}</strong>
            <span v-bind:class="{done:todo.completed}" >{{todo.title}}</span>
        </div>

        <div class="icons-group">
            <i class="material-icons icon" v-bind:class="{'completed-icon':todo.completed}">
                done
            </i>
            <button class="material-icons" v-on:click="removeTodo(todo.id)">
                delete
            </button>
        </div>
        
    </li>
</template>

<script>
export default {
    props:{
        todo:{
            type: Object,
            required: true
        },
        index: {
            type: Number,
            required: true
        }
    },
    data() {
        return {
            deleted: false
        }
    },
    methods: {
        removeTodo(id) {
            this.deleted = true;
            setTimeout(() => {
                this.$emit('remove-todo', id);
            }, 200);
        }
    }
}
</script>

<style scoped>
li{
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 5px 0;
    border-bottom: 1px solid #dadada;
    box-sizing: border-box;
    transition: 0.2s;
}

.done{
    text-decoration: line-through;
}

.deleted{
    transform: translateX(-100%);
    opacity: 0;
}

.icon{
    color: gray;
    border: 2px solid gray;
    width: 30px;
    height: 30px;
    border-radius: 3px;
    font-size: 21px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: .1s;
    margin-right: 5px;
    box-sizing: border-box;
    opacity: 0.5;
}

.completed-icon{
    opacity: 1;
    color: white;
    background: green;
    border: 2px solid green;
}

.icons-group{
    display: flex;
}

button{
    border: 2px solid #9F001D;
    color: white;
    transition: all .2s ease;
    background: #B50021;
    font-size: 21px;
    border-radius: 3px;
    width: 30px;
    height: 30px;
    display: flex;
    align-items: center;
    justify-content: center;
    outline: none;
}

button:hover{
    /* transform: scale(1.05); */
    color: #B50021;
    background: white;
}

button:active{
    transform: scale(0.9);
}

span{
    margin-left: 5px;
    font-weight: bold;
}
</style>