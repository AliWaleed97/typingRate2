<template>
<div id="app" style="height:100%;">

  <router-view></router-view>

</div>
</template>

<script>
import AppNav from './AppNav.vue'
import AppNavBar from './AppNavBar.vue'
import AppNavAdmin from './AppNavAdmin.vue'
import router from './router'
var custom = require('../static/js/custom.js');

//var AppNav = () =>
//import ('./AppNav.vue')
//import AppFooter from './AppFooter.vue'
var AppFooter = () =>
  import ('./AppFooter.vue')
export default {
  name: 'app',
  components: {
    AppNav,
    AppNavBar,
    AppFooter,
    AppNavAdmin,
  },

  created: function() {
    var self = this;
    // self.initSlick();
  },

  methods: {
    // initSlick: function() {
    //
    //   this.$nextTick(function() {
    //
    //     var wow = new WOW();
    //     wow.init();
    //
    //     jQuery("#header").sticky({
    //       topSpacing: 0
    //     });
    //
    //     $(window).load(function() {
    //       $('.homeslider').flexslider({
    //         animation: "fade",
    //         controlNav: false,
    //         directionNav: false,
    //         slideshowSpeed: 6000,
    //       });
    //     });
    //
    //     jQuery('#text-slider').bxSlider({
    //       mode: 'fade',
    //       pager: false,
    //       auto: true,
    //       controls: false
    //     });
    //
    //
    //     $(".single-work-slider").owlCarousel({
    //
    //       navigation: false, // Show next and prev buttons
    //       slideSpeed: 400,
    //       pagination: false,
    //       singleItem: true,
    //       autoPlay: true,
    //       navigation: true,
    //       navigationText: [
    //         "<i class='fa fa-angle-left'></i>",
    //         "<i class='fa fa-angle-right'></i>"
    //       ],
    //
    //     });
    //
    //     $('.related-project-carousel').owlCarousel({
    //       autoPlay: 3000,
    //       slideSpeed: 200,
    //       items: 4,
    //       itemsDesktop: [1199, 4],
    //       itemsDesktopSmall: [979, 3],
    //       stopOnHover: true,
    //       pagination: false,
    //       navigation: true,
    //       navigationText: [
    //         "<i class='fa fa-angle-left'></i>",
    //         "<i class='fa fa-angle-right'></i>"
    //       ],
    //     });
    //
    //     $(window).bind('load', function() {
    //       if (!onMobile)
    //         parallaxInit();
    //     });
    //
    //     function parallaxInit() {
    //       $('#facts').parallax("50%", 0.2);
    //       $('#cta').parallax("50%", 0.2);
    //       $('#pricing').parallax("50%", 0.2);
    //       $('#contact').parallax("50%", 0.2);
    //       $('#banner').parallax("50%", 0.2);
    //
    //       /*add as necessary*/
    //     }
    //
    //     var onMobile = false;
    //     if (/Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent)) {
    //       onMobile = true;
    //     }
    //
    //     jQuery('.work-grid').mixitup({
    //       targetSelector: '.mix',
    //     });
    //
    //     $('.popup-image').magnificPopup({
    //       type: 'image',
    //       closeOnContentClick: true,
    //       mainClass: 'mfp-img-mobile',
    //       image: {
    //         verticalFit: true
    //       }
    //
    //     });
    //
    //
    //     (function($) {
    //       "use strict";
    //       $(".scroll a[href^='#']").on('click', function(e) {
    //         e.preventDefault();
    //         var hash = this.hash;
    //         $('html, body').stop().animate({
    //           scrollTop: $(hash).offset().top
    //         }, 2000, 'easeOutExpo');
    //       });
    //     })(jQuery);
    //
    //     $('.collapse ul li a').click(function() {
    //       $('.navbar-toggle:visible').click();
    //     });
    //
    //     $(window).scroll(function() {
    //       if ($(this).scrollTop() > 100) {
    //         $('.scrollup').fadeIn();
    //       } else {
    //         $('.scrollup').fadeOut();
    //       }
    //     });
    //
    //     $('.scrollup').click(function() {
    //       $("html, body").animate({
    //         scrollTop: 0
    //       }, 2000);
    //       return false;
    //     });
    //
    //
    //   });
    // }
  },

  data() {
    return {
      admin: false,
      home:true

    }
  },
  updated() {

    if (this.$route.path === '/admin') {
      this.admin = true
    } else if (this.$route.path === '/') {
      this.admin = false
      this.home = true
    }else {
        this.home = false
    }
  },


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
