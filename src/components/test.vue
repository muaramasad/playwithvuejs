<template>
  <div class="test">
      <input type="text" v-model="title">
      <h1>{{title}}</h1>
      <span v-html="titleHtml"></span>
      <p>{{user.first_name}}</p>
      <p v-text="user.last_name"></p>
      <p v-if="showName">{{user.first_name_if}}</p>
      <p v-else>Nobody</p>
      <ul>
        <li v-for="item in items">{{item.title}}</li>
      </ul>
      <button type="button" name="button" v-on:click="greet()">Say greetings</button>
      <button type="button" name="button" v-on:click="greetParam('hello world param')">Say greetings with param</button>
      <br/>
      <input type="text" name="" value="" v-on:keyup="pressKey" v-on:keyup.enter="enterPress">
      <hr/>
      <label>First Name: </label><input type="text" name="" value="" v-model="user.first_name"><br/>
      <label>First Name: </label><input type="text" name="" value="" v-model="user.last_name"><br/>
      <h3>{{fullName}}</h3>
      <h3>{{msg}}</h3>
    </br/>
  </div>
</template>
<script>
  export default {
    name: 'test',
    props: {
      msg: {
        type: String,
        default: 'foobar'
      }
    },
    data(){
      return {
        title: 'Hello World',
        titleHtml: '<h1>Hello World</h1>',
        user: {
          first_name_if: 'If John',
          first_name: 'John',
          last_name: 'Doe'
        },
        showName: true,
        items: [
          {title: 'Item One'},
          {title: 'Item Two'},
          {title: 'Item Three'},
          {title: 'Item Four'},
        ]
      }
    },
    methods: {
      greet: function(){
        alert('Hello');
      },
      greetParam: function(param){
          alert(param);
      },
      pressKey: function(e) {
        console.log(e.target.value);
      },
      enterPress: function() {
        console.log('enter key pressed!');
      }
    },
    computed: {
      fullName: function(){
        return this.user.first_name+' '+this.user.last_name
      }
    }
  }
</script>
<style scoped>

</style>
