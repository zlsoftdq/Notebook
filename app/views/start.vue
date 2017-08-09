<style scoped>
  textarea {
    flex: 1;
    margin-bottom: 10px;
  }
</style>

<template>
  <div class="inner">
    <h1 class="page-header drag">{{$t('sidebar.actions.start')}}</h1>
    <textarea cols="80" rows="10" v-model="content"></textarea>
    <button class="btn btn-primary btn-lg btn-block" @click="save()">{{$t('sidebar.actions.start')}}</button>
  </div>
</template>

<script>
  export default {
    name: 'start',
    pathname: '/start',

    data () {
      this.$root.title = ''
      return { content: '' }
    },

    methods: {
      save () {
        if (!this.content) {
          return this.$dialog.error('笔记内容太少了，请再丰富一点吧!')
        }
        const stamp = this.$utils.getFilename()
        this.$storage.set(stamp, { content: this.content })
        this.$router.go({ name: 'watch', params: { item: stamp } })
      }
    }
  }
</script>
