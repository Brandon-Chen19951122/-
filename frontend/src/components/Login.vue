<template>

    <div class="row">
    
    <div class="col-sm-4" >
     <h2 align="center"> Login</h2>
   
     <form @submit.prevent="LoginData">
     
   
     <div class="form-group" align="left">
       <label>電話</label>
       <input type="phone" v-model="employee.phone" class="form-control"  placeholder="電話">
     </div>


    <div class="form-group" align="left">
    <label>密碼</label>
    <input type="password" v-model="employee.password" class="form-control"  placeholder="密碼">
  </div>
  <br/>

     <button type="submit" class="btn btn-primary">Login</button>
     </form>
   </div>
   </div>

</template>
   
   <script>
       import Vue from 'vue';
       import axios from 'axios';
   
     Vue.use(axios)
     export default {
       name: 'Registation',
       data () {
         return {
           result: {},
           employee:{
                      phone: '',
                      password: ''
           }
         }
       },
       created() { 
       },
       mounted() {
             console.log("mounted() called.......");
         },
       methods: {
              LoginData()
              {
               axios.post("http://localhost:8090/api/v1/employee/login", this.employee)
               .then(
                 ({data})=>{
                  console.log(data);
                  try {
                  if (data.message === "Email not exits") 
                      {
                       alert("電話號碼不存在");
                       
                        }
                         else if(data.message == "Login Success")
                        {
                       
                         this.$router.push({ name: 'Home' })
                        }
                         else 
                        { 
                            alert("Incorrect Phone and Password not match");
                        }

                        } catch (err) {
                        alert("Error, please try again");
                        }    
                 }
               )
              }
         }
     }
     </script>