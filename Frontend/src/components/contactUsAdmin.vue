<template>
  <div class="contactUsAdmin">
    <!-- Four -->
    <section id="four" class="wrapper style1 special fade-up">
<!--       <div class="table-wrapper">
        <div v-for='inf in announcements'>
          <h1> {{inf.number}} </h1>
        </div>
        <div v-for='text in announcements.texts'>
          <h1> {{text}} </h1>
        </div>
      </div> -->
      <div class="container">
        <div class="table-wrapper">
          <div v-for='text in phones'>
            <h1> {{text}} </h1>
          </div>
        </div>
        <div>
          <p>{{number}}</p>
          <input type="text" name="number" v-model="number" required>
        </div>
        <div>
          <button data-toggle="modal" data-target="#editPhone" class="button special">Edit</button>
          </td>
        </div>
      </div>
      <!-- Modal -->
      <div class="modal fade" id="editPhone" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
        <div class="modal-dialog">
          <!-- Modal content-->
          <div class="modal-content">
            <!-- Modal header-->
            <div class="modal-header">
              <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
              <h4><CENTER>Edit Phone</CENTER></h4>
            </div>
            <!-- Modal body-->
            <div class="modal-body">
              <div class="row" style="border:none;">
                <div class="col-md-12">
                  <form @submit.prevent="addPhone()" role="form" style="display: block;">
                    <table>
                      <thead>
                        <tr>
                          <th>Phone</th>
                          <th>Actions</th>
                        </tr>
                      </thead>
                      <tbody>
                        <tr v-for="phone in phones">
                          <td>{{phone}}</td>
                          <td><a v-on:click="deletePhone(phone)" class="button special">Delete</a></td>
                        </tr>
                        <td>
                          <input type="text" name="phone" v-model="phone" required>
                        </td>
                        <td>
                          <button class="button special">+</button>
                        </td>
                      </tbody>
                    </table>
                  </form>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <form @submit.prevent="addBlock()" role="form" style="display: block;">
        <button class="button special">Add Block</button>
      </form>
    </section>
  </div>
</template>
<script>
import env from '../env'
import auth from '../auth'
export default {
  name: 'contactUsAdmin',
  data() {
    return {
      phones: [],
      info: {texts:[],
            number:''
      },
      number: '',
      phone: '',
      mobile: '',
      fax: '',
      contactPerson: ''
    }
  },
  created() {
    this.getBlocks()
  },
  methods: {
    getBlocks: function() {
      this.$http.get(env.URL + '/admin/getBlocks').then(data => {
        this.announcements = data.data.data.announcements
        console.log(this.announcements)
      })
    },
    addBlock: function() {
      console.log(this.info)
      this.info.texts = this.phones
      this.info.number = this.number
      console.log(this.info)
      this.$http.post(env.URL + '/admin/addBlock', this.info).then(response => {
        alertify.notify(response.body.msg, 'success', 5);
        this.fetchInfo()
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
    addPhone: function() {
      var phones = this.phones
      if (phones.indexOf(this.phone) == -1) {
        this.phones.push(this.phone)
        this.phone = ''
      } else {
        alertify.notify("Duplicate number", 'error', 5);
      }
    }
  }
}

</script>
<style scoped>
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

article.special,
section.special {
  text-align: left;
  padding-left: 2.55em;
}

h3 {
  text-align: center;
}

</style>
