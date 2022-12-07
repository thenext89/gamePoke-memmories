<script>
import Card from "./Card.vue";
export default {
  name: "InteractScreen",
  components: {
    Card,
  },
  computed: {
    layout() {
      let layout;
      console.log(Math.sqrt(this.cardContext.length))
      switch (Math.sqrt(this.cardContext.length)) {
        case 4:
          layout = "layout-4";
          break;
        case 6:
          layout = "layout-6";
          break;
        case 8:
          layout = "layout-8";
          break;
        case 10:
          layout = "layout-10";
          break;
        default:
          layout = "layout-4";
          break;
      }
      return layout;
    },
  },
  data() {
    return {
      rules: [],
    };
  },
  props: {
    cardContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
  methods: {
    checkRules(card) {
      // console.log(card)
      // trường hợp click 3 thẻ 1 lúc thì không cho nhấn và set số thẻ đc chọn bằng 0
      // trường hợp mảng có nhiều hơn 2 phần tử thì return false
      if (this.rules.length === 2) {
        this.$refs[`card-${card.index}`][0].onFlipBackCard();
        return false;
      }
      // thêm thẻ vào trong mảng để kiểm tra dữ liệu
      this.rules.push(card);
      // kiểm tra giá trị của 2 thẻ có bằng nhau hay không, nếu bằng và khác index thì ngửa lên luôn
      if (
        this.rules.length == 2 &&
        this.rules[0].value == this.rules[1].value &&
        this.rules[0].index != this.rules[1].index
      ) {
        // add class disable
        this.$refs[`card-${this.rules[0].index}`][0].onEnableDisableMode();
        this.$refs[`card-${this.rules[1].index}`][0].onEnableDisableMode();
        this.rules = [];
        const disableElements = document.querySelectorAll(".card.disable");
        console.log(disableElements);
        if (
          disableElements &&
          disableElements.length === this.cardContext.length - 2
        ) {
          setTimeout(() => {
            console.log("xong");
            this.$emit("onFinish");
          }, 1000);
        }
      }
      // giá trị bằng nhưng trùng index thì reset lại mảng và count đồng thời push lại giá trị
      else if (
        this.rules.length == 2 &&
        this.rules[0].value == this.rules[1].value &&
        this.rules[0].index == this.rules[1].index
      ) {
        this.rules = []
        this.rules.push(card);
      }
      // trường hợp 2 thẻ khác dữ liệu thì úp lại 2 thẻ
      else if (
        this.rules.length == 2 &&
        this.rules[0].value != this.rules[1].value
      ) {
        // close card and reset rules
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 1000);
      } else return false;
    },
  },
};
</script>
<template>
  <div class="scre" :class="layout">
    <card
      v-for="(card, index) in cardContext"
      :key="index"
      :ref="`card-${index}`"
      :imgBackFaceUrl="`${card}.png`"
      :card="{ index: index, value: card }"
      @onFlip="checkRules($event)"
    />
  </div>
</template>
<style scoped lang="css">
.scre {
  margin: 0 auto;
  width: 1200px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.card {
  margin: 0;
  padding: 10px;
}
.scre.layout-4{
  width: 640px;
}
.scre.layout-4 .card{
  flex:0 0 25%;
  height:200px;
}
.scre.layout-6 .card{
  flex:0 0 16.65%;
  height:240px;
}

.scre.layout-8 .card{
  flex:0 0 12.5%;
  height:180px;
}
.scre.layout-10 .card{
  flex:0 0 10%;
  height:140px;
}
</style>
