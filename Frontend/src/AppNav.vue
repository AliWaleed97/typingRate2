<template>
<div class="AppNav" style="height:100%">
  <!--Start Slider -->
  <section id="home">
    <div class="slider-overlay"></div>
    <div class="homeslider flexslider">
      <ul class="slides">
        <li class="slide1 bg"></li>
        <li class="slide2 bg"></li>
        <li class="slide3 bg"></li>
      </ul>
    </div>
    <!--/ homeslider-->
    <!-- start text slider-->
    <div class="tb">
      <div class="tb-cell">
        <div class="slide-text">
          <ul id="text-slider">
            <li>
              <h1>WE ARE CREATIVE INTERIOR DESIGN</h1></li>
            <li>
              <h1>EASY CUSTOMIZE</h1></li>
            <li>
              <h1>RESPONSIVE & CLEAN DESIGN</h1></li>
          </ul>
          <div class="page-scroll scroll"><a class="btn btn-lg btn-primary btn-color-white" href="#services">What we do</a>
            <a class="btn btn-lg btn-primary btn-color-white" href="#works">View Works</a>
          </div>
        </div>
      </div>
    </div>
  </section>
  <!--End Slider-->
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
  created() {
    var self = this;
    self.initSlick();

    if (this.$route.path === '/') {
      this.home = true
    } else {
      this.home = false
    }
    auth.checkAuth();
  },
  methods: {
    //open overla
    initSlick: function() {

      this.$nextTick(function() {

        var wow = new WOW();
        wow.init();

        jQuery("#header").sticky({
          topSpacing: 0
        });

        $(window).load(function() {
          $('.homeslider').flexslider({
            animation: "fade",
            controlNav: false,
            directionNav: false,
            slideshowSpeed: 6000,
          });
        });

        jQuery('#text-slider').bxSlider({
          mode: 'fade',
          pager: false,
          auto: true,
          controls: false
        });


        $(".single-work-slider").owlCarousel({

          navigation: false, // Show next and prev buttons
          slideSpeed: 400,
          pagination: false,
          singleItem: true,
          autoPlay: true,
          navigation: true,
          navigationText: [
            "<i class='fa fa-angle-left'></i>",
            "<i class='fa fa-angle-right'></i>"
          ],

        });

        $('.related-project-carousel').owlCarousel({
          autoPlay: 3000,
          slideSpeed: 200,
          items: 4,
          itemsDesktop: [1199, 4],
          itemsDesktopSmall: [979, 3],
          stopOnHover: true,
          pagination: false,
          navigation: true,
          navigationText: [
            "<i class='fa fa-angle-left'></i>",
            "<i class='fa fa-angle-right'></i>"
          ],
        });

        $(window).bind('load', function() {
          if (!onMobile)
            parallaxInit();
        });

        function parallaxInit() {
          $('#facts').parallax("50%", 0.2);
          $('#cta').parallax("50%", 0.2);
          $('#pricing').parallax("50%", 0.2);
          $('#contact').parallax("50%", 0.2);
          $('#banner').parallax("50%", 0.2);

          /*add as necessary*/
        }

        var onMobile = false;
        if (/Android|webOS|iPhone|iPad|iPod|BlackBerry/i.test(navigator.userAgent)) {
          onMobile = true;
        }

        jQuery('.work-grid').mixitup({
          targetSelector: '.mix',
        });

        $('.popup-image').magnificPopup({
          type: 'image',
          closeOnContentClick: true,
          mainClass: 'mfp-img-mobile',
          image: {
            verticalFit: true
          }

        });



        $('.collapse ul li a').click(function() {
          $('.navbar-toggle:visible').click();
        });


      });
    }
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

.slide1:before{
    background: url(/static/images/slider/slide1.webp) center center;
}

.slide2:before{
    background: url(/static/images/slider/slide2.webp) center center;
}

.slide3:before{
    background: url(/static/images/slider/slide3.webp) center center;
}

</style>
