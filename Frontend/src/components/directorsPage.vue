<template>
  <div>
    <!-- page-header -->
    <div class="full-section banner parallax">
      <div class="overlay"></div>
      <div class="container">
        <div class="row">
          <div class="col-md-6 col-sm-6">
            <h4>Directors</h4> </div>
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
            <div class="post-content wow zoomIn" data-wow-duration="700ms" data-wow-delay="300ms">
              <!-- Post Image -->
              <div class="post-img">
                <img src="images/blog/blog1.jpg" alt="">
              </div>
              <!-- /Post Image-->
              <!-- Start Team-->
              <section id="team" class="section">
                <div class="container">
                  <div class="row" v-for="Director in Directors">
                    <div class="single_comment first-comment">
                      <div class="comment-avatar">
                        <div class="avatar">
                          <img v-if="Director.profileimg.path" :src="url+Director.profileimg.path.replace('public','')">
                          <img v-else src="static/images/no_image_available.jpeg" class="image" alt="" />
                        </div>
                      </div>
                      <div class="comment-content">
                        <div class="comment-name">{{Director.name}}</div>
                        <div class="comment-desc">{{Director.title}}</div>
                        <div class="comment-text">
                          <p>
                            {{Director.description}}
                          </p>
                        </div>
                      </div>
                    </div>
                  </div>
                  <!--/row-->
                </div>
                <!--/container-->
              </section>
              <!-- End Team-->
            </div>
          </div>
          <!-- /row -->
        </div>
      </div>
      <!-- /blog -->
    </div>
    <!--End Page section-->
  </div>
</template>
<script>
import env from '../env'
import auth from '../auth'
export default {
  name: 'DirectorsAdmin',
  data() {
    return {
      Directors: [],
      name: '',
      description: '',
      selectedDirector: '',
      formData: {},
      url: '',
      boolean: false
    }
  },
  methods: {
    fetchDirectors: function() {
      this.$http.get(env.URL + '/user/getAllDirectors').then(response => {
        this.Directors = response.data.data.Directors
        console.log(this.Directors)
      }).catch(error => {
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
    setSelectedDirector: function(Director) {
      this.selectedDirector = Director
      this.formData = new FormData()
      if (this.selectedDirector) {
        this.name = this.selectedDirector.name
        this.title = this.selectedDirector.title
        this.description = this.selectedDirector.description
        var $el = $('#editDirectorPicture');
      } else {
        this.name = ''
        this.description = ''
        var $el = $('#addDirectorPicture');
      }
      $el.wrap('<form>').closest('form').get(0).reset();
      $el.unwrap();
    },
    upload: function(fieldName, fileList) {
      // append the files to FormData
      Array.from(Array(fileList.length).keys()).map(x => {
        this.formData.append(fieldName, fileList[x], fileList[x].name);
      });
    }
  },
  created() {
    this.fetchDirectors()
    this.url = env.URL
  },
  components: {}
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#scroll {
  position: fixed;
  bottom: 100px;
  right: 50px;
}

img {
  height: auto;
}

img {
  max-width: 100%;
  border: none;
}

@media (min-width: 768px) .col-sm-12 {
  width: 100%;
}


.modal-content {
  position: relative;
  background-color: #1c1d26;
  border: 1px solid #999;
  border: 1px solid rgba(0, 0, 0, 0.2);
  border-radius: 6px;
  -webkit-box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  box-shadow: 0 3px 9px rgba(0, 0, 0, 0.5);
  background-clip: padding-box;
  outline: 0;
}

.\34 u img {
  max-height: 100%;
  max-width: 100%;
}

</style>
