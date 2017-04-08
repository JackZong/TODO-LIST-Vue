<template>
  <div id="app">
    <h1 v-text="title" v-bind:class="{title: true}"></h1>
    <input type="text" v-model="newItem" v-on:keyup.enter="addNew()" v-bind="{placeholder,autofocus}">
    <ul>
      <li v-for="item in items" v-bind:class="{finished: item.isFinished}"v-on:click="doSometing(item)" v-if="">
        {{item.label}}
        <span v-bind:class="{floatR: true}" v-on:click="delItem">&times;</span>
      </li>
    </ul>
  </div>
</template>

<script>
import Store from './store'
export default {
  name: 'app',
  data: function(){
    return {
      title: 'enter the code',
      items: Store.fetch(),
      newItem: '',
      placeholder: 'enter the code',
      autofocus: 'autofocus'
    }
  },
  watch: {
     items: {
      handler: function (items){
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    doSometing: function(item){
      item.isFinished = !item.isFinished;
    },
    addNew: function(){
      this.items.push({
        label: this.newItem,
        isFinished: false
      })
      this.newItem = '';
    },
    delItem: function(){
     console.log("123");
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background: #f8f8f8;
}
.title {
  font-size: 50px;
  color: rgba(175, 47, 47, 0.15)
}
input {
  width: 500px;
  height: 60px;
  border: none;
 /*  box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03) */
}
.finished {
  text-decoration: line-through;
}
ul {
  padding: 0;
}
ul >li {
  list-style: none;
  border-bottom: dashed 1px grey;
  width: 300px;
  height: 60px;
  margin: auto;
  line-height: 60px;
  font-size: 26px;
}
ul>li>span {
  font-size: 40px;
}
.floatR {
  float: right;
}
</style>
