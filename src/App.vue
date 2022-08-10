<script setup>
import AppCss from "../src/assets/App.css"
import BootstrapCss from "../src/assets/bootstrap.css"
import Datepicker from '@vuepic/vue-datepicker';
import '@vuepic/vue-datepicker/dist/main.css';

</script>

<template>
  <div class="row">
    <div class="col" style="max-width: 40%;">
      <div class="card">
        <!--***********************************************NEW FORM**********************************************************************-->
        <form id="form" @submit.prevent="addRecord()" v-if = "isHidden == true" v-on:click="isHidden == true"  >
          <h2 class="title">Form</h2><br>
          <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.userExists">{{msg.userExists}}</span>

          <div class="email-login">
            <label for = "firstName"><b>First Name </b></label>
            <input type="text" placeholder="Enter First Name" name="firstName" v-model = "firstName" required>
            <label for = "lastName"><b>Last Name </b></label>
            <input type="text" placeholder="Enter Last Name" name="lastName" v-model = "lastName" required>

            <label  for = "DOB"><b>DOB</b></label>
            <datepicker ref="DOB" v-model = "DOB" :format ="format" :preview-format ="format" :maxDate="new Date()" :enable-time-picker ="false"></datepicker>

            <label for="email"> <b>Email</b></label>
            <input type="email" placeholder="Enter Email"  name="email" v-model = "email" required>
            <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.email"><ul><li
            >{{msg.email}}</li></ul></span>

              <label for ="gender"> <b>Gender</b></label>
              <label>Male<input class= "maleRadio" name="gender" type ="radio" id="gender" v-model = "gender" value="male">
              </label>
              <label>Female<input class="femaleRadio" name="gender" type ="radio" id="gender" v-model = "gender" value="female"></label>


            <label for="phoneNo"><b>Phone Number</b></label>
            <input type="text" id="phoneno" placeholder="Enter Phone Number" name="phoneNo"  v-model = "phoneNo" required>
            <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.phoneNo"><ul><li
            >{{msg.phoneNo}}</li></ul></span>
            <label><b>Hobbies</b></label>
            <label v-for= "(hobbies, index) in hobbies" :key= index>
              {{ hobbies.label }}
              <input type="checkbox" :value="hobbies.value" v-model="checkedValues"/>
            </label>

          </div>
          <button type="submit" class="cta-btn" >Submit</button>
        </form>
<!--***********************************************UPDATE FORM**********************************************************************-->
        <form id="form" @submit.prevent="updateRecord()" v-else v-on:click="isHidden == !isHidden" >
          <h2 class="title">Form</h2><br>
          <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.userExists">{{msg.userExists}}</span>
          <div class="email-login">

            <label for = "UID"><b>UID</b></label>
            <input type="text" placeholder="Enter UID" name="UID" v-model = "UID" required>

            <label for = "fname"><b>First Name </b></label>
            <input type="text" placeholder="Enter First Name" name="firstName" v-model = "firstName" required>

            <label for = "lname"><b>Last Name </b></label>
            <input type="text" placeholder="Enter Last Name" name="lastName" v-model = "lastName" required>

            <label  for = "DOB"><b>DOB</b></label>
            <datepicker ref="DOB" v-model = "DOB" :format ="format" :preview-format ="format" :maxDate="new Date()" :enable-time-picker ="false" value="DOB"></datepicker>

            <label for="email"> <b>Email</b></label>
            <input type="email" placeholder="Enter Email"  name="email" v-model = "email" required>
            <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.email"><ul><li
            >{{msg.email}}</li></ul></span>

            <label for ="gender"> <b>Gender</b></label>
            <label>Male<input class= "maleRadio" name="gender" type ="radio" id="gender" v-model = "gender" value="male"></label>
            <label>Female<input class="femaleRadio" name="gender" type ="radio" id="gender" v-model = "gender" value="female"></label>

            <label for="phoneno"><b>Phone Number</b></label>
            <input type="text" id="phoneno" placeholder="Enter Phone Number" name="phoneNo"  v-model = "phoneNo" required>
            <span style="color:red ; font-size: 15px ; padding-bottom: 10px" v-if="msg.phoneNo"><ul><li
            >{{msg.phoneNo}}</li></ul></span>

            <label v-for= "(hobbies, index) in hobbies" :key= index>
              {{ hobbies.label }}
              <input type="checkbox" :value="hobbies.value" v-model="checkedValues"/>
            </label>
          </div>
          <button type="submit" class="cta-btn" >Update</button>
        </form>
      </div>
    </div>
