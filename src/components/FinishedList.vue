<template>
    <div id="finished-list">
        <h4>Finished List</h4>

        <div class="item" v-for="(item, index) in items">
            <div>
                {{item.label}}
                <span class="handle">
                    <span class="time" v-text="timeFormat(item.time)"></span>
                    <i class="el-icon-error" title="not finish" @click="notFinish(index)"></i>
                    <i class="el-icon-delete" title="delete" @click="deleteItem(index)"></i>
                </span>
            </div>
            <div class="clearfix"></div>
        </div>

    </div>
</template>

<script>
export default {
    name: 'FinishedList',
    data() {
        return {
        }
    },
    methods: {
        deleteItem: function (index) {
           this.$emit('deleteItem', index)
        },
        notFinish: function (index) {
            this.$emit('notFinish', index)
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
    #finished-list {
        min-height: 300px;
        margin-top: 20px;
    }

    .item {
        border-left: 5px solid #ccc;
        text-decoration: line-through;
    }

    .el-icon-error:hover {
        color: red;
    }

    .el-icon-delete:hover {
        color: #000;
    }
</style>