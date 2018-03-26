<template>
<div class="projects">

         <!-- Start Team-->
         <section id="team" class="section">
             <div class="overlaym"></div>
              <div class="container">
                  <div class="row">

                     <!--Start heading-->
                     <div class="col-md-offset-2 col-md-8 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="300ms">
                          <div class="section-header">
                              <h2 class="smt"><span> Projects</span></h2>
                          </div>
                      </div>
                      <!--End heading-->

                      <!--No project-->
                    <div class="col-md-offset-2 col-md-8 wow fadeInUp" v-if="projects.length==0" style="text-align: center; clear:both;" data-wow-duration="700ms" data-wow-delay="500ms">
                      <h3>No projects added.</h3>
                    </div>

                      <!--Start Team item #1-->
                      <div class="col-lg-4 col-md-6 col-sm-6 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="500ms" v-for="project in first_three_projects">
                        <a>
                          <router-link v-bind:to="'/project/' + project._id">
                            <div class="team-member">
                              <img v-if="project.profilePic" :src="url+project.profilePic.replace('public','')" class="image" alt=""/>
                              <img v-else src="static/images/no_image_available.jpeg" class="image" alt=""/>

                                 <div class="team-info">
                                      <h4>{{project.name}}</h4>
                                      <p v-if="project.client">{{project.client}}</p>
                                      <p v-else>No client</p>

                                 </div>
                            </div>
                            </router-link>
                          </a>
                      </div>


                  </div> <!--/row-->

              </div> <!--/container-->

              <div class="clear"></div>

                 <div class="work-all wow fadeInUp" data-wow-duration="700ms" data-wow-delay="800ms"> <router-link to="/projects"> <a  class="btn btn-primary btn-lg" style="position: relative; z-index: 100;">View All Projects</a></router-link> </div>


         </section>
        <!-- End Team-->


</div>
</template>

<script>
import env from '../env'
export default {
  name: 'projects',
  data() {
    return {
      projects: [],
      first_three_projects: [],
      url: ""
    }
  },
  components: {},
  methods: {
    fetchProjects: function() {
      this.$http.get(env.URL + '/user/getAllProjects').then((response) => {
        if (response.body.success) {
          this.projects = response.body.data.Projects
          if(response.body.data.Projects[0]){
            this.first_three_projects.push(response.body.data.Projects[0]);
          }
          if(response.body.data.Projects[1]){
            this.first_three_projects.push(response.body.data.Projects[1]);
          }
          if(response.body.data.Projects[2]){
            this.first_three_projects.push(response.body.data.Projects[2]);
          }

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