<!--******************************************************TABLE********************************************************************-->
    <div class = "col" style="max-width: 200%">
      <div class="cardTable table">
        <table>
          <tr class = "row">
            <td class="col">
              <b>UID</b>
            </td>
            <td class = "col">
              <b>First Name</b>
            </td>
            <td class = "col">
              <b>Last Name</b>
            </td>
            <td class="col">
              <b>DOB</b>
            </td>
            <td class = "col">
              <b>Email</b>
            </td>
            <td class="col">
              <b>Gender</b>
            </td>
            <td class = "col">
              <b>Phone No</b>
            </td>
            <td class="col">
              <b>Hobbies</b>
            </td>
            <td class="col">
             <b>Actions</b>
            </td>
          </tr>


<!--*****************************************************************************************************-->
          <tr class = "row" v-for="(user,i) in allRecords" :key = "i">
            <td class = "col">
              {{user.UID}}
            </td>
            <td class = "col">
              {{user.firstName}}
            </td>
            <td class = "col">
              {{user.lastName}}
            </td>
            <td class="col">
              {{user.DOB}}
            </td>
            <td class = "col">
              {{user.email}}
            </td>
            <td class="col">
              {{user.gender}}
            </td>
            <td class = "col">
              {{user.phoneNo}}
            </td>
            <td class ="col">
              {{user.checkedValues}}
            </td>
            <td class="col">

                <button type="submit" class="cta-btn-table" @click = "editButton(user)">
                  Edit
                </button>

                <button type="submit" class="cta-btn-table" @click = "deleteButton(user)" >Delete</button>

            </td>


          </tr>

        </table>

    </div><br>
      <h4 class = "totalRecords">Total Number of Records : {{this.allRecords.length}}</h4>
    </div>

  </div>



</template>

<!-- ***************************************************JS************************************************************-->
<script>
import {ref} from "vue";
import dateFormat from "dateformat";

