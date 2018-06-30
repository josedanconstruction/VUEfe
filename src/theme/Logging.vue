<template>
    <div id="login">
        <h1>Login</h1>
        <input type="text" name="username" v-model="input.username" placeholder="Username" />
        <input type="password" name="password" v-model="input.password" placeholder="Password" />
        <button type="button" v-on:click="login()">Login</button>
    </div>
</template>

<script>
    var tokenPath = 'http://52.14.168.26:8081/api/security/login'
    var dataAPI = 'http://52.14.168.26:8081/api/client/city?area=boulder&report=master'
    var apiCall = require("../util/APIcall.js")
    var dataRequest = require("../util/DataRequest.js")
    export default {
        name: 'Login',
        data() {
            return {
                input: {
                    username: "",
                    password: ""
                }
            }
        },
        methods: {
            login() {
                if(this.input.username != "" && this.input.password != "") {
                  if(this.input.username == "admin" && this.input.password == "password"){
                    var token = apiCall.APItoken(tokenPath, 'admin', 'password', 'ADMIN')
                    token.done(function(response){
                      console.log(response)
                    })
                  }
                }

                if(this.input.username == "nraboy" && this.input.password == "password") {
                    var token = dataRequest.APItoken(tokenPath, 'user', 'clave', 'client')
                    debugger
                    token.done(function(response){
                      console.log(response)
                      dataRequest.APIget(dataAPI, response, '').then( value => {
                        console.log(value); // Success!
                      }, reason => {
                        console.log(reason); // Error!
                      } );
                  }
                )}
                else {
                    console.log("A username and password must be present");
                }
            }
        }
      }
</script>

<style scoped>
    #login {
        width: 500px;
        border: 1px solid #CCCCCC;
        background-color: #FFFFFF;
        margin: auto;
        margin-top: 200px;
        padding: 20px;
    }
</style>
