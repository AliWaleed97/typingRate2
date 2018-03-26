<template>
  <div>
    <!-- Start Header-->
    <div class="full-section banner parallax" v-bind:style="{ 'background-position': 'center 26.85px' ,'background-image':'url('+coverPic+')', 'background-size': '100%',
    'background-repeat': 'no-repeat'}">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-md-6 col-sm-6">
            <h4>{{project.name}}</h4></div>
        </div>
      </div>
    </div>
    <!-- End Header-->
    <!--Start Page Section-->
    <div class="page-section">
      <!--Start single-work -->
      <div class=" full-section single-work wow zoomIn" data-wow-duration="700ms" data-wow-delay="400ms">
        <div class="container">
          <div class="row">
            <div class="col-md-7">
              <div class="single-work-slider owl-carousel owl-theme">
                <div class="item" v-for="image in 3">
                  <img :src="carousel[image-1]">
                </div>
              </div>
            </div>
            <!--Start Work Detail-->
            <div class="col-md-5 work-detail wow zoomIn" data-wow-duration="700ms" data-wow-delay="500ms">
              <div class="heading">
                <h2>Project Description</h2></div>
              <p v-if="project.description">{{project.description}}</p>
              <p v-else>No description</p>
              <hr>
              <ul class="work-detail-list">
                <li><span>Client :</span><i v-if="project.client">{{project.client}}</i><i v-else>No client</i></li>
                <li><span>Engineer :</span><i v-if="project.engineer">{{project.engineer}}</i><i v-else>No engineer</i></li>
                <li><span>Location :</span><i v-if="project.location">{{project.location}}</i><i v-else>No location</i></li>
                <li><span>Start date :</span><i v-if="project.startDate">{{project.startDate}}</i><i v-else>No start date</i></li>
                <li><span>Completion date :</span><i v-if="project.completionDate">{{project.completionDate}}</i><i v-else>No completion date</i></li>
              </ul>
            </div>
            <!--End Work Detail-->
          </div>
          <!--/ row-->
        </div>
        <!--/ container-->
      </div>
      <!--End single-work -->
      <!--related works -->
      <div class="featured-works full-section parallax wow zoomIn" data-wow-duration="700ms" data-wow-delay="700ms">
        <div class="container">
          <div class="row">
            <!--Start heading-->
            <div class="heading">
              <h2>Pre Construction Images</h2>
            </div>
            <!--End heading-->
          </div>
          <!-- /.row -->
        </div>
        <!-- /.container -->
        <div class="related-project-carousel owl-carousel">
          <!-- Start Item-->
          <div class="item" v-for="image in preImages">
            <div class="fworks-image">
              <img :src="image" alt="" />
              <!--Hover link-->
              <div class="hover-link">
                <a href="#">
                                    <i class="fa fa-link"></i>
                                </a>
                <a v-bind:href="image" class="popup-image">
                                    <i class="fa fa-search-plus"></i>
                                </a>
              </div>
              <!--End link-->
              <!--Hover Caption-->
              <div class="featured-caption">
                <h4>Project Title</h4>
                <p>category</p>
              </div>
              <!--End Caption-->
            </div>
          </div>
          <!-- End Item-->
        </div>
      </div>
      <div class="featured-works full-section parallax wow zoomIn" data-wow-duration="700ms" data-wow-delay="700ms">
        <div class="container">
          <div class="row">
            <!--Start heading-->
            <div class="heading">
              <h2>During Construction Images</h2>
            </div>
            <!--End heading-->
          </div>
          <!-- /.row -->
        </div>
        <!-- /.container -->
        <div class="related-project-carousel owl-carousel">
          <!-- Start Item-->
          <div class="item" v-for="image in duringImages">
            <div class="fworks-image">
              <img :src="image" alt="" />
              <!--Hover link-->
              <div class="hover-link">
                <a href="#">
                                    <i class="fa fa-link"></i>
                                </a>
                <a v-bind:href="image" class="popup-image">
                                    <i class="fa fa-search-plus"></i>
                                </a>
              </div>
              <!--End link-->
              <!--Hover Caption-->
              <div class="featured-caption">
                <h4>Project Title</h4>
                <p>category</p>
              </div>
              <!--End Caption-->
            </div>
          </div>
          <!-- End Item-->
        </div>
      </div>
      <div class="featured-works full-section parallax wow zoomIn" data-wow-duration="700ms" data-wow-delay="700ms">
        <div class="container">
          <div class="row">
            <!--Start heading-->
            <div class="heading">
              <h2>Post Construction Images</h2>
            </div>
            <!--End heading-->
          </div>
          <!-- /.row -->
        </div>
        <!-- /.container -->
        <div class="related-project-carousel owl-carousel">
          <!-- Start Item-->
          <div class="item" v-for="image in postImages">
            <div class="fworks-image">
              <img :src="image" alt="" />
              <!--Hover link-->
              <div class="hover-link">
                <a href="#">
                                    <i class="fa fa-link"></i>
                                </a>
                <a v-bind:href="image" class="popup-image">
                                    <i class="fa fa-search-plus"></i>
                                </a>
              </div>
              <!--End link-->
              <!--Hover Caption-->
              <div class="featured-caption">
                <h4>Project Title</h4>
                <p>category</p>
              </div>
              <!--End Caption-->
            </div>
          </div>
          <!-- End Item-->
        </div>
      </div>
      <!-- End related works -->
    </div>
    <!--End Page Section-->
  </div>
