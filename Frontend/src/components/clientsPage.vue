<template>
<div class="clients">

  <!--Start clients-->
  <section id="clients" class="section">
    <div class="overlayk"></div>
      <div class="container wow fadeInUp" data-wow-duration="700ms" data-wow-delay="600ms">
            <div class="row">

              <!--Start heading-->
              <div class="col-md-offset-2 col-md-8 wow fadeInUp" data-wow-duration="700ms" data-wow-delay="300ms">
                <div class="section-header">
                  <h2 class="smt"><span>Clients</span></h2>
                </div>
              </div>
              <!--End heading-->


                <div v-if="clients.length != 0" class="clients-carousel">
                     <div  class="col-md-3 col-xs-6" v-for="client in clients">
                         <a v-on:click="changeClient(client)" data-toggle="modal" data-target="#myModal">
                             <figure>
                               <img v-if="client.profileimg.path" :src="url+client.profileimg.path.replace('public','')">
                               <img v-else src="/static/images/pic07.jpg">
                             </figure>
                         </a>
                      </div>
                </div>

                <div style="clear:both" v-if="clients.length == 0">
                    <br>
                    <h3> No clients added </h3>
                </div>

            </div> <!--/row-->
        </div> <!--/container-->
  </section>
  <!--End clients-->

  <!-- Modal -->
<div id="myModal" class="modal fade" role="dialog">
  <div class="modal-dialog">

    <!-- Modal content-->
    <div class="modal-content">

      <div class="modal-body">
        <div class="row">
          <div class="col-lg-4 col-md-4 col-sm-12">
            <div data-animation class="team-member">
              <figure v-if="client1"  style="margin: 5px; background: rgba(172, 108, 32, 0.35);  padding: 40px 10px; margin-bottom: 30px;">
                <img v-if="client1.profileimg.path" :src="url+client1.profileimg.path.replace('public','')">
                <img v-else src="/static/images/pic07.jpg">
              </figure>
            </div>
          </div>
          <div v-if="client1" class="col-lg-8 col-md-6 col-sm-12">
            <h3>{{client1.name}}</h3>
            <p>{{client1.description}}</p>
            <br>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
      </div>
    </div>

  </div>
</div>


</div>
</template>

<script>
import env from '../env'
export default {
  name: 'clients',
  data() {
    return {
      clients: [],
      client1: '',
      url: ""
    }
  },
  components: {},
  methods: {

    fetchClients: function() {
      this.$http.get(env.URL + '/user/getAllClients').then((response) => {
        if (response.body.success) {
          this.clients = response.body.data.clients
          this.client1 = response.body.data.clients[0]
        } else {
          this.error = response.body.msg
        }
      })
    },

    changeClient: function(client) {
      this.client1 = client;
    }
  },

  created: function() {
    this.fetchClients();
    this.url = env.URL;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
