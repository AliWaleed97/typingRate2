<template>
  <div class="DirectorsAdmin" align="left">
    <br>
    <br>
    <br>
    <br>
    <!-- Directors Admin -->
    <section id="four" class="wrapper style1 special fade-up">
      <div class="container">
        <header class="major">
          <h2>Directors</h2>
        </header>
        <section class="col-lg-12 col-md-12 col-sm-12 small-padding">
          <div class="row" v-for="Director in Directors">
            <div class="col-lg-12 col-md-12 col-sm-12">
              <div class="col-lg-4 col-md-4 col-sm-12">
                <div data-animation class="team-member">
                  <img v-if="Director.profileimg.path" :src="url+Director.profileimg.path.replace('public','')">
                  <img v-else src="/static/images/pic07.jpg">
                </div>
              </div>
              <div class="col-lg-8 col-md-6 col-sm-12">
                <h3>{{Director.name}}</h3>
                <h3>{{Director.title}}</h3>
                <p>{{Director.description}}</p>
                <ul class="actions">
                  <li><a data-toggle="modal" data-target="#editDirector" class="button special" v-on:click="setSelectedDirector(Director)">Edit</a></li>
                  <li><a class="button special" v-on:click="deleteDirector(Director._id)">Delete</a></li>
                </ul>
                <br>
              </div>
            </div>
          </div>
        </section>
      </div>
      <section class=" 4u 6u(medium) 12u$(xsmall) ">
        <CENTER>
          <button id="scroll" data-toggle="modal" data-target="#addDirector" class="button special big" v-on:click="setSelectedDirector('')">+</button>
        </CENTER>
      </section>
      <!-- Modal -->
      <div class="modal fade" id="editDirector" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <!-- Modal content-->
          <div class="modal-content">
            <!-- Modal header-->
            <div class="modal-header">
              <button type="button" class="close" data-dismiss="modal" aria-label="Close" v-on:click="setSelectedDirector('')"><span aria-hidden="true">&times;</span></button>
              <h4><CENTER>Edit Director</CENTER></h4>
            </div>
            <!-- Modal body-->
            <div class="modal-body">
              <div class="row" style="border:none;">
                <div class="col-md-12">
                  <form @submit.prevent="editDirector()" role="form" style="display: block;">
                    <label class="test">Name</label>
                    <input type="text" name="name" v-model="name" required>
                    <label class="test">Title</label>
                    <input type="text" name="title" v-model="title" required>
                    <label class="test">Description</label>
                    <textarea type="text" name="description" v-model="description" required></textarea>
                    <div class="form-group">
                      <label for="exampleInputName2">Upload Images</label>
                      <input ref="avatar" class="button special" type="file" name="avatar" id="editDirectorPicture" v-on:change="upload($event.target.name, $event.target.files)">
                    </div>
                    <br>
                    <div>
                      <CENTER>
                        <button class="button special">Submit</button>
                      </CENTER>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <!-- Modal -->
      <div class="modal fade" id="addDirector" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <!-- Modal content-->
          <div class="modal-content">
            <!-- Modal header-->
            <div class="modal-header">
              <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
              <h4><CENTER>Add Director</CENTER></h4>
            </div>
            <!-- Modal body-->
            <div class="modal-body">
              <div class="row" style="border:none;">
                <div class="col-md-12">
                  <form @submit.prevent="addDirector()" role="form" style="display: block;" class="form-group">
                    <label class="test">Name</label>
                    <input type="text" name="name" placeholder="Name" v-model="name" required>
                    <label class="test">Title</label>
                    <input type="text" name="title" placeholder="Title" v-model="title" required>
                    <label class="test">Description</label>
                    <textarea type="text" name="description" placeholder="Description" v-model="description" required></textarea>
                    <div class="form-group">
                      <label for="exampleInputName2">Upload Images</label>
                      <input ref="avatar" class="button special" type="file" name="avatar" id="addDirectorPicture" v-on:change="upload($event.target.name, $event.target.files)">
                    </div>
                    <div>
                      <br>
                      <CENTER>
                        <input class="button special" type="submit" value="Submit">
                      </CENTER>
                    </div>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
    <br>
    <br>
    <br>
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
      title:'',
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
    addDirector: function() {
      this.formData.append("name", this.name)
      this.formData.append("title", this.title)
      this.formData.append("description", this.description)
      this.$http.post(env.URL + '/admin/addDirector', this.formData, {
        headers: auth.getAuthHeader()
      }).then(response => {
        $('#addDirector').modal('hide');
        alertify.notify(response.body.msg, 'success', 5);
        this.fetchDirectors()
      }).catch((error) => {
        this.setSelectedDirector('')
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
    editDirector: function() {
      this.formData.append("id", this.selectedDirector._id)
      this.formData.append("name", this.name)
      this.formData.append("title", this.title)
      this.formData.append("description", this.description)
      this.$http.post(env.URL + '/admin/updateDirector', this.formData, {
        headers: auth.getAuthHeader()
      }).then(response => {
        $('#editDirector').modal('hide');
        alertify.notify(response.body.msg, 'success', 5);
        this.fetchDirectors()
      }).catch(error => {
        this.setSelectedDirector(this.selectedDirector)
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
    deleteDirector: function(DirectorId) {
      swal({
        title: 'Are you sure?',
        text: "You won't be able to revert this!",
        type: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#3085d6',
        cancelButtonColor: '#d33',
        confirmButtonText: 'Yes, delete it!'
      }).then(() => {
        this.$http.post(env.URL + '/admin/deleteDirector', {
          id: DirectorId
        }, {
          headers: auth.getAuthHeader()
        }).then((response) => {
          swal(
            'Deleted!',
            response.body.msg,
            'success'
          )
          this.fetchDirectors()

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
      }, (dismiss) => {})
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
