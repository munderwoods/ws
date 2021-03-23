<template>
  <div
    class="image-carousel"
    @click.stop="handleClose"
    @keyup.esc="handleClose"
  >
    <div
      class="image"
      :style="{ backgroundImage: `url(${this.images[this.imageNumber].href})` }"
    >
      <img
        class="tool close"
        @click.stop="handleClose"
        alt="close"
        src="../assets/close.svg"
      />
      <img
        class="tool previous"
        @click.stop="handlePrevious"
        alt="previous"
        src="../assets/previous.svg"
      />
      <img
        class="tool next"
        @click.stop="handleNext"
        alt="next"
        src="../assets/next.svg"
      />
      <div class="dots">
        <div
          class="dot-wrapper"
          v-for="(image, x) in this.images"
          :key="x + 'circle'"
          @click.stop="handleSelectImage(x)"
        >
          <img
            v-if="x === imageNumber"
            class="circle"
            alt="circle"
            :key="x + 'circle'"
            src="../assets/dot.svg"
          />
          <img
            v-else
            class="circle"
            alt="circle"
            :key="x + 'circle'"
            src="../assets/circle.svg"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageCarousel",
  props: {
    images: Array
  },
  data() {
    return {
      imageNumber: 0
    };
  },
  methods: {
    handleClose: function() {
      this.$emit("close");
    },
    handleNext: function() {
      if (this.imageNumber < this.images.length - 1) {
        this.imageNumber++;
      } else {
        this.imageNumber = 0;
      }
    },
    handleSelectImage: function(imageNumber) {
      this.imageNumber = imageNumber;
    },
    handlePrevious: function() {
      if (this.imageNumber === 0) {
        this.imageNumber = this.images.length - 1;
      } else {
        this.imageNumber--;
      }
    },
    getSource: function(x) {
      if (x === this.imageNumber) {
        return "../assets/dot.svg";
      } else {
        return "../assets/circle.svg";
      }
    }
  }
};
</script>

<style scoped>
.image-carousel {
  z-index: 2;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: rgba(0, 0, 0, 0.2);
  cursor: pointer;
}
.image {
  background-color: white;
  content: "";
  position: relative;
  width: 80%;
  height: 80%;
  background-position: center;
  background-size: contain;
  box-shadow: 0 10px 10px 0 rgba(0, 0, 0, 0.2), 0 1px 10px 0 rgba(0, 0, 0, 0.19);
  background-repeat: no-repeat;
  display: flex;
  flex-direction: column-reverse;
  border-radius: 4px;
  transition: all 0.3s;
}
.tool {
  position: absolute;
  padding: 20px;
  cursor: pointer;
}
.close {
  top: 8px;
  right: 8px;
  height: 50px;
  width: 50px;
}
.previous {
  top: 50%;
  left: 8px;
  height: 50px;
  width: 50px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50px;
}
.next {
  top: 50%;
  right: 8px;
  height: 50px;
  width: 50px;
  background: rgba(255, 255, 255, 0.5);
  border-radius: 50px;
}
.dots {
  display: flex;
  flex-direction: row;
  justify-content: center;
  background: rgba(255, 255, 255, 0.5);
}
.dot-wrapper {
  display: flex;
  transition: all 0.3s;
}
.circle {
  transition: all 0.3s;
  height: 24px;
  width: 24px;
}
</style>
