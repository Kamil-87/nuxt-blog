<template>
  <article class="post">
    <header class="post-header">
      <div class="post-title">
        <h1>Title</h1>
        <nuxt-link to="/">
          <i class="el-icon-back"></i>
        </nuxt-link>
      </div>

      <div class="post-info">
        <small>
          <i class="el-icon-time"></i>
          {{ new Date().toLocaleString() }}
        </small>
        <small>
          <i class="el-icon-view"></i>
          42
        </small>
      </div>
      <div class="post-image">
        <img
          src="https://www.flytap.com/-/media/Flytap/new-tap-pages/destinations/europe/russia/moscow/destinations-moscow-banner-mobile-1024x553.jpg"
          alt="post-img"
          class="post-img">
      </div>
    </header>
    <main class="post-content">
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consectetur, culpa doloremque ducimus eaque ex excepturi hic, illo optio pariatur possimus quos reprehenderit sequi totam! Possimus!</p>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consectetur, culpa doloremque ducimus eaque ex excepturi hic, illo optio pariatur possimus quos reprehenderit sequi totam! Possimus!</p>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consectetur, culpa doloremque ducimus eaque ex excepturi hic, illo optio pariatur possimus quos reprehenderit sequi totam! Possimus!</p>
    </main>
    <footer class="post-footer">
      <app-comment-form
        v-if="canAddComment"
        @created="createCommentHandler"
      />

      <div class="comments" v-if="false">
        <app-comment
          v-for="comment in 4"
          :key="comment"
          :comment="comment"
        />
      </div>

      <div v-else class="text-center">
        Комментариев нет
      </div>
    </footer>
  </article>
</template>

<script>
import AppComment from '@/components/main/Comment'
import AppCommentForm from '@/components/main/CommentForm'

export default {
  validate({params}) {
    return !!params.id
  },
  components: {
    AppComment, AppCommentForm
  },
  data() {
    return {
      canAddComment: true
    }

  },
  methods: {
    createCommentHandler() {
      this.canAddComment = false
    }
  }
}
</script>

<style lang="scss" scoped>
.post {
  max-width: 600px;
  margin: 0 auto;
}
.post-title {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}
.post-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: .5rem;
}
.post-image img {
  width: 100%;
  height: auto;
}

.post-header {
  margin-bottom: 1.5rem;
}

.post-content {
  margin-bottom: 2rem;
}
</style>
