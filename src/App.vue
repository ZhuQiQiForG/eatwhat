<template>
  <div id="app">
    <login></login>
    <div class="main-wrapper">
      <div class="top-wrapper">
        <div class="distance">
          <h1 class="title" @click.stop="distance">距离</h1>
          <div class="distanceSelecter" v-show="showDistance">
            <ul>
              <li class="range" v-for="(item, index) in distanceArr" @click="selectedDistance(index)">{{item.text}}米</li>
            </ul>
          </div>
        </div>
        <div class="price" @click.stop="choose">去哪</div>
      </div>
      <div class="eatwhat-wrapper">
        <BMap ref="BMap"></BMap>
      </div>
      <v-footer></v-footer>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import login from './components/login/login';
  import footer from './components/footer/footer';
  import BMap from './components/BMap/BMap';

  export default {
    components: {
      login,
      'v-footer': footer,
      BMap
    },
    data() {
      return {
        distanceArr: [
          {text: '500'},
          {text: '1000'},
          {text: '2000'},
          {text: '5000'}
        ],
        showDistance: false,
        sd: 500
      };
    },
    methods: {
      distance(event) {
        this.showDistance = !this.showDistance;
      },
      selectedDistance(index) {
        this.sd = Number(this.distanceArr[index].text);
        this.showDistance = !this.showDistance;
        this.$refs.BMap.drawMap(this.sd);
      },
      choose() {
        this.$refs.BMap.drawMap(this.sd, true);
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .main-wrapper
    position: fixed
    top: 0
    left: 0
    width: 100%
    height: 100%
    .top-wrapper
      position: absolute
      display: flex
      left: 0
      top: 0
      height: 56px
      line-height: 56px
      width: 100%
      .distance, .price
        position: relative
        flex: 1
        text-align: center
      .distance
        border-right: 1px solid #dedede
        .title
          width: 100%
        .distanceSelecter
          position: absolute
          top: 56px
          left: 0
          width: 100%
          z-index: 100
          background: #dedede
          .range
            height: 30px
            line-height: 30px
            border-bottom: 1px solid #fff
            color: #fff
            &:last-child
              border-bottom: none
    .eatwhat-wrapper
      position: absolute
      top: 56px
      bottom: 50px
      width: 100%
</style>
