<template>
  <div class="carousel-container">
    <b-container>
      <b-row>
        <transition-group name="fade" tag="div">
          <div v-for="i in [currentIndex]" :key="i">
            <div style="position: relative;">
              <img :src="currentImg" class="item" height="475" />
              <div class="title">
                <p class="title--1">{{ titles[i] }}</p>
                <h1 class="title--2">{{ subTitles[i] }}</h1>
                <p class="title--3">{{ content[i] }}</p>
                <a class="btn white_btn button_large">Button</a>
              </div>
            </div>
          </div>
        </transition-group>
        <a class="cprev" @click="prev" href="#">&#10094;</a>
        <a class="cnext" @click="next" href="#">&#10095;</a>

        <ol class="carousel-indicators1">
          <li
            v-for="i in totalImg"
            :key="i"
            data-target="#banner_slider"
            :data-slide-to="i"
            :class="{ active: currentIndex === i - 1 }"
            @click="setCustomIndex(i)"
          ></li>
        </ol>
      </b-row>
    </b-container>
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
    this.startSlide();
  },

  methods: {
    startSlide: function() {
      this.timer = setInterval(this.next, 3000);
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
.btn {
  -webkit-border-radius: 3px;
  border-radius: 3px;
  padding: 10px 25px;
  font-family: "Nunito", sans-serif;
  font-weight: 600;
  font-style: normal;
  font-size: 14px;
  line-height: 19px;
  letter-spacing: 0.03em;
  border: 0;
  position: relative;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.btn:not(:disabled):not(.disabled) {
  cursor: pointer;
}
.btn.button_large {
  height: 50px;
  padding: 15px 25px;
}
.btn.white_btn {
  background-color: #fafafb;
  color: #283441;
}
.title {
  z-index: 999;
  position: absolute;
  top: 50%;
  left: 60px;
  transform: translateY(-50%);
}

.title--1 {
  background-color: pink;
  height: 30px;
  width: 80px;
  border-radius: 5px;
}

.title--2,
.title--3 {
  color: white;
}

.title--3 {
  text-align: left;
}

.carousel-container {
  position: relative;
  height: 475px;
}

.active {
  background-color: rgb(255, 255, 255) !important;
  width: 24px !important;
  border-radius: 10px !important;
}

.item {
  border-radius: 50px;
  height: 475px;
}

.carousel-indicators1 {
  display: flex;
  right: auto;
  bottom: 60px;
  left: 20%;
  padding-left: 0;
  position: absolute;
  list-style: none;
  margin-right: 0;
  margin-left: 0;
  z-index: 15;
}

.carousel-indicators1 li {
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
  animation: fadeIn ease 1.5s;
  overflow: hidden;
  position: relative;
  width: 100%;
  opacity: 1;
}

.fade-enter,
.fade-leave-to {
  animation: fadeOut ease 1.5s;
  display: none;
  width: 100%;
  opacity: 0;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes fadeOut {
  0% {
    opacity: 1;
  }
  100% {
    opacity: 0;
  }
}

img {
  height: 600px;
  width: 100%;
}

.cprev,
.cnext {
  cursor: pointer;
  position: absolute;
  top: 40%;
  width: 90px;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 44px;
  transition: 0.7s ease;
  border-radius: 50%;
  text-decoration: none;
  user-select: none;
}

.cnext {
  right: 10px;
}

.cprev {
  left: 10px;
}

.cprev:hover,
.cnext:hover {
  background-color: rgba(0, 0, 0, 0.9);
}
</style>
