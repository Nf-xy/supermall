<template>
 <div class="tab-bar-item" @click="itemClick">
   <div v-if="!isActive"><slot  name="item-icon"></slot></div>
   <div v-else><slot name="item-icon-active"></slot></div>

   <div :style="activeStyle"><slot name="item-text"></slot></div>
 </div>
  <!--<div class="tab-bar-item">-->
    <!--<img src="../../assets/img/home.jpg" alt="">-->
   <!--<div>首页</div>-->
  <!--</div>-->
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
              // isActive: true,

            }
        },
        computed: {
            isActive() {
              // /home -> item(/home) = true
              // /home -> item(/category) = false
              // /home -> item(/cart) = false
              // /home -> item(/profile) = false
              return this.$route.path.indexOf(this.path) !== -1
            },
            activeStyle() {
                return this.isActive ? {color: this.activeColor} : {}
            }
        },
        methods: {
            itemClick() {
              this.$router.replace(this.path)
            }
        }
    }
</script>

<style scoped>
  .tab-bar-item{
    flex: 1;
    text-align: center;
    height: 49px;
    font-size: 12px;
    margin-bottom: 3px;

  }
  .tab-bar-item img{
    width: 30px;
    height: 30px;
    margin-top: 3px;
    vertical-align: middle;
    margin-bottom: 2px;
  }
</style>