</template>
<script>
import env from '../env'
import Vue from 'vue'

export default {
  name: 'projectsPage',
  data() {
    return {
      project: "",
      url: "",
      images: [],
      coverPic: "",
      profilePic: "",
      postImages: [],
      duringImages: [],
      preImages: [],
      carousel: [],
      length: 0
    }
  },
  components: {},
  methods: {
    fetchProject: function() {
      this.$http.get(env.URL + '/user/getProject/' + this.$route.params.project_id).then((response) => {
        if (response.body.success) {
          this.project = response.body.data.Project
          this.profilePic = env.URL.concat(this.project.profilePic.replace('public', ''))
        } else {
          this.error = response.body.msg
        }
      })
    },
    getImages: function() {
      this.$http.get(env.URL + '/user/getImages/'.concat(this.$route.params.project_id)).then(response => {
        this.images = response.data.data.images
        this.length = this.length + this.images.length
        this.updateArray(this.images)
        this.coverPic = this.carousel[2]
      })
    },
    updateArray: function(array) {
      for (var i = 0; i <= 2; i++) {
        if (array[i] != null) {
          this.carousel[i] = env.URL.concat(array[i].img.path.replace('public', ''))
        }
      }

    },
    updatePath: function(array) {
      for (var i = 0; i <= array.length; i++) {
        if (array[i] != null) {
          array[i] = env.URL.concat(array[i].img.path.replace('public', ''))
        }
      }
    },


    initSlick: function() {

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


  created: function() {
    this.url = env.URL;
    this.fetchProject();
    this.getImages();
  },
  mounted: function() {
    var vm = this;
    this.$http.get(env.URL + '/user/getImages/'.concat(this.$route.params.project_id)).then(response => {
      this.images = response.data.data.images
      this.length = this.length + this.images.length


      // console.log(array)
      for (var i = 0; i < this.images.length; i++) {
        if (this.images[i].Type == 'post') {
          this.postImages.push(this.images[i])
        } else if (this.images[i].Type == 'during') {
          this.duringImages.push(this.images[i])
        } else if (this.images[i].Type == 'pre') {
          this.preImages.push(this.images[i])
        }
      }
      this.carousel = this.images.slice(0,3)

      this.updateArray(this.carousel)
      this.updatePath(this.postImages)
      this.updatePath(this.duringImages)
      this.updatePath(this.preImages)
      console.log(this.postImages)
      console.log("Post")
      console.log(this.duringImages)
      console.log("during")
      console.log(this.preImages)
      console.log("[pre]")

      Vue.nextTick(function() {
        vm.initSlick();
      }.bind(vm));
    }).catch((err) => {
      if (err) console.log(err);
    });


  },
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
