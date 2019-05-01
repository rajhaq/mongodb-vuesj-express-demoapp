<template>
  <div class="container">
    <div class="row">
		<div class="col-8">
			<ul class="list-group">
				<li class="list-group-item" v-for="item in Users">{{item.first_name}} {{item.last_name}} ({{item.email}})</li>
			</ul>
		</div>
		<div class="col-4">
			      <div class="well">
        <h4> Add User</h4>
        <div class="form-group">
          <label class="pull-left"> First Name </label>
          <input type="text" class="form-control" placeholder="First Name" v-model="User.first_name">
        </div>
        <div class="form-group">
          <label class="pull-left"> Last Name </label>
          <input type="text" class="form-control" placeholder="Last Namen" v-model="User.last_name">
        </div>
        <div class="form-group">
          <label class="pull-left"> Email </label>
          <input type="text" class="form-control" placeholder="Email " v-model="User.email">
        </div>
      </div>
  
      <button type="submit" class="btn btn-large btn-block btn-primary full-width" @click="addToAPI">Submit</button>

		</div>

  

	  </div>
  
  </div>
</template>

<script>
/* eslint-disable */
import axios from 'axios';
export default {
  name: 'hello',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      User: { first_name: '', last_name: '', email: '' },
      Users:[],
    }
  }, 
  methods: {
	   setupData()
	  {
		      axios.get('http://localhost:3000/users')
            .then((response) => {
                console.log(response.data);
                this.Users = response.data;
            })
            .catch((error) => {
                console.log(error);
            });

	  },
		async addToAPI() {
		let newUser = {
			first_name: this.User.first_name,
			last_name: this.User.last_name,
			email: this.User.email
		}
		console.log(newUser);
		axios.post('http://localhost:3000/users', newUser)
			.then((response) => {
			console.log(response);
			this.Users.push(response.data);
			})
			.catch((error) => {
			console.log(error);
			});
		},

	  },
	created(){
		axios.get('http://localhost:3000/users')
            .then((response) => {
                console.log(response.data);
                this.Users = response.data;
            })
            .catch((error) => {
                console.log(error);
            });


  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>