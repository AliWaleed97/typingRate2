<template>
<div class="addFleet">
  <section id="four" class="wrapper style1 special fade-up">
    <div class="container">
      <header class="major">
        <h2>Add Fleet</h2>
      </header>

      <div class="row">
        <div class="col-md-8 col-md-offset-2">
          <form role="form" class="form-horizontal" v-on:submit.prevent="AddFleet()">
            <div class="form-group">
              <label for="exampleInputName2">Name</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Name" v-model="name" required>
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Client</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Client" v-model="client">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Location</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Location" v-model="location">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Engineer</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Class" v-model="engineer">
            </div>
            <div class="form-group">
              <label for="exampleInputEmail2">Description</label>
              <input type="text" class="form-control" id="exampleInputEmail2" placeholder="Description" v-model="desctiption">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Completion date</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Completion Date" v-model="completionDate">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Start Date</label>
              <input type="text" class="form-control" id="exampleInputName2" placeholder="Start Date" v-model="startDate">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Upload Pre-Images</label>
              <input ref="avatar" class="button special" type="file" name="avatar" id="avatar" v-on:change="upload($event.target.name, $event.target.files, 'pre')" multiple="multiple">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Upload During-Images</label>
              <input ref="avatar" class="button special" type="file" name="avatar" id="avatar" v-on:change="upload($event.target.name, $event.target.files, 'during')" multiple="multiple">
            </div>
            <div class="form-group">
              <label for="exampleInputName2">Upload Post-Images</label>
              <input ref="avatar" class="button special" type="file" name="avatar" id="avatar" v-on:change="upload($event.target.name, $event.target.files, 'post')" multiple="multiple">
            </div>
            <br>
            <br>
            <button type="submit" class="button special" v-if="!loading">Add Fleet</button>
            <button type="submit" class="button special" v-else><i class="fa fa-circle-o-notch fa-spin fa-fw"></i></button>
          </form>
        </div>
      </div>

    </div>
  </section>
</div>
</template>

<script>
import env from '../env'
import auth from '../auth'
import router from '../router'
export default {
  name: 'addFleet',
  data() {
    return {
      name:  "",
      client:  "",
      location:  "",
      engineer: "",
      desctiption:  "",
      completionDate:  "",
      startDate: "",
      project_id: "",
      formData1: [],
      formData2: [],
      formData3: [],
      images: [],
      loading: false
    }
  },
  methods: {
    // Send a request to the login URL and save the returned JWT
    AddFleet: function() {
      this.loading = true
      this.$http.post(env.URL + '/admin/addProject', {
          "name": this.name,
            "client": this.client,
            "location": this.location,
            "engineer": this.engineer,
            "desctiption": this.desctiption,
            "completionDate": this.completionDate,
            "startDate": this.startDate,
      }, {
        headers: auth.getAuthHeader()
      }).then(response => {
        this.project_id = response.data.data.Project._id
        if (this.formData1.length != 0) {
          this.formData1.append("Project_id", this.project_id)
          this.$http.post(env.URL + '/admin/addImage', this.formData1, {
            headers: auth.getAuthHeader()
          }).then(response => {
            if (this.formData2.length != 0) {
              this.formData2.append("Project_id", this.project_id)
              this.$http.post(env.URL + '/admin/addImage', this.formData2, {
                headers: auth.getAuthHeader()
              }).then(response => {
                if (this.formData3.length != 0) {
                  this.formData3.append("Project_id", this.project_id)
                  this.$http.post(env.URL + '/admin/addImage', this.formData3, {
                    headers: auth.getAuthHeader()
                  }).then(response => {
                    this.loading = false
                    alertify.notify(response.body.msg, 'success', 5);
                  }).catch((error) => {
                    this.loading = false
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
                        this.$router.go(-1)
                      }
                    }
                  })
                } else {
                  this.loading = false
                  alertify.notify(response.body.msg, 'success', 5);
                }
              }).catch((error) => {
                this.loading = false
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
                    this.$router.go(-1)
                  }
                }
              })
            } else {
              this.loading = false
              alertify.notify(response.body.msg, 'success', 5);
            }
          }).catch((error) => {
            this.loading = false
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
                this.$router.go(-1)
              }
            }
          })
        } else {
          this.loading = false
          alertify.notify(response.body.msg, 'success', 5);
        }
      }).catch((error) => {
        console.log(error)
        this.loading = false
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
    upload: function(fieldName, fileList, type) {
      // handle file changes
      const formData = new FormData();
      // append the files to FormData
      Array.from(Array(fileList.length).keys()).map(x => {
        formData.append(fieldName, fileList[x], fileList[x].name);
      });
      formData.append("Type", type)
      if(this.formData1.length == 0){
        this.formData1 = formData
      } else if (this.formData2.length == 0) {
        this.formData2 = formData
      } else if (this.formData3.length == 0) {
        this.formData3 = formData
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
