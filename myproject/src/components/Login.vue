<template>
  <!--Login Page Template-->
  <div class="container">
    <form>
      <div class="well">
        <h4>Login Page</h4>
        <div class="form-group">
          <label class="pull-left"> Username </label>
          <input type="text" class="form-control" placeholder="Username" v-model="User.username" required />
        </div>
        <div class="form-group">
          <label class="pull-left"> Password </label>
          <input type="password" class="form-control" placeholder="Password " v-model="User.password" required />
        </div>
      </div>
      <div class="btn-group">
        <button type="submit" class="btn btn-md btn-success" @click="handleSubmit()">Signin</button>
        <br />
        <router-link to="/accounts/signup">
          <button type="submit" class="btn btn-md btn-primary">Signup</button>
        </router-link>
      </div>
      <p class="message">{{ message }}</p>
    </form>
  </div>
</template>

<script>
/*eslint-disable */
import axios from "axios";
import router from "../router";
export default {
  name: "Login",

  data() {
    return {
      // initialising variables as null
      User: {
        username: "",
        password: "",
      },
      submitted: false,
      message: "",
    };
  },
  methods: {
    handleSubmit() {
      this.submitted = true;
      // assign values to new user
      let newUser = {
        username: this.User.username,
        password: this.User.password,
      };
      console.log(newUser);
      axios
        // posting user details into database
        .post("http://127.0.0.1:5000/accounts/login", newUser)
        .then((response) => {
          // comparing values with database vzalues
          if (response.username === this.username && response.password === this.password) {
            this.message = response;

            console.log(response);
            router.push({
              name: "accountdetails",
              // send username to account details page using params
              params: { username: newUser.username },
            });
          } else {
            this.message = "Invalid Credentials";
          }
        })
        // if user does not exist in database throws error
        .catch((error) => {
          console.log(error.response);
          this.message = "Invalid Credentials";
        });
    },
  },
};
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
.message {
  color: red;
}
</style>
