<template>
<div id="Banner">
  <div class="margin"></div>
  <!--Start Services-->
  <section id="services" class="section">
    <div class="container">
      <div class="row">

        <!--Start heading-->
        <div class="col-md-offset-2 col-md-8 wow zoomIn" data-wow-duration="700ms" data-wow-delay="300ms">
          <div class="section-header">
            <h2 class="smt"><span>Services</span></h2>
          </div>
        </div>
        <!--End heading-->

        <!--Services Item #1-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="300ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-leaf"></i> </div>
            <div class="services-desc">
              <h4>Web Design</h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>

        <!--Services Item #2-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="400ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-edit"></i> </div>
            <div class="services-desc">
              <h4>CMS Integration</h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>

        <!--Services Item #3-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="500ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-leaf"></i> </div>
            <div class="services-desc">
              <h4>SEO</h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>


        <!--Services Item #4-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="600ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-rocket"></i> </div>
            <div class="services-desc">
              <h4>Graphic Design</h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>

        <!--Services Item #5-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="700ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-film"></i> </div>
            <div class="services-desc">
              <h4>Responsive Design </h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>

        <!--Services Item #6-->
        <div class="col-md-4 wow zoomIn" data-wow-duration="700ms" data-wow-delay="800ms">
          <div class="services-box">
            <div class="services-icon"> <i class="fa fa-codepen"></i> </div>
            <div class="services-desc">
              <h4>Corporate Design</h4>
              <p>Lorem ipsum dolor consectetur adipisicing incididunt eiusmod tempor incididunt laboredolore magna aliqua.</p>
            </div>
          </div>
        </div>

      </div>
      <!--/.row-->
    </div>
    <!--/.container-->
  </section>
  <!--End Services-->
  <!--Start facts-->
  <section id="facts" class="section parallax">

    <div class="container">
      <div class="row">
        <!--Start facts info #1-->
        <div class="col-lg-3 col-md-3 col-sm-6 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="300ms">
          <div class="facts-detail">
            <i class="fa fa-group"></i>
            <span>250</span>
            <p>Clients</p>
          </div>
        </div>

        <!--Start facts info #3-->
        <div class="col-lg-3 col-md-3 col-sm-6 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="500ms">
          <div class="facts-detail">
            <i class="fa fa-gift"></i>
            <span>300</span>
            <p>Completed Projects</p>
          </div>
        </div>

        <!--Start facts info #4-->
        <div class="col-lg-3 col-md-3 col-sm-6 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="600ms">
          <div class="facts-detail">
            <i class="fa fa-trophy"></i>
            <span>53</span>
            <p>Award Won</p>
          </div>
        </div>
      </div>
      <!--/row-->
    </div>
    <!--/container-->
  </section>
  <!--End facts-->


</div>
</template>

<script>
export default {
  name: 'banner',
  data() {
    return {}
  },
  created(){
    var self = this;
    self.initWorkGrid();
  },
  methods: {
    initWorkGrid: function(){

      this.$nextTick(function() {
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
    })
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.overlaym{
  background-image: url();
}

.crop {
  width: 300px;
  height: 350px;
  overflow: hidden;
}

.crop img {
  height: 50%;
  width: 100%;
  max-width: 100%;
  max-width: 100%;
}

.slide1 {
  background: url(/static/images/device.png) center center;
}

.slide2 {
  background: url(/static/images/slider/slide2.jpg) center center;
}

.slide3 {
  background: url(/static/images/slider/slide3.jpg) center center;
}
</style>
