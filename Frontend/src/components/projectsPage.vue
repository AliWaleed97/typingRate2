<template>

<div>
  <!-- page-header -->
  <div class="full-section banner parallax">
     <div class="overlay"></div>
     <div class="container">
         <div class="row">
             <div class="col-md-6 col-sm-6"> <h4>Projects</h4> </div>


         </div>
     </div>
 </div>
  <!-- /page-header -->


<!--Start Page section-->
<div class="page-section">

  <!--Start blog -->
  <div class="full-section">
      <div class="container">
          <div class="row">
              <!-- Blog Post -->
                  <div class="post-content wow zoomIn"  data-wow-duration="700ms" data-wow-delay="300ms">
                      <!-- Post Image -->
                      <div class="post-img">
                          <img src="images/blog/blog1.jpg" alt="">
                      </div>
                      <!-- /Post Image-->

                      <!-- Start Team-->
                      <section id="team" class="section">
                           <div class="container">
                               <div class="row">

                                     <!--No project-->
                                   <div v-if="projects.length==0" style="text-align: center;" data-wow-duration="700ms" data-wow-delay="500ms">
                                     <h3>No projects added.</h3>
                                   </div>

                                     <!--Start Team item #1-->
                                   <div class="col-lg-4 col-md-6 col-sm-6 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="500ms" v-for="project in projects">
                                     <a>
                                       <router-link v-bind:to="'/project/' + project._id">
                                       <div class="team-member">
                                           <img v-if="project.profilePic" :src="url+project.profilePic.replace('public','')" class="image" alt="" />
                                           <img v-else src="static/images/no_image_available.jpeg" class="image" alt="" />

                                              <div class="team-info">
                                                   <h4>{{project.name}}</h4>
                                                   <p v-if="project.client">{{project.client}}</p>
                                                   <p v-else>No client</p>
                                                   <ul class="socials">
                                                       <li><a href="#"><i class="fa fa-facebook"></i></a></li>
                                                       <li><a href="#"><i class="fa fa-twitter"></i></a></li>
                                                       <li><a href="#"><i class="fa fa-google-plus"></i></a></li>
                                                       <li><a href="#"><i class="fa fa-linkedin"></i></a></li>
                                                    </ul>
                                              </div>
                                       </div>
                                     </router-link>

                                   </a>

                                   </div>


                               </div> <!--/row-->

                           </div> <!--/container-->

                      </section>
                     <!-- End Team-->

                  </div>



          </div> <!-- /row -->
      </div>
  </div>
  <!-- /blog -->


</div>
<!--End Page section-->



</div>
</template>

<script>
import env from '../env'

export default {
  name: 'projectsPage',
  data() {
    return {
      projects: [],
      url: "",
    }
  },
  components: {},
  methods: {
    fetchProjects: function() {
      this.$http.get(env.URL + '/user/getAllProjects').then((response) => {
        if (response.body.success) {
          this.projects = response.body.data.Projects
          console.log(this.projects[2].profilePic.substring())
        } else {
          this.error = response.body.msg
        }
      })
    },
  },

  created: function() {
    this.fetchProjects();
    this.url = env.URL;
  }
  }
  </script>

  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

  </style>
