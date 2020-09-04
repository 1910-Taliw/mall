<template>
  <!--所有的item都展示同一个图片，同一个文字-->
  <div class="tab-bar-item" @click="itemClick">
    <slot v-if="!isActive" name="item-icon"></slot>
    <slot v-else name="item-icon-active"></slot>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: "TabBarItem",
    props: {
      path: String,
      activeColor: {
        type: String,
        default: 'red'
      }
    },
    data() {
      return {
        // isActive: true
      }
    },
    computed: {
      isActive() {
        return this.$route.path.indexOf(this.path) != -1//判断当前活跃的路由是否包含相对应的路径
      },
      activeStyle() {
        return this.isActive ? {color: this.activeColor} : {}//当前路由是否活跃，是的话就使用当前路由给定的color样式，不是就返回空对象
      }
    },
    methods: {
      itemClick() {
        this.$router.replace(this.path)//点击事件的监听
      }
    }
  }
</script>

<style scoped>
  .tab-bar-item {
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 14px;
  }

  .tab-bar-item img{
    width: 28px;
    height: 28px;
    margin-top: 3px;
    vertical-align: middle;
  }


</style>
