<template>
    <div v-if="this.todolists.length" class="main">
        <ul>
            <li v-for="todo in newTodolists" :key="todo.id">
                <div class="check-box"><input :id="`${todo.id}in`" type="checkbox" v-model="todo.isComplete">
                    <label :for="`${todo.id}in`" :style="`text-decoration:${todo.isComplete?'line-through':'none'}`">{{todo.todoText}}</label>
                </div>
                <button class="delete-btn" @click="handleDel(todo.id)"></button>
            </li>
        </ul>

        <footer>
            <span class="num">{{leaveEvent}} items left</span>
            <div class="toShow">
                <span @click="handleChange('all')"  :class="{selected:type==='all'}">All</span>
                <span @click="handleChange('active')" :class="{selected:type==='active'}" >Active</span>
                <span @click="handleChange('completed')" :class="{selected:type==='completed'}">Completed</span>
            </div>
            <!-- <span>{{newTodolists}}</span> -->
            <button class="clear" @click="handleDelAll" :style="`display:${completedEvent?'block':'none'}`">ClearCompleted</button>
        </footer>

    </div>

</template>
<script>
export default {
    name: "eventLists",
    props: ["todolists", "handleDelete", "handleDelAll", "type", "changeType"],
    methods: {
        handleDel(id) {
            this.handleDelete(id);
        },
        handleChange(str) {
            this.changeType(str);
        }
    },
    computed: {
        completedEvent() {
            return this.todolists.filter(t => t.isComplete === true).length;
        },
        leaveEvent() {
            return this.todolists.filter(t => t.isComplete === false).length;
        },
        newTodolists() {
            return this.type === "active"
                ? this.todolists.filter(t => t.isComplete === false)
                : this.type === "completed"
                    ? this.todolists.filter(t => t.isComplete === true)
                    : this.type === "all" ? this.todolists : this.todolists;
        }
    }
};
</script>
<style scoped>
.main {
    width: 100%;
    margin: 0 auto;
}
ul {
    margin: 0;
    padding: 0;
}
li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px 15px 15px 60px;
    border-bottom: 1px solid #ccc;
    position: relative;
    font-size: 24px;
}
li .check-box input[type="checkbox"] {
    position: absolute;
    top: 0;
    left: 0;
    z-index: -1;
    opacity: 0;
}
li .check-box label::before {
    content: "";
    display: block;
    width: 30px;
    height: 30px;
    border: 2px solid #ccc;
    background-color: #fff;
    border-radius: 50%;
    position: absolute;
    top: 18px;
    left: 10px;
}
li .check-box label {
    margin-left: 10px;
}
li .check-box input:checked ~ label::before {
    background-image: url("http://pcgnine5c.bkt.clouddn.com/%E5%AF%B9%E9%92%A9.png");
    background-repeat: no-repeat;
    background-size: contain;
}
.delete-btn {
    width: 30px;
    height: 30px;
    background-image: url("http://pcgnine5c.bkt.clouddn.com/x.png");
    background-repeat: no-repeat;
    background-size: contain;
    border: 0;
    outline: 0;
    background-color: #fff;
}
footer {
    width: 100%;
    height: 30px;
    display: flex;
    align-items: center;
    padding: 10px 10px 0 10px;
}
span {
    margin-right: 20px;
    border: 1px solid #fff;
    border-radius: 3px;
    padding: 5px;
}
.num {
    margin-right: 30px;
}
.clear {
    margin-left: 20px;
    outline: 0;
    border: 0;
    width: 120px;
    line-height: 30px;
    border-radius: 5px;
    background-color: #1992ff;
    color: #fff;
}
.selected {
    border-color: rgba(175, 47, 47, 0.2);
}
</style>

