<template>
    <div id="to-do-list">
        <h4>To Do List</h4>

        <div class="item" v-for="(item, index) in items">
            <div>
                {{item.label}}
                <span class="handle">
                    <span class="time" v-text="timeFormat(item.time)"></span>
                    <i class="el-icon-success" title="finish" @click="finish(index)"></i>
                    <i class="el-icon-delete" title="delete" @click="deleteItem(index)"></i>
                </span>
            </div>
            <div class="clearfix"></div>
        </div>

    </div>
</template>

<script scoped>
export default {
    name: 'ToDoList',
    methods: {
        deleteItem: function (index) {
           this.$emit('deleteItem', index)
        },
        finish: function (index) {
            this.$emit('finish', index)
        },
        timeFormat: function (time) {
            return time.getFullYear() + '-' + (time.getMonth() + 1) + '-' +
                    (time.getDate() + 1) + ' ' + (time.getHours() + 1) + ':' +
                    (time.getMinutes() + 1) + ':' + (time.getSeconds() + 1)
        }
    },
    props: ['items']
}
</script>

<style scoped>
    #to-do-list {
        min-height: 300px;
        margin-top: 20px;
    }

    .item {
        border-left: 5px solid #0ecbff;
    }
    
    .el-icon-success:hover {
        color: #0cff00;
    }

    .el-icon-delete:hover {
        color: #000;
    }
</style>