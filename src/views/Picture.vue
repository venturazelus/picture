<template>
  <div>

    <base-header class="pb-6 pb-8 pt-5 pt-md-8 bg-gradient-success">
      <!-- Card stats -->
      <b-row>
        <b-col xl="3" md="6">
          <stats-card title="Total traffic"
                      type="gradient-red"
                      sub-title="350,897"
                      icon="ni ni-active-40"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">3.48%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Total traffic"
                      type="gradient-orange"
                      sub-title="2,356"
                      icon="ni ni-chart-pie-35"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">12.18%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Sales"
                      type="gradient-green"
                      sub-title="924"
                      icon="ni ni-money-coins"
                      class="mb-4">

            <template slot="footer">
              <span class="text-danger mr-2">5.72%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>

        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Performance"
                      type="gradient-info"
                      sub-title="49,65%"
                      icon="ni ni-chart-bar-32"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">54.8%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
      </b-row>
    </base-header>

    <b-carousel 
      id="carousel-1"
      class="m-5"
      v-model="slide"
      :interval="5000"
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 10px 10px 20px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=52" >
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=54">
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=58">
      </b-carousel-slide>

      <b-carousel-slide>
        <template #img>
          <img
            class="d-block img-fluid w-100"
            width="1024"
            height="480"
            src="https://picsum.photos/1024/480/?image=55"
            alt="image slot"
          >
        </template>
     </b-carousel-slide>

      <b-carousel-slide caption="Blank Image" img-blank img-alt="Blank image">
        <p> Just a Blank Image </p>
      </b-carousel-slide>
    </b-carousel>

    <b-row>
    <b-col>
    <b-carousel
      id="carousel-2"
      class = "ml-5"
      controls
      :interval="10000000000000000"
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
    >
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=40">
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=44">
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=48">
      </b-carousel-slide>

      <b-carousel-slide>
        <template #img>
          <img
            class="d-block img-fluid w-100"
            width="1024"
            height="480"
            src="https://picsum.photos/1024/480/?image=45"
            alt="image slot"
          >
        </template>
      </b-carousel-slide>

      <b-carousel-slide caption="Blank Image" img-blank img-alt="Blank image">
        <b> Nothing Here </b>
      </b-carousel-slide>
    </b-carousel>
    </b-col>

    <b-col>
    <b-carousel
      id="carousel-3"
      class = "mr-5"
      indicators
      :interval="10000000000000000"
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
    >
      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=32">
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=34">
      </b-carousel-slide>

      <b-carousel-slide img-src="https://picsum.photos/1024/480/?image=38">
      </b-carousel-slide>

      <b-carousel-slide>
        <template #img>
          <img
            class="d-block img-fluid w-100"
            width="1024"
            height="480"
            src="https://picsum.photos/1024/480/?image=35"
            alt="image slot"
          >
        </template>
      </b-carousel-slide>

      <b-carousel-slide caption="Blank Image" img-blank img-alt="Blank image">
        <b>Lorem ipsum dolor sit amet</b>
      </b-carousel-slide>
    </b-carousel>
    </b-col>
    </b-row>
    
  </div>
</template>

<script>
  export default {
    data() {
      return {
        slide: 0,
        sliding: null
      }
    },
    methods: {
      onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      }
    }
  }
</script>
