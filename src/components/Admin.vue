<template>

<div class="admin">

              <h1> {{ msg }} </h1>
              <!-- <h3> {{name}} </h3> -->
              <!-- <h3> {{desc}} </h3> -->
              <!-- <hr> -->
              <!-- <User></User> -->
              <hr>
  <div>

<div class="container">
  <form id="newUserform" @submit="submitForm">
    <div class="row">
      <div class="col-25">
        <label for="fname">First Name</label>
      </div>
      <div class="col-75">
        <input type="text" id="fname" name="firstname" placeholder="Your first name..">
      </div>
    </div>
    <div class="row">
      <div class="col-25">
        <label for="lname">Last Name</label>
      </div>
      <div class="col-75">
        <input type="text" id="lname" name="lastname" placeholder="Your last name..">
      </div>
    </div>
    <div class="row">
      <div class="col-25">
        <label for="mobile">Mobile</label>
      </div>
      <div class="col-75">
        <input type="text" id="mobile" name="mobile" placeholder="Your Mobile Number..">
      </div>
    </div>
    <div class="row">
      <div class="col-25">
        <label for="email">Email</label>
      </div>
      <div class="col-75">
        <input type="text" id="email" name="email" placeholder="Your email address..">
      </div>
    </div>
    <div class="row">
      <div class="col-25">
        <label for="country">Country</label>
      </div>
      <div class="col-75">
        <select id="country" name="country">
          <option value="australia">Australia</option>
          <option value="india">India</option>
          <option value="canada">Canada</option>
          <option value="usa">USA</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-25">
        <label for="subject">Address</label>
      </div>
      <div class="col-75">
        <textarea id="address" name="address" placeholder="Enter full address here.." style="height:200px"></textarea>
      </div>
    </div>
    <div class="pull-right">
      <button type="button" class="btn btn-success" @click="submitForm">Save</button>
    </div>
  </form>
</div>

       </div>
    </div>
</template>




<script>
import User from './User'
import HelloWorld from './HelloWorld'
import axios from 'axios';
// import api from '../services/api';

// const api = new api

export default {
name: 'Admin',
components: {
    User,
    HelloWorld
},
// data: {
//   todos: [],
//   name: String,
//   description: String,
// },
 data () {
    return {
      name: String,
      desc: String,
      msg: 'Welcome Admin'
    }
  },

created() {

    axios.get(`http://localhost:3500/users/users`)
    .then(res => {
     console.log('res here...', res.data);
    })
    .catch(e => {
      console.log('err here...',e);
    })

  },

  mounted() {
  console.log(process.env.ROOT_API)
},
  methods: {
    submitForm(){
      let password = Math.random().toString(36).slice(-8);
      let userData = new FormData();
      userData.firstname = fname.value;
      userData.lastname = lname.value;
      userData.mobile = mobile.value;
      userData.email = email.value;
      userData.address = address.value;
      userData.country = country.value;
      userData.password = password;
      // console.log('generated password', password);
      console.log('form data ...', userData);
      
    axios({
    method: 'post',
    url: 'http://localhost:3500/users/create',
    data: {userData} ,
    config: { 
      headers: {'Content-Type': 'application/json'}
      }
    })
    .then(function (response) {
        console.log('res here',response);
    })
    .catch(function (response) {
        console.log('err here',response);
    });
     this.$router.push({ path : '/' });
    }
  }
}
</script>




<style>
/* Style inputs, select elements and textareas */
input[type=text], select, textarea{
  width: 100%;
  padding: 12px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  resize: vertical;
}

/* Style the label to display next to the inputs */
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}

/* Style the submit button */
input[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  float: right;
}

/* Style the container */
.container {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

/* Floating column for labels: 25% width */
.col-25 {
  float: left;
  width: 25%;
  margin-top: 6px;
}

/* Floating column for inputs: 75% width */
.col-75 {
  float: left;
  width: 75%;
  margin-top: 6px;
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}

/* Responsive layout - when the screen is less than 600px wide, make the two columns stack on top of each other instead of next to each other */
@media screen and (max-width: 600px) {
  .col-25, .col-75, input[type=submit] {
    width: 100%;
    margin-top: 0;
  }
}
</style>

