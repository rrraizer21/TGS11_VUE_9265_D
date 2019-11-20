<template>
  <v-app>
      <v-content>
          <v-container class="fill-height" fluid>
            <v-row align="center" justify="center">
                <v-col cols="6" md="6">
                    <v-card>
                        <v-row>
                            <v-col cols="12">
                                <div class="header">
                                    <div id="title" style="margin-left:315px">
                                        SIGN IN FOR CONTINUE
                                    </div>
                                </div>
                                <div class="form">
                                    <v-text-field
                                    v-model="form.email"
                                    label="Email"      
                                    outlined
                                    height=50
                                    ></v-text-field>

                                    <v-text-field
                                    v-model="form.password"
                                    label="Password"
                                    type="password"
                                    outlined
                                    height=50
                                    ></v-text-field>
                                    
                                 <v-btn @click="login()" rounded block class="elevation-0" color="primary" height=50 dark>SIGN IN NOW</v-btn>
                                </div>    
                            </v-col>
                        </v-row>
                    </v-card>
                </v-col>
            </v-row>
          </v-container>
      </v-content>
  </v-app>
</template>

<script>
export default {
    data () {
        return {
            checkbox: false,
            form : {
                email : null,
                password : null,
            },

            user: new FormData,
        }
    },
    methods :{
        login(){
            var url = this.$apiUrl + '/auth'
            this.user = new FormData()
            this.user.append('email', this.form.email)
            this.user.append('password', this.form.password)
            this.$http.post(url,this.user).then(response =>{
                if(response.data.token){
                    localStorage.setItem("token", response.data.token)
                    this.$router.push({name : 'UserController'})
                }else{
                    alert('Username atau Password yang anda Masukkan Salah!')
                }
            })
        }
    },
}
</script>

<style>
    .header{
        margin-left: 47px;
        margin-top: 50px;
    }

    #title{
        font-family: Roboto;
        font-style: normal;
        font-weight: bold;
        font-size: 32px;
        line-height: 56px;
    }

    .form{
        margin-top: 47px;
        margin-left: 38px;
        margin-bottom: 50px;
        margin-right: 38px;
    }
</style>