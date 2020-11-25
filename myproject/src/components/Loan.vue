<template>
  <!--Apply Loan Page-->
  <div class="container">
    <form>
      <div class="well">
        <h4>Apply Loan</h4>
        <div class="logout">
          <router-link to="/">
            <button type="button" class="btn1 btn-md btn-danger">logout</button>
          </router-link>
        </div>
        <div class="form-group">
          <label class="pull-left"> Username </label>
          <input type="text" class="form-control" placeholder="Username" v-model="username" readonly="readonly" required minlength="6" />
        </div>
        <div class="form-group">
          <label class="pull-left"> Loan Type</label>
          <input type="text" class="form-control" placeholder="Loan Type " v-model="Loan.loan_type" required minlength="3" />
        </div>
        <div class="form-group">
          <label class="pull-left"> Loan Amount </label>
          <input type="number" class="form-control" placeholder="Loan amount" v-model="Loan.loan_Amount" required min="1000" minlength="4" />
          <div class="form-group">
            <label class="pull-left"> Date </label>
            <input type="date" class="form-control" placeholder="Date  " v-model="Loan.date" required />
          </div>
          <div class="form-group">
            <label class="pull-left"> Rate Of Interest</label>
            <input type="number" class="form-control" placeholder="Rate Of Interest" v-model="Loan.rate_of_interest" required minlength="1" />
          </div>
          <div class="form-group">
            <label class="pull-left"> Duration of loan</label>
            <input type="number" class="form-control" placeholder="Duration Of Loan" v-model="Loan.duration_of_loan" required minlength="1" />
          </div>
        </div>

        <button type="submit" class="btn btn-md btn-primary" @click="addToAPI">Submit</button>
        <router-link
          :to="{
            name: 'ViewLoans',
            params: { username: this.username },
          }"
          ><button class="btn1 btn-md btn-danger">Cancel</button></router-link
        >
      </div>
    </form>
  </div>
</template>

<script>
/*eslint-disable*/
import axios from "axios";
import router from "../router";
export default {
  name: "Loan",
  data() {
    return {
      // initialising variables
      username: this.$route.params.username,
      Loan: {
        username: this.username,
        loan_type: "",
        loan_Amount: "",
        date: "",
        rate_of_interest: "",
        duration_of_loan: "",
      },
    };
  },
  methods: {
    addToAPI() {
      // assigning the update values to new loan variable
      let newLoan = {
        username: this.username,
        loan_type: this.Loan.loan_type,
        loan_Amount: this.Loan.loan_Amount,
        date: this.Loan.date,
        rate_of_interest: this.Loan.rate_of_interest,
        duration_of_loan: this.Loan.duration_of_loan,
      };
      console.log(newLoan);
      axios
        // applying loan
        .post("http://127.0.0.1:5000/accounts/login/" + this.username + "/loans", newLoan)
        .then((response) => {
          console.log(response);
          router.push({
            name: "ViewLoans",
            params: { username: this.username },
          });
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
};
</script>
<style scoped>
h4 {
  color: green;
}
.logout {
  margin-left: 94%;
}
</style>
