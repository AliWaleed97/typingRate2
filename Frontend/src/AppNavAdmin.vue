<template>
  <div>
  <div class="header-bot">
  <div class="header-bot_inner_wthreeinfo_header_mid">
    <div class="col-md-4 header-middle">
  
    </div>
    <!-- header-bot -->
      <div class="col-md-4 logo_agile" align="left" >
        <img src="/static/images/fitLogo.png">
      </div>
        <!-- header-bot -->
    <div class="col-md-4 agileits-social top_content">
        
    </div>
    <div class="clearfix"></div>
  </div>
</div>
<!-- banner -->
<div class="ban-top">
  <div class="container">
    <div class="top_nav_left">
      <nav class="navbar navbar-default">
        <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <!-- <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
          <span class="sr-only">Toggle navigation</span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          <span class="icon-bar"></span>
          </button>
        </div> -->
        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse menu--shylock" id="bs-example-navbar-collapse-1">
          <ul class="nav navbar-nav menu__list">
          <li class=" menu__item "><router-link class="menu__link" to="/">Home</router-link></li>
          <li class=" menu__item"><router-link class="menu__link" to="/aboutUs">About</router-link></li>
          <li class="dropdown menu__item">
            <a href="#" class="dropdown-toggle menu__link" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Men's wear <span class="caret"></span></a>
              <ul class="dropdown-menu multi-column columns-3">
                <div class="agile_inner_drop_nav_info">

                  <div class="col-sm-3 multi-gd-img">
                    <ul class="multi-column-dropdown">
                      <li><router-link to="/services">Services</router-link></li>
                      <li><router-link to="/clients">Clients</router-link></li>
                    </ul>
                  </div>
                  <div class="col-sm-3 multi-gd-img">
                    <ul class="multi-column-dropdown">
                      <li><a href="mens.html">Jewellery</a></li>
                      <li><a href="mens.html">Sunglasses</a></li>
                    </ul>
                  </div>
                  <div class="clearfix"></div>
                </div>
              </ul>
          </li>
          <li class="dropdown menu__item">
            <a href="#" class="dropdown-toggle menu__link" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="false">Women's wear <span class="caret"></span></a>
              <ul class="dropdown-menu multi-column columns-3">
                <div class="agile_inner_drop_nav_info">
                  <div class="col-sm-3 multi-gd-img">
                    <ul class="multi-column-dropdown">
                      <li><a href="womens.html">Clothing</a></li>
                      <li><a href="womens.html">Wallets</a></li>
                    </ul>
                  </div>
                  <div class="col-sm-3 multi-gd-img">
                    <ul class="multi-column-dropdown">
                      <li><a href="womens.html">Jewellery</a></li>
                      <li><a href="womens.html">Sunglasses</a></li>
                    </ul>
                  </div>
                  <div class="col-sm-6 multi-gd-img multi-gd-text ">
                    <a href="womens.html"><img src="static/images/top1.jpg" alt=" "/></a>
                  </div>
                  <div class="clearfix"></div>
                </div>
              </ul>
          </li>
          <li class="menu__item dropdown">
             <a class="menu__link" href="#"  data-toggle="dropdown">Short Codes <b class="caret"></b></a>
                <ul class="dropdown-menu agile_short_dropdown">
                  <li><a href="icons.html">Web Icons</a></li>
                  <li><a href="typography.html">Typography</a></li>
                </ul>
          </li>
          <li class=" menu__item"><router-link class="menu__link" to="/contactUs">Contact</router-link>
          </li>
          </ul>
        </div>
        </div>
      </nav>  
    </div>
    <div class="top_nav_right">
      <div class="wthreecartaits wthreecartaits2 cart cart box_1"> 
            <form action="#" method="post" class="last"> 
            <input type="hidden" name="cmd" value="_cart">
            <input type="hidden" name="display" value="1">
            <button class="w3view-cart" type="submit" name="submit" value=""><i class="fa fa-cart-arrow-down" aria-hidden="true"></i></button>
          </form>  
  
            </div>
    </div>
    <div class="clearfix"></div>
  </div>
</div>
<!-- //banner-top -->
<router-view></router-view>
</div>
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
  created() {
    if (this.$route.path === '/') {
      this.home = true
    } else {
      this.home = false
    }
    auth.checkAuth();
  },
  updated() {
    if (this.$route.path === '/') {
      this.home = true
    } else {
      this.home = false
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
