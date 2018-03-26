<template>

<div>
    <!-- Start Page loader -->
    <!-- <div id="pageloader">
      <div class="loader">
        <img src="static/images/progress.gif" alt='loader' />
      </div>
    </div> -->
    <!--End Page loader -->

    <!-- page-header -->
    <div class="full-section banner parallax">
       <div class="overlay"></div>
       <div class="container">
           <div class="row">
               <div class="col-md-6 col-sm-6"> <h4>About Us</h4> </div>
           </div>
       </div>
   </div>
    <!-- /page-header -->

    <div class="container">
      <br>
      <br>
      <div class="row">
        <div class="4u 12u$(medium)">
          <header>
            <h2>Founder Message</h2>
          </header>
        </div>
        <br>
        <br>
        <div>
          <p >"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."</p>
        </div>
        <div>
          <p align="left">"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."</p>
        </div>
      </div>
      <br>
      <br>
      <div class="row">
        <div class="4u 12u$(medium)">
          <header>
            <h2>Personnel</h2>
          </header>
        </div>
        <br>
        <br>
        <div>
          <p align="left">"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.""Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.""Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."</p>
        </div>
      </div>
      <br>
      <br>
  </div>

</div>

</div>
</template>

<script>
export default {
  name: 'aboutUsPage',
  data() {
    return {}
  },
  created() {
    var self = this;
    self.initSlick();
  },
  methods: {
    initSlick: function() {
      this.$nextTick(function() {

      $(window).ready(function() {
          $(".loader-item").delay(500).fadeOut();
          $("#pageloader").delay(1000).fadeOut("slow");
        });
      });
    }
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#tab1:checked~#content1,
#tab2:checked~#content2,
#tab3:checked~#content3,
#tab4:checked~#content4,
#tab5:checked~#content5 {
  display: block;
}

.tab_container .tab-content p,
.tab_container .tab-content h3 {
  -webkit-animation: fadeInScale 0.7s ease-in-out;
  -moz-animation: fadeInScale 0.7s ease-in-out;
  animation: fadeInScale 0.7s ease-in-out;
}

.tab_container .tab-content h3 {
  text-align: center;
}

.tab_container [id^="tab"]:checked+label {
  background: #1c1d26;
  box-shadow: inset 0 3px #e44c65;
}

.tab_container [id^="tab"]:checked+label .fa {
  color: #1c1d26;
}

label .fa {
  font-size: 1.3em;
  margin: 0 0.4em 0 0;
}


label {
  font-weight: 700;
  font-size: 18px;
  display: block;
  float: left;
  width: 33%;
  cursor: pointer;
  text-decoration: none;
  text-align: center;
}


input,
section {
  clear: both;
  padding-top: 10px;
  display: none;
}




input[type=checkbox]+label:before,
input[type=radio]+label:before {
  border: 1px solid rgba(255, 255, 255, .3);
  content: '';
  display: none;
  height: 1.8em;
  left: 0;
  line-height: 1.725em;
  position: absolute;
  text-align: center;
  top: 0;
  width: 1.8em;
}


.spotlight.style1 .content {
  border-color: #191a22;
}

.\34 u,
.\34 u\24 {
  width: 100%%;
}
</style>
