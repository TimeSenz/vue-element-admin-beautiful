<template>
  <transition :name="transitionName">
    <div
      v-show="visible"
      :style="customStyle"
      class="back-to-ceiling"
      @click="backToTop"
    >
      <byui-icon :icon="['fas', 'eject']" />
    </div>
  </transition>
</template>

<script>
export default {
  name: "ByuiBackToTop",
  props: {
    visibilityHeight: {
      type: Number,
      default: 400,
    },
    backPosition: {
      type: Number,
      default: 0,
    },
    customStyle: {
      type: Object,
      default: function () {
        return {
          background: "#fff",
          color: "#1890ff",
          right: "25px",
          bottom: "75px",
          width: "50px",
          height: "50px",
          paddingTop: "15px",
          borderRadius: "99px",
          boxShadow: "0 1px 4px rgba(0, 21, 41, 0.08)",
        };
      },
    },
    transitionName: {
      type: String,
      default: "fade",
    },
  },
  data() {
    return {
      visible: false,
      interval: null,
      isMoving: false,
    };
  },
  watch: {
    $route() {
      this.destroy();
      this.init();
    },
  },
  mounted() {
    this.init();
  },
  beforeDestroy() {
    this.destroy();
  },
  methods: {
    init() {
      window.addEventListener("scroll", this.handleScroll);
    },
    destroy() {
      window.removeEventListener("scroll", this.handleScroll);
      if (this.interval) {
        clearInterval(this.interval);
      }
    },
    handleScroll() {
      this.visible = window.pageYOffset > this.visibilityHeight;
    },
    backToTop() {
      if (this.isMoving) return;
      //   横向
      const start = window.pageYOffset;
      let i = 0;
      this.isMoving = true;
      this.interval = setInterval(() => {
        const next = Math.floor(this.easeInOutQuad(10 * i, start, -start, 500));
        if (next <= this.backPosition) {
          window.scrollTo(0, this.backPosition);
          clearInterval(this.interval);
          this.isMoving = false;
        } else {
          window.scrollTo(0, next);
        }
        i++;
      }, 16.7);
    },
    easeInOutQuad(t, b, c, d) {
      if ((t /= d / 2) < 1) return (c / 2) * t * t + b;
      return (-c / 2) * (--t * (t - 2) - 1) + b;
    },
  },
};
</script>

<style scoped>
.back-to-ceiling {
  position: fixed;
  display: inline-block;
  text-align: center;
  cursor: pointer;
  z-index: 99;
}

.back-to-ceiling:hover {
  background: #d5dbe7;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}

.back-to-ceiling .Icon {
  fill: #9aaabf;
  background: none;
}
</style>
