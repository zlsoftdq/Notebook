<style lang="less" scoped>
  .inner {
    align-items: center;
    justify-content: center;
  }
  img {
    margin-top: -25px;
    width: 400px;
    transition: transform 1s ease;
    transform-origin: 50px 50px;

    &.rotate {
      transform: rotate(700deg);
    }
  }
  p {
    line-height: 16px;
    code {
      background-color: rgba(40, 56, 76, .5);
      border-radius: 3px;
      color: #fff;
      font-weight: bold;
      padding: 3px 6px;
      margin: 0 3px;
      vertical-align: bottom;
    }
  }
  a {
    color: rgb(50, 174, 110);
    text-decoration: none;
    &:hover { color: rgb(40, 56, 76); }
  }
  ul {
    list-style-type: none;
    margin-top: 10px;
    padding: 0;
    li {
      display: inline-block;
    }
    li + li::before {
      content: '|';
      padding: 6px;
      color: #ccc;
    }
  }
</style>

<template>
  <div class="inner">
    <img src="../assets/img/logo.png" alt="electron-vue" :class="{rotate: rotate}" @click="eggshell()">
    <h1>{{$t('about.appname')}}</h1>
    <p>{{$t('about.appdescription')}}</p>
    <p>{{$t('dashboard.copyright')}}</p>
  </div>
</template>

<script>
  import os from 'os'

  export default {
    name: 'dashboard',
    pathname: '/',

    data () {
      this.$root.title = ''
      return {
        platform: os.platform(),
        versions: process.versions,
        click: 0,
        rotate: false
      }
    },

    methods: {
      eggshell () {
        if (!this.click) {
          setTimeout(() => {
            if (this.click > 6) {
              this.rotate = !this.rotate
              alert(`手速：${this.click}/1000ms`)
            }
            this.click = 0
          }, 1000)
        }
        this.click++
      }
    }
  }
</script>
