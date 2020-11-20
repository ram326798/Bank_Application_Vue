<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="loans">
      <router-link
        :to="{
          name: 'accountdetails',
          params: { username: this.username },
        }"
        ><button class="btn1 btn-md btn-success">Account Details</button></router-link
      >
      <router-link
        :to="{
          name: 'Loan',
          params: { username: this.username },
        }"
        ><button class="btn1 btn-md btn-info">Apply Loan</button></router-link
      >
      <router-link to="/">
        <button type="button" class="btn1 btn-md btn-danger">logout</button>
      </router-link>
    </div>
    <div v-if="!IsLoanAvailable" style="text-align: left; margin-left: 235px">
      <h3 style="color: red; margin-left: 150px; margin-top: 45px">No active loans at this moment to show!!!</h3>
    </div>
    <table v-if="IsLoanAvailable" border="1" class="center">
      <thead>
        <tr>
          <th>S.no</th>
          <th>UserName</th>
          <th>LoanType</th>
          <th>LoanAmount (INR)</th>
          <th>Date</th>
          <th>Rate of Interest</th>
          <th>Duration Of Loan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(loan, i) in Loan" :key="i">
          <td>{{ i + 1 }}</td>
          <td>{{ loan.username }}</td>
          <td>{{ loan.loan_type }}</td>
          <td>{{ loan.loan_Amount }}</td>
          <td>{{ loan.date }}</td>
          <td>{{ loan.rate_of_interest }}%</td>
          <td>{{ loan.duration_of_loan }}year</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
/*eslint-disable*/
import axios from "axios";
import router from "../router";
export default {
  name: "ViewLoans",
  data: function () {
    return {
      msg: "Loan Details",
      username: this.$route.params.username,
      IsLoanAvailable: true,
      Loan: [],
    };
  },
  methods: {
    getLoan(username) {
      axios.get("http://127.0.0.1:5000/accounts/login/" + this.username + "/loans").then(
        (res) => {
          if (res.data.length) {
            this.Loan = res.data;
            console.log(this.Loan);
            router.push({
              params: { username: this.username },
            });
          } else {
            this.IsLoanAvailable = false;
          }
        },
        (err) => {
          console.log(err);
        }
      );
    },
  },
  created: function () {
    this.getLoan();
  },
};
</script>
<style scoped>
.center {
  width: 96%;
  margin: 26px auto;
}
.loans {
  display: inline;
  margin-left: 70%;
}
h1 {
  color: green;
}
.hello {
  color: black;
}
</style>
