<template>
  <div class="container column">
    <resume-form @block-added="addBlock"></resume-form>
    <resume-view :blocks="blocks"></resume-view>
  </div>
  <div class="container">
    <app-loader v-if="loading"></app-loader>
    <resume-comments v-else :comments="comments" @load-comments="loadComments"></resume-comments>
  </div>
</template>

<script>
import ResumeForm from './components/ResumeForm.vue';
import ResumeView from './components/ResumeView.vue';
import ResumeComments from './components/ResumeComments.vue';
import AppLoader from './components/AppLoader.vue';

export default {
  data() {
    return {
      blocks: [],
      loading: false,
      comments: []
    }
  },
  components: {
    ResumeForm,
    ResumeView,
    ResumeComments,
    AppLoader
  },
  methods: {
    async loadComments() {
      this.loading = true
      const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = await response.json()
      this.loading = false
    },
    addBlock(block) {
      this.blocks.push(block)
    }
  }
}
</script>

<style></style>
