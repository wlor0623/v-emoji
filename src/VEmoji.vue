<template>
  <div class="emoji-keyboard">
    <div class="tab scroll">
      <div class="main scroll">
        <div
          class="tab-item"
          v-for="(item, index) in emoji"
          :key="index"
          :style="{ color: tabIndex === index ? color : '#666','background-color': tabIndex === index ?'#fff':'' }"
          @click.stop="toogleTabIndex(index)"
        >
          {{ item.title }}1
        </div>
      </div>
    </div>
    <div class="content" ref="emojiContent">
      <div
        class="flex-cell"
        v-for="(item, index) in emoji[tabIndex].list"
        :key="index"
        @click="selectIcon(item)"
      >
        <div class="icon">
          {{ item.key }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import emoji from "./emoji.js";
export default {
  components: {},
  data() {
    return {
      tabIndex: 0,
    };
  },
  created() {},
  props: {
    color: {
      default: "#2e98d4",
      type: String,
    },
  },
  mounted() {},
  computed: {
    emoji: () => {
      return emoji;
    },
  },
  methods: {
    toogleTabIndex(index) {
      this.tabIndex = index;
      this.scrollToTop(this.$refs["emojiContent"], 200);
    },
    scrollToTop(element, duration) {
      if (element.scrollTop === 0) return;
      const totalScrollDistance = element.scrollTop;
      let scrollY = totalScrollDistance,
        oldTimestamp = null;
      function step(newTimestamp) {
        if (oldTimestamp !== null) {
          scrollY -=
            (totalScrollDistance * (newTimestamp - oldTimestamp)) / duration;
          if (scrollY <= 0) return (element.scrollTop = 0);
          element.scrollTop = scrollY;
        }
        oldTimestamp = newTimestamp;
        window.requestAnimationFrame(step);
      }
      window.requestAnimationFrame(step);
    },
    selectIcon(item) {
      this.$emit("select", item.key);
    },
  },
};
</script>

<style lang="less" scoped>
.scroll::-webkit-scrollbar {
  display: none;
}
.emoji-keyboard {
  background-color: #e7e8e9;
  .tab {
    width: 100%;
    overflow-x: scroll;
    -webkit-overflow-scrolling: touch;
    .main {
      box-sizing: border-box;
      display: flex;
      align-items: center;
      flex-wrap: nowrap;
      height: 40px;

      .tab-item {
        height: 30px;
        border-radius: 3px;
        flex: 0 0 20%;
        font-size: 14px;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        transition: all 0.2s;
        &.active {
          background-color: #fff;
        }
      }
    }
  }
  .content {
    display: flex;
    flex-wrap: wrap;
    height: 260px;
    padding: 15px 10px;
    overflow-y: scroll;
    -webkit-overflow-scrolling: touch;
    background-color: #fff;
    .flex-cell {
      flex: 0 0 12.5%;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 35px;
      margin-bottom: 5px;
      .icon {
        font-size: 24px;
      }
    }
  }
}
</style>
