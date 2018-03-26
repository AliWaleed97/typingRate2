<template>
  <!--Start Navigation-->
  <div id="header-sticky-wrapper" class="sticky-wrapper" style="height: 111px;">
    <header id="header">
      <div class="container">
        <div class="row">
          <div class="col-sm-12">
            <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#main-menu">
              <span class="sr-only">Toggle navigation</span>
              <span class="fa fa-bars"></span>
              <span class="icon-bar"></span>
              <span class="icon-bar"></span>
            </button>
            <!--Start Logo -->
            <div class="logo-nav">
              <a href="index.html">

                    <img src="/static/images/logo-copy.png" alt="Company logo">

                  </a>
            </div>
            <!--End Logo -->
            <div class="clear-toggle"></div>
            <div id="main-menu" class="collapse scroll navbar-right">
              <ul class="nav">
                <li class="active">  <a href="/">Home</a>  </li>
                <li> <a href="/aboutUs">About Us</a>  </li>
                <li> <a href="/projects">Projects</a> </li>
                <li> <a href="#">Clients</a> </li>
                <li> <a href="#">Contact</a> </li>
                <li v-if="!this.user.authenticated">
                  <a @click="openNav"><i class="fa fa-sign-in fa-2x" aria-hidden="true"> Login</i></a>
                </li>
                <li v-else-if="this.user.authenticated">Logout <a @click="logout"><i class="fa fa-sign-out fa-2x" aria-hidden="true"></i></a>
                </li>
              </ul>
            </div>
            <!-- End main-menu -->
          </div>
        </div>
      </div>
    </header>

      <div id="myNav" class="overlay">

    <!-- Button to close the overlay navigation -->
    <a href="javascript:void(0)" class="closebtn" @click="closeNav()">&times;</a>

    <!-- Overlay content -->
    <div class="overlay-content">
      <div class="container">
        <form class="form-group" @submit.prevent="login">
          <label class="test">Email</label>
          <input type="email" name="email" placeholder="Enter Your Email.." v-model="email" required>
          <label class="test">Password</label>
          <input type="password" name="password" placeholder="Enter Your Password.." v-model="password" required>
          <br>
          <input type="submit" class="button special">
        </form>
      </div>

    </div>

  </div>
  </div>
  <!--End Navigation-->
</template>
<script>
import env from './env'
import auth from './auth'
import router from './router'
export default {
name: 'AppNav',
  data() {
    return {
      email: "",
      password: "",
      user: auth.user,
      home: true
    }
  },
  created() {
    var self = this;
    if (this.$route.path === '/') {
      this.home = true
    } else {
      this.home = false
    }
    auth.checkAuth();
  },
  methods: {
    //open overlay
    openNav: function() {
      this.email = ""
      this.password = ""
      document.getElementById("myNav").style.width = "100%";
    },
    //close overlay
    closeNav: function() {
      document.getElementById("myNav").style.width = "0%";
    },
    // Send a request to the login URL and save the returned JWT
    login: function() {
      this.$http.post(env.URL + '/admin/authenticate', {
        email: this.email,
        password: this.password
      }).then((response) => {
        let data = {
          token: response.body.data.token,
          admin: JSON.stringify(response.body.data.admin)
        }
        auth.login(data)
        this.closeNav();
         this.$router.push('/admin' )
      }).catch((error) => {
        if (error.body.msg instanceof String || typeof error.body.msg === "string") {
          swal(
            'Oops...',
            error.body.msg,
            'error'
          );
        } else {
          for (var i = 0; i < error.body.msg.length; i++) {
            var msg = error.body.msg[i].msg
            alertify.notify(msg, 'error', 5);
          }
        }
      })
    },
    // To log out, we just need to remove the token
    logout: function() {
      auth.logout();
    },
  },


}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


.overlay {
  height: 100%;
  width: 0%;
  position: fixed;
  z-index: 1111;
  left: 0;
  top: 0;
  background-color: #000;
  background-color: rgba(0, 0, 0, .9);
  overflow-x: hidden;
  transition: .5s
}

.overlay-content {
  position: relative;
  top: 25%;
  width: 100%;
  text-align: center;
  margin-top: 30px;
}

.overlay a {
  padding: 8px;
  text-decoration: none;
  font-size: 36px;
  color: #818181;
  display: block;
  transition: .3s
}

.overlay a:focus,
.overlay a:hover {
  color: #f1f1f1
}


.overlay .closebtn {
  position: absolute;
  top: 20px;
  right: 45px;
  font-size: 60px
}
</style>
