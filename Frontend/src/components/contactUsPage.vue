<template>
<div class="contactUsPage">

 <!--/contact-->
    <div class="banner_bottom_agile_info">
      <div class="container">
      <div class="contact-grid-agile-w3s">
        <div class="col-md-4 contact-grid-agile-w3">
            <div class="contact-grid-agile-w31">
              <i class="fa fa-map-marker" aria-hidden="true"></i>
              <h4>Address</h4>
              <p>17, Al-Hasan St., off Yathreb St., Dokki, <span> Cairo, Egypt</span></p>
            </div>
          </div>
          <div class="col-md-4 contact-grid-agile-w3">
            <div class="contact-grid-agile-w32">
              <i class="fa fa-phone" aria-hidden="true"></i>
              <h4>Call Us</h4>
              <p>+ (202) 3760 8362<span>+ (202) 3760 8364</span></p>
            </div>
          </div>
          <div class="col-md-4 contact-grid-agile-w3">
            <div class="contact-grid-agile-w33">
              <i class="fa fa-envelope-o" aria-hidden="true"></i>
              <h4>Email</h4>
              <p><a href="mailto:info@example.com">info@example1.com</a><span><a href="mailto:info@example.com">info@example2.com</a></span></p>
            </div>
          </div>
          <div class="clearfix"> </div>
        </div>
     </div>
   </div>
     <div class="contact-w3-agile1 map" data-aos="flip-right">
      <iframe width="100%" height="600" src="https://maps.google.com/maps?width=100%&amp;height=600&amp;hl=en&amp;coord=30.0410911,31.195042899999976&amp;q=%0917%2C%20Al-Hasan%20St.%2C%20off%20Yathreb%20St.%2C%20Dokki%2C%20Cairo%2C%20Egypt+(Fit%20In)&amp;ie=UTF8&amp;t=&amp;z=14&amp;iwloc=B&amp;output=embed" frameborder="0" scrolling="no" marginheight="0" marginwidth="0"><a href="https://www.maps.ie/create-google-map/">Create Google Map</a></iframe>
      
       <!-- <iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d100949.24429313939!2d-122.44206553967531!3d37.75102885910819!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x80859a6d00690021%3A0x4a501367f076adff!2sSan+Francisco%2C+CA%2C+USA!5e0!3m2!1sen!2sin!4v1472190196783" class="map" style="border:0" allowfullscreen=""></iframe> -->
     </div>
   <div class="banner_bottom_agile_info">
  <div class="container">
     <div class="agile-contact-grids">
        <div class="agile-contact-left">
          <div class="col-md-6 address-grid">
            <h4>For More <span>Information</span></h4>
              <div class="mail-agileits-w3layouts">
                <i class="fa fa-volume-control-phone" aria-hidden="true"></i>
                <div class="contact-right">
                  <p>Telephone </p><span>+ (202) 3760 8362, 4</span>
                </div>
                <div class="clearfix"> </div>
              </div>
              <div class="mail-agileits-w3layouts">
                <i class="fa fa-envelope-o" aria-hidden="true"></i>
                <div class="contact-right">
                  <p>Mail </p><a href="mailto:info@example.com">info@example.com</a>
                </div>
                <div class="clearfix"> </div>
              </div>
              <div class="mail-agileits-w3layouts">
                <i class="fa fa-map-marker" aria-hidden="true"></i>
                <div class="contact-right">
                  <p>Address</p><span>17, Al-Hasan St., off Yathreb St., Dokki, Cairo, Egypt</span>
                </div>
                <div class="clearfix"> </div>
              </div>
              
          </div>
          <div class="col-md-6 contact-form">
            <h4 class="white-w3ls">Contact <span>Form</span></h4>
            <form action="#" method="post">
              <div class="styled-input agile-styled-input-top">
                <input type="text" name="Name" required="">
                <label>Name</label>
                <span></span>
              </div>
              <div class="styled-input">
                <input type="email" name="Email" required=""> 
                <label>Email</label>
                <span></span>
              </div> 
              <div class="styled-input">
                <input type="text" name="Subject" required="">
                <label>Subject</label>
                <span></span>
              </div>
              <div class="styled-input">
                <textarea name="Message" required=""></textarea>
                <label>Message</label>
                <span></span>
              </div>   
              <input type="submit" value="SEND">
            </form>
          </div>
        </div>
        <div class="clearfix"> </div>
      </div>
       </div>
  </div>
 <!--//contact-->
<!--/grids-->
<div class="coupons">

</div>
<!--grids-->
</div>
</template>

<script>
import env from '../env'
export default {
  name: 'contactUsPage',
  data() {
    return {
      info: {}
    }
  },
  created() {
    this.fetchInfo()

  },
  methods: {
    fetchInfo: function() {
      this.$http.get(env.URL + '/user/getInfo').then(response => {
        this.info = response.data.data.info
      })
    }
  }
}
</script>

<style scoped>
article.special, section.special {
    text-align: left; 
    padding-left: 2.55em;
}

h3{
padding-left: 2.55em;
}
.td{
  text-align: right;
}

</style>
