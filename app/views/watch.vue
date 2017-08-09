<style scoped>
  textarea {
    flex: 1;
    margin-bottom: 10px;
  }
</style>

<template>
  <div class="inner">
    <h1 class="page-header drag" v-show="!display">{{$t('watch.title')}}</h1>
    <textarea cols="80" rows="10" v-model="item.content" @keyup="displayBtn()" @change="displayBtn()" @mousedown="displayBtn()"></textarea>
    <button class="btn btn-primary btn-lg btn-block"  v-show="display" @click="saveModify()">{{$t('watch.save')}}</button>
  </div>
</template>

<script>
  export default {
    name: 'watch',
    pathname: '/watch/:item',

    data () {
      return { display: false, item: {} }
    },

    route: {
      data (transition) {
        const stamp = transition.to.params.item
        this.loadData(stamp)
        this.$storage.watch(stamp, () => this.loadData(stamp))
      }
    },

    methods: {
      loadData (stamp) {
        if (!stamp) return this.$router.go({ name: 'start' })
        const item = this.$storage.get(stamp)
        if (!item) return this.$router.go({ name: 'start' })
        this.item = item
        this.$root.title = stamp
        return this.item
      },
      displayBtn () {
        this.display = true
      },
      saveModify () {
        if (!this.item.content) {
          return this.$dialog.error('笔记内容太少了，请再丰富一点吧!')
        }
        const stamp = this.$root.title
        this.$storage.set(stamp, { content: this.item.content })
        this.display = false
        // this.$router.go({ name: 'watch', params: { item: stamp } })
      }
    }
  }
</script>
