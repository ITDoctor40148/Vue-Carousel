<template>
  <div class="carousel-container">
    <transition-group name="fade" tag="div">
      <div v-for="i in [currentIndex]" :key="i">
        <div>
          <img :src="currentImg" class="item" />
          <div class="title">
            <h1>{{ titles[i] }}</h1>
            <h2>{{ subTitles[i] }}</h2>
            <p>{{ content[i] }}</p>
          </div>
        </div>
      </div>
    </transition-group>
    <a class="prev" @click="prev" href="#">&#10094;</a>
    <a class="next" @click="next" href="#">&#10095;</a>

    <ol class="carousel-indicators">
      <li
        v-for="i in totalImg"
        :key="i"
        data-target="#banner_slider"
        :data-slide-to="i"
        :class="{ active: currentIndex === i - 1 }"
        @click="setCustomIndex(i)"
      ></li>
    </ol>
  </div>
</template>
<script>
export default {
  name: "Carousel",
  data() {
    return {
      images: [
        "https://cdn.pixabay.com/photo/2015/12/12/15/24/amsterdam-1089646_1280.jpg",
        "https://cdn.pixabay.com/photo/2016/02/17/23/03/usa-1206240_1280.jpg",
        "https://cdn.pixabay.com/photo/2015/05/15/14/27/eiffel-tower-768501_1280.jpg",
        "https://cdn.pixabay.com/photo/2016/12/04/19/30/berlin-cathedral-1882397_1280.jpg"
      ],
      titles: ["Title1", "Title2", "Title3", "Title4"],
      subTitles: ["SubTitle1", "SubTitle2", "SubTitle3", "SubTitle4"],
      content: ["Content1", "Content2", "Content3", "Content4"],
      timer: null,
      currentIndex: 0
    };
  },

  mounted: function() {
    // this.startSlide();
  },

  methods: {
    startSlide: function() {
      this.timer = setInterval(this.next, 4000);
    },

    next: function() {
      this.currentIndex += 1;
      if (this.currentIndex >= this.totalImg) {
        this.currentIndex -= this.totalImg;
      }
    },
    prev: function() {
      this.currentIndex -= 1;
      if (this.currentIndex < 0) {
        this.currentIndex += this.totalImg;
      }
    },

    setCustomIndex: function(i) {
      this.currentIndex = i - 1;
    }
  },

  computed: {
    currentImg: function() {
      return this.images[this.currentIndex];
    },
    totalImg: function() {
      return this.images.length;
    }
  }
};
</script>

<style lang="css">
.title {
  z-index: 999;
  position: absolute;
  top: 150px;
  left: 250px;
}

.carousel-container {
  position: relative;
  height: 650px;
}

.active {
  background-color: rgb(255, 255, 255) !important;
  width: 24px !important;
  border-radius: 10px !important;
}

.item {
  border-radius: 50px;
}

.carousel-indicators {
  display: flex;
  right: auto;
  bottom: 100px;
  left: 60px;
  padding-left: 0;
  position: absolute;
  list-style: none;
  margin-right: 0;
  margin-left: 0;
  z-index: 15;
}

.carousel-indicators li {
  border-radius: 100%;
  position: relative;
  -ms-flex: 0 1 auto;
  -webkit-box-flex: 0;
  flex: 0 1 auto;
  width: 12px;
  height: 12px;
  margin-right: 5px;
  margin-left: 5px;
  text-indent: -999px;
  cursor: pointer;
  background-color: rgba(255, 255, 255, 0.5);
}

.fade-enter-active,
.fade-leave-active {
  transition: all 0.9s ease;
  overflow: hidden;
  visibility: visible;
  position: absolute;
  width: 100%;
  opacity: 1;
}

.fade-enter,
.fade-leave-to {
  visibility: hidden;
  width: 100%;
  opacity: 0;
}

img {
  height: 600px;
  width: 100%;
}

.prev,
.next {
  cursor: pointer;
  position: absolute;
  top: 40%;
  width: 58px;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 44px;
  transition: 0.7s ease;
  border-radius: 50%;
  text-decoration: none;
  user-select: none;
}

.next {
  right: 10px;
}

.prev {
  left: 10px;
}

.prev:hover,
.next:hover {
  background-color: rgba(0, 0, 0, 0.9);
}
</style>
