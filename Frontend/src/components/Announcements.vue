<template>
  <section id="announcements" class="wrapper style1 special fade-up">
    <div class="full-section">
      <div class="container">
        <div class="row" v-for="Ann in announcements">
          <!-- Blog Post -->
          <div class="col-md-8 col-sm-8">
            <div class="post-content wow zoomIn" data-wow-duration="700ms" data-wow-delay="300ms">
              <!-- Post Image -->
              <div class="post-img">
                <img v-if="Ann.profileimg.path" :src="url+Ann.profileimg.path.replace('public','')">
                <img src="/static/images/rms.jpg" v-else>
              </div>
              <!-- /Post Image-->
              <!-- Post Description -->
              <div class="post-description wow zoomIn" data-wow-duration="700ms" data-wow-delay="400ms">
                <h3>{{Ann.title}}</h3>
                <!-- Post Meta-->
                <div class="post-meta">
                  <ul class="list-inline">
                    <li><a href="#"><i class="fa fa-calendar"></i>{{Ann.createdAt}}</a> </li>
                    <li><a href="#"><i class="fa fa-user"></i>by Admin</a></li>
                  </ul>
                </div>
                <!-- /Post Meta-->
                <p>
                  {{Ann.content}}
                </p>

              </div>
            </div>
          </div>
          <!-- /Post Description -->
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import env from '../env'
export default {
  name: 'Announcements',
  data() {
    return {
      announcements: [],
      url: ''
    }
  },
  created() {
    this.getAnnouncements()
    this.url = env.URL
  },
  methods: {
    // Send a request to the login URL and save the returned JWT
    getAnnouncements: function() {
      this.$http.get(env.URL + '/admin/getAnnouncements').then(data => {
        this.announcements = data.data.data.announcements
        console.log(this.announcements)
        this.announcements.sort(function(a, b) {
          return new Date(b.createdAt) - new Date(a.createdAt);
        })
        for (var i = 0; i < this.announcements.length; i++) {
          this.announcements[i].createdAt = this.formatDate(this.announcements[i].createdAt)
        }
      })
    },
    formatDate: function(date) {
      var date = new Date(date)
      var monthNames = [
        "January", "February", "March",
        "April", "May", "June", "July",
        "August", "September", "October",
        "November", "December"
      ];

      var day = date.getDate();
      var monthIndex = date.getMonth();
      var year = date.getFullYear();

      return day + ' ' + monthNames[monthIndex] + ' ' + year;
    }
  }
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#cd-timeline {
  position: relative;
  padding: 2em 0;
  margin-top: 2em;
  margin-bottom: 2em;
}

#cd-timeline::before {
  /* this is the vertical line */
  content: '';
  position: absolute;
  top: 0;
  left: 18px;
  height: 100%;
  width: 4px;
  background: #d7e4ed;
}

.cssanimations .cd-timeline-img.is-hidden {
  visibility: hidden;
}

.cssanimations .cd-timeline-img.bounce-in {
  visibility: visible;
  animation: cd-bounce-1 0.6s;
}

@keyframes cd-bounce-1 {
  0% {
    opacity: 0;
    transform: scale(0.5);
  }

  60% {
    opacity: 1;
    transform: scale(1.2);
  }

  100% {
    transform: scale(1);
  }
}

</style>
