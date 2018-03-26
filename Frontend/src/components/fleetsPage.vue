<template>
  <div class="fleetsPage">
    <div class="single-pro">
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m1.jpg" alt="">
            <div class="men-cart-pro">
            </div>
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Formal Blue Shirt</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m2.jpg" alt="">
            <div class="men-cart-pro">
            </div>
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Gabi Full Sleeve Sweatshirt</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m3.jpg" alt="">
            <div class="men-cart-pro">
            </div>
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Dark Blue Track Pants</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m4.jpg" alt="">
            <div class="men-cart-pro">
            </div>
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Round Neck Black T-Shirt</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m5.jpg" alt="">
            <div class="men-cart-pro">
            </div>
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Men's Black Jeans</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m7.jpg" alt="">
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Analog Watch</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m6.jpg" alt="">
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Reversible Belt</a></h4>
          </div>
        </div>
      </div>
      <div class="col-md-3 product-men">
        <div class="men-pro-item simpleCart_shelfItem">
          <div class="men-thumb-item">
            <img src="/static/images/m8.jpg" alt="">
          </div>
          <div class="item-info-product ">
            <h4><a href="single.html">Party Men's Blazer</a></h4>

          </div>
        </div>
      </div>
      <br>
      <div class="clearfix"></div>
    </div>
  </div>
  </div>
  <!-- //mens -->
  </div>
</template>
<script>
import env from '../env'
import {
  Carousel3d,
  Slide
} from 'vue-carousel-3d';
export default {
  name: 'fleetsPage',
  data() {
    return {
      fleets: [],
      url: ""
    }
  },
  created() {
    this.fetchFleets()
    this.url = env.URL
  },
  updated() {
    $('.carousel-3d-container').css("height", "273px")
    $('.carousel-3d-controls>a').css("border-bottom", "none")
  },
  methods: {
    fetchFleets: function() {
      this.$http.get(env.URL + '/user/getAllFleets').then(response => {
        this.fleets = response.data.data.fleets
      })
    },
  },
  components: {
    Carousel3d,
    Slide
  },
}

</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  -webkit-filter: grayscale(0);
  cursor: pointer;
  transition: all .5s ease;
  max-width: 90%;
  max-height: auto;
  height: auto;
  width: auto;
}

.imgcarousel {
  display: inline;
  margin: auto;
  height: 75%;
  width: 100%;
}

.carousel-3d-slide {
  border-style: none;
  background-color: rgba(0, 0, 0, .0001);
  text-align: center;
}

.a {
  border-bottom: none;
}

</style>
