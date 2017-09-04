<template>
  <div class="user">
      <h1>Users</h1>
      <form v-on:submit="addUser">
          <input type="text" v-model="newUser.name" placeholder="Name">
          <br/>
          <input type="text" v-model="newUser.email" placeholder="Email">
          <br/>
          <input type="submit" value="submit">
      </form>
      <ul>
        <li v-for="user in users">
          <input type="checkbox" class="toggle" v-model="user.contacted">
          <span :class="{contacted: user.contacted}">
            {{user.name}} : {{user.email}} <button v-on:click="deleteUser(user)">Delete</button>
          </span>
        </li>
      </ul>
      <hr/>
      <h4>Users from placeholder</h4>
      <ul>
        <li v-for="userPlaceholder in usersPlaceholder">
            {{userPlaceholder.name}} : {{userPlaceholder.email}} <button v-on:click="deleteUserPlaceholder(userPlaceholder)">Delete</button>
        </li>
      </ul>
  </div>
</template>
<script>
  export default {
    name: 'users',
    data(){
      return {
        newUser: {},
        users: [
          {
            name: 'John Doe',
            email: 'john@gmail.com',
            contacted: false
          },
          {
            name: 'Jack Daniel',
            email: 'jack@gmail.com',
            contacted: false
          },
          {
            name: 'Mary Ann',
            email: 'mary@gmail.com',
            contacted: false
          },
        ],
        usersPlaceholder: []
      }
    },
    methods: {
      addUser: function(e){
        this.users.push({
          name: this.newUser.name,
          email: this.newUser.email,
          contacted: false
        });
        e.preventDefault();
      },
      deleteUser: function(user){
        this.users.splice(this.users.indexOf(user),1);
      },
      deleteUserPlaceholder: function(user){
        this.usersPlaceholder.splice(this.usersPlaceholder.indexOf(user),1);
      },
    },
    created: function(){
      this.$http.get('https://jsonplaceholder.typicode.com/users')
        .then(function(response){
            this.usersPlaceholder = response.data;
        })
    }
  }
</script>
<style scoped>
  .contacted {
    text-decoration: line-through;
  }
</style>
