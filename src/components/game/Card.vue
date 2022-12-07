<script>
export default {
  data() {
    return {
      isDisable: false,
      isFlipped: false,
    };
  },
  methods: {
    onToggelFlipCard() {
      if (this.isDisable) return false;
      this.isFlipped = !this.isFlipped;
      if (this.isFlipped) {
        this.$emit("onFlip", this.card);
      }
    },
    onFlipBackCard() {
      this.isFlipped = false;
    },
    onEnableDisableMode() {
      this.isDisable = true;
    },
  },
  props: {
    imgBackFaceUrl: {
      type: String,
      required: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
  },
};
</script>
<template>
  <div class="card" :class="{ disable: isDisable }">
    <div
      class="card_inner"
      :class="{ is_flip: isFlipped }"
      @click="onToggelFlipCard"
    >
      <div class="card_face card_face-front">
        <div class="card_content"></div>
      </div>
      <div class="card_face card_face-back">
        <div
          class="card_content"
          :style="{ backgroundImage: `url('/images/${imgBackFaceUrl}')` }"
        ></div>
      </div>
    </div>
  </div>
</template>
<style scoped lang="css">
.card {
  display: flex;
  margin: 0 1rem 1rem 0;
  width: 90px;
  height: 120px;
}
.card_inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 1s ease;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card.disable .card_inner {
  cursor: default;
}
.card_inner.is_flip {
  transform: rotateY(-180deg);
}
.card_face {
  position: absolute;
  width: 100%;
  height: 100%;
  font-size: 1.6rem;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  box-shadow: 3px 3px 5px rgba(255 255 255 /0.2);
}
.card_face-front .card_content {
  background-image: url(/images/icon_back.png);
  background-size: 40px 40px;
  background-color: rgb(145, 119, 119);
}
.card_content {
  background-repeat: no-repeat;
  background-position: center center;
  height: 100%;
  width: 100%;
}
.card_face-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card_face-back .card_content {
  background-size: 100% auto;
}
</style>
