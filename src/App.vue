<template>
  <div id="app">
    <router-view/>
    <el-input v-model="input" placeholder="YOUR TASK" @keyup.enter.native="addNew()">
      <i class="el-icon-edit el-input__icon" slot="suffix" @click="addNew()"></i>
    </el-input>
    <to-do-list :items="items" @finish="finish" @deleteItem="deleteItem"></to-do-list>
    <finished-list :items="finishedItems" @notFinish="notFinish" @deleteItem="deleteFinishedItem"></finished-list>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList'
import FinishedList from './components/FinishedList'

export default {
  name: 'app',
  data() {
    return {
      input: '',
      items: [],
      finishedItems: []
    }
  },
  methods: {
    addNew: function() {
      this.items.push({
        label: this.input,
        time: new Date()
        })
      this.input = ''
      this.items = this.items.sort(function (a, b) {
        return b.time - a.time
      })
    },
    finish: function (index) {
      this.finishedItems.push(this.items[index])
      this.items = this.items.filter((item, i) => i !== index)
      this.finishedItems = finishedItems.sort(function (a, b) {
        return b.time - a.time
      })
    },
    deleteItem: function(index) {
      this.items = this.items.filter((item, i) => i !== index)
    },
    deleteFinishedItem: function(index) {
      this.finishedItems = this.finishedItems.filter((item, i) => i !== index)
    },
    notFinish: function (index) {
      this.items.push(this.finishedItems[index])
      this.finishedItems = this.finishedItems.filter((item, i) => i !== index)
      this.items = items.sort(function (a, b) {
        return b.time - a.time
      })
    }
  },
  components: {
    ToDoList,
    FinishedList
  }
}
</script>

<style>
#app {
  width: 90%;
  margin:auto;
}

.clearfix {
  clear: both;
}

hr {
  width: 200px;
  float: left;
  margin: 2px 0px;
}

i {
  padding: 5px;
}

.item {
  font-size: 20px;
  padding: 10px;
  margin-bottom: 2px;
  border-bottom: 1px solid #efefef;
}

.item:hover {
  color: #ccc;
  border-bottom: 1px solid #ccc;
}

.time {
  font-size: 10px;
  padding: 0px 20px;
}

.handle {
  
  float: right;
}
</style>
