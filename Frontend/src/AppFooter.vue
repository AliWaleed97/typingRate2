<template>
<div class="AppFooter">
    <!--Start footer-->
    <footer>
        <div class="container wow zoomIn"  data-wow-duration="700ms" data-wow-delay="500ms">
            <div class="row">
                <div class="col-md-12 text-center">
                    <!--Start footer social-->
                    <ul class="list-inline footer-social">
                       <li><a href="#"><i class="fa fa-facebook"></i></a></li>
                       <li><a href="#"><i class="fa fa-vimeo-square"></i></a></li>
                       <li><a href="#"><i class="fa fa-instagram"></i></a></li>
                       <li><a href="#"><i class="fa fa-behance"></i></a></li>
                       <li><a href="#"><i class="fa fa-twitter"></i></a></li>
                       <li><a href="#"><i class="fa fa-dribbble"></i></a></li>
                    </ul>
                    <!-- End footer social -->

                    <!-- footer copyright text -->
                    <p>Copyright &copy; 2018 All reserved</p>
                    <!-- end of the footer copyright text -->
                </div>
            </div> <!--/.row-->
        </div> <!--/.container-->
    </footer>
    <!--End footer-->

    <a href="#" class="scrollup"> <i class="fa fa-chevron-up"> </i> </a>

<!-- //footer -->
</div>
</template>

<script>
export default {
  name: 'AppFooter',
  data() {
    return {}
  },

  created() {
    var self = this;
    self.initGoTop();
  },

  methods: {
    initGoTop: function() {
      this.$nextTick(function() {

        $(window).scroll(function() {
          if ($(this).scrollTop() > 100) {
            $('.scrollup').fadeIn();
          } else {
            $('.scrollup').fadeOut();
          }
        });

        $('.scrollup').click(function() {
          $("html, body").animate({
            scrollTop: 0
          }, 2000);
          return false;
        });

    })
  },
}


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#footer1:before {
  background-position: center;
  background-image: url(/static/images/RapidoGee.jpg);
  background-size: cover;
  background-attachment: fixed;
}

.spotlight {
  background-attachment: fixed;
  background-size: cover;
  box-shadow: 0 0.25em 0.5em 0 rgba(0, 0, 0, .25);
  height: 30vh;
  position: relative;
}
</style>