export default {
  setup() {
    const date = ref(new Date());
    const format = (date) => {
      const day = date.getDate();
      const month = date.getMonth() + 1;
      const year = date.getFullYear();

      return `${day}/${month}/${year}`;
    }

    return {
      date,
      format,
    }
  },

  data: () => ({
    form : "",
    key : "",
    UID:"",
    firstName: "",
    lastName: "",
    DOB:"",
    email: "",
    gender:"",
    phoneNo: "",
    hobbies:[
        { label: 'Playing', value: 'Playing' },
      { label: 'Singing', value: 'Singing' },
      { label: 'Reading', value: 'Reading' },
      {label: 'Photography', value: 'Photography'}
    ],
    checkedValues:[],
    msg:[],
    allRecords: [],
    user:[],
    displayData : "",
    isHidden : true}),

  watch: {
    email(value){
      this.email = value;
      if(value == ""){
        this.msg['email'] = '';
      }
      else{
        this.validateEmail(value);
      }

    },

    phoneNo(valuePhone){
        this.phoneNo = valuePhone;
        this.validatePhoneNo(valuePhone);
    }
  },

  methods: {
    clearForm() {
      this.firstName = "";
      this.lastName = "";
      this.DOB = "";
      this.email = "";
      this.gender = "";
      this.phoneNo = "";
      this.checkedValues = [];
    },
    validatePhoneNo(valuePhone){
        if(valuePhone.length == 0){
          this.msg['phoneNo'] = '';
        }
        else{
          if(valuePhone.length != 10){
            this.msg['phoneNo'] = 'Invalid Phone No';
          }
          else{
            this.msg['phoneNo'] = '';
          }
        }
    },
    validateEmail(value){
      if (!/^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(value))
      {
        this.msg['email'] = 'Invalid Email Address';
      } else{
        this.msg['email'] = '';
      }
    },

    addRecord(event) {

      const allRecords = this.allRecords;
      const formEmail = this.email;
      const formPhoneNo = this.phoneNo;
      const UID = Math.floor(100000 + Math.random() * 900000)
        const found = allRecords.some(el => el.email === formEmail || el.phoneNo === formPhoneNo );
        if (!found) {
          var mailformat = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
          if(this.firstName != "" && this.lastName != "" && this.email != "" && this.phoneNo != "" && this.checkedValues != "" && this.gender != "" && this.DOB != ""){
            if(this.phoneNo.length == 10){
              if(this.email.match(mailformat)){
                  this.allRecords.push({
                  UID : UID,
                  firstName: this.firstName,
                  lastName: this.lastName,
                  DOB : dateFormat(this.DOB,"mmmm dd,yyyy"),
                  email: this.email,
                  gender: this.gender ,
                  phoneNo: this.phoneNo ,
                  checkedValues: this.checkedValues });
                  this.clearForm();
              }
              else {
                this.msg['email'] = 'Invalid Email Address';
              }
            }
            else{
              this.msg['phoneNo'] = 'Invalid PhoneNo';
            }

          }
          else{
            this.msg['all'] = "Fill all fields";
          }

        }
        else {
          this.msg['userExists'] = "User Already Exists with Same Email or Phone No"
        }
      },

    editButton(user){
      this.UID = user.UID;
      this.firstName = user.firstName;
      this.lastName = user.lastName;
      const date = new Date(user.DOB)
      this.DOB = dateFormat(date,"mm/dd/yyyy");
      this.email = user.email;
      this.gender = user.gender;
      this.phoneNo = user.phoneNo;
      this.checkedValues = user.checkedValues;
      this.isHidden = false
    },

    updateRecord(){
      const allRecords = this.allRecords;
      const UID = this.UID;
      const formPhoneNo = this.phoneNo;
      const elementIndex = allRecords.findIndex(el => el.UID === UID );
      if(elementIndex != -1){
        var mailformat = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
          if(this.UID != "" && this.firstName != "" && this.lastName != "" &&  this.DOB != "" && this.email != "" && this.phoneNo != "" && this.gender != "" && this.checkedValues != "" ){
            if(this.phoneNo.length == 10){
              if(this.email.match(mailformat)){
                allRecords[elementIndex].firstName = this.firstName;
                allRecords[elementIndex].lastName = this.lastName;
                allRecords[elementIndex].DOB = dateFormat(this.DOB,"mmmm dd,yyyy");
                allRecords[elementIndex].email = this.email;
                allRecords[elementIndex].gender = this.gender;
                allRecords[elementIndex].phoneNo = this.phoneNo;
                allRecords[elementIndex].checkedValues = this.checkedValues;
                this.isHidden =true;
                this.clearForm();

              }
              else {
                this.msg['email'] = 'Invalid Email Address';
              }
            }
            else{
              this.msg['phoneNo'] = 'Invalid PhoneNo';
            }

          }
          else{
            this.msg['all'] = "Fill all fields";
          }

        }
        else {
          this.msg['userExists'] = "User Does not exist"
          this.isHidden = true;
        }
      },

    deleteButton(user){
      const allRecords = this.allRecords;
      const UID = user.UID;
      const elementIndex = allRecords.findIndex(el => el.UID === UID);
      if(elementIndex != -1){
        allRecords.splice(elementIndex);
      }
    }

    },
};


</script>
