<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-white">
    <a class="navbar-brand"><img class="nav-img" src="https://media-exp1.licdn.com/dms/image/C510BAQFcsfRxRwPkfQ/company-logo_200_200/0?e=2159024400&v=beta&t=7coWtr_u9KmMQ9e9yrpy9U5TWTN4cbOvjWQNAmdZfmI"></a>
    </nav>
    <div class="row top">
    <transition name="fade" mode="out-in">

        <div key=1 class="col-lg-8 col-xl-6 col-sm-10 main-panel" v-if="!loggedIn">
            <div class="header">
                <h5 v-if="!success" style="color:#b30000" class="mt-3 mb-1">Registration failed. Please try again.
                    <br>{{message}}
                </h5>
                <br>
                <strong>SIGN UP</strong>
                <br><br>
                <h3>Create your account</h3>
                <br>
                <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
            </div>
            <div class="row second">


                <div class="col-md-5 col-10 main mb-1 mb-md-0">
                    <div class="content">
                    <img src="https://i.pinimg.com/originals/39/21/6d/39216d73519bca962bd4a01f3e8f4a4b.png">
                    Sign Up with Google
                    </div>
                </div>
                <!-- <div class="col-1">              -->
                <div class="col-md-5 col-10 main mt-1 mt-md-0">
                    <div class="content">
                    <img src="https://icons-for-free.com/iconfiles/png/512/color+facebook+icon-1320168272811213233.png">
                    Sign Up with Facebook
                    </div>
                    <fb:login-button style="opacity:0;"
                    scope="public_profile,email">
                    </fb:login-button>
                </div> 
            </div>
            <div class="row second my-2 mt-md-0">
                <div class="col-5 mx-auto">
                    <hr>
                </div>
                <div class="col-2  mx-auto">
                     or
                </div>
               
                <div class="col-5 mx-auto">
                    <hr>
                </div>
            </div>
            <div class="row">   
                <div class="col-12 m-0">
                    <div class="form-group ">
                        <input type="text" class="form-control" id="" v-model="user.fname" placeholder="First Name" required>
                    </div>
                </div>
                <div class="col-12 m-0">
                    <div class="form-group ">
                        <input type="text" class="form-control" v-model="user.lname" placeholder="Last Name" required>
                    </div>
                </div>
                <div class="col-12 m-0">
                    <div class="form-group ">
                        <input type="email" class="form-control" v-model="user.email" placeholder="Email" required>
                    </div>
                </div>
                <div class="col-12 m-0">
                    <div class="form-group form-field">
                        <input :type="visible" class="form-control" v-model="user.password" placeholder="Password" id="password" required>
                        <img src="https://static.thenounproject.com/png/7467-200.png" @click="showPass()" alt="Your image" class="input-icon" />
                    </div>
                </div>
                <div class="col-12 m-0">
                    <p>By clicking Sign Up, you agree to our <span>Terms of Use</span> and our <span> Privacy Policy</span></p>
                </div>
                <div class="col-12 m-0">
                    <button type="button" @click="sendData()" class="btn btn-info size">Sign Up</button>
                </div>

            </div>
        </div>
        <div key=2 class="col-lg-8 col-xl-6 col-sm-10 main-panel" v-else>
             <div class="header">
                 <br>
                <h5>Hello, {{user.fname}}!</h5>
                <br>
                <h3 style="color:#138496;">You have been successfully registered. <br>
                </h3>
                <br>
                <h4>Your details are listed below: </h4>
                <br>
                <ul class="text-left">
                <li>First Name: <strong>{{this.user.fname}}</strong></li>
                <li>Last Name: <strong>{{this.user.lname}}</strong></li>
                <li>Email: <strong>{{this.user.email}}</strong></li>
                </ul>
                <br>
                <button type="button" @click="loggedIn=false" class="btn btn-info size">Register again</button>
            </div>
        </div>
    </transition>
    </div>
  </div>
</template>

<script>
export default {
    data(){
        return{
            visible: 'password',
            user:[{
                fname:'',
                lname:'',
                email:'',
                password:''
            }],
            data:[],
            loggedIn: false,
            success:true,
            message:'',
        }
    },
    methods:{
        showPass(){
            this.visible= this.visible==='password'?'text':'password'
            console.log(this.user)
        },
        sendData(){
              this.$http.post ('https://reqres.in/api/register', {"email":this.user.email, 'password':this.user.password }).then(function (response) {
                 console.log(response);
                 this.data=response
                 this.loggedIn= true;
                this.success=response.ok
                 console.log(this.success)
            })
            .catch(function(error){
            console.log(error)
            this.success=error.ok
            this.message=error.body.error

    });
    },
    
  },
  created: function() {
    console.log('created main');
    window.fbAsyncInit = function() {
      window.FB.init({
        appId      : '321329778977007',
        xfbml      : true,
        version    : 'v8.0'
      });

      //This function should be here, inside window.fbAsyncInit

   };

    (function(d, s, id){
     var js, fjs = d.getElementsByTagName(s)[0];
     if (d.getElementById(id)) {return;}
     js = d.createElement(s); js.id = id;
     js.src = "//connect.facebook.net/en_US/sdk.js";
     fjs.parentNode.insertBefore(js, fjs);
    }(document, 'script', 'facebook-jssdk'));
  }
}


</script>

<style scoped>
    .form-field { position: relative; }
    .form-field #password {line-height: 20px; }
    .form-field .input-icon { position: absolute; max-height: 20px; max-width: 20px; right: 20px; top: 22%; z-index: 2; }

    .password{
 
  /* background-color: floralwhite; */
  background-image: url("https://static.thenounproject.com/png/7467-200.png");
  background-size: 50px 50px;
  background-repeat: no-repeat;
  background-position: 99% 100%;
    }

    .top{
        margin-top:50px;
        margin-bottom:100px
    }
    .navbar{
        box-shadow: 1px 1px 32px #d8d6d6;

    }
    .navbar-brand{
        margin: 0 auto
    }
    .nav-img{
        width:30%;
        height:auto;
    }
    .main-panel{
        border: 1px solid #1111;
        font-weight:300;
        padding: 0 90px;
        padding-bottom:40px;
        margin:0 auto;

    }
    .main{
        border: 1px solid #1111;
        font-weight:350;
        height: 50px;
        display: flex;
        width:100vw;
        justify-content: center;
        align-items: center;
        margin:0 auto;
    }
    .size{
        width:100%;
    }
    .content{
          flex: 0 0 200px;
          width:100%;
          position:absolute;
    }
    img{
     width:20%;   
    }
    .one{
        margin-left:20px
    }
    span{
        color:#138496;
    }
    input:focus:active,input:focus{
    outline: none;
    -webkit-box-shadow: none;
    box-shadow: none;
    /* border:none; */
    }
    .second{
        margin:0 auto;
    }
    @media screen and (max-width: 420px) {
       .main-panel{
           padding:0 40px;
       }
    }
    .fade-enter-active,
.fade-leave-active {
    transition: opacity 0.6s
}

.fade-enter,
.fade-leave-to {
    opacity: 0
}
</style>