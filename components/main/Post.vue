<template>
    <el-card
      shadow="hover"
      :body-style="{padding:0}"
      class="post"
    >
      <header slot="header" class="post-header">
        <h3>Post title</h3>
        <small>
          <i class="el-icon-time"></i>
          {{ new Date().toLocaleString() }}
        </small>
      </header>
      <div class="post-body">
        <img
          src="https://www.flytap.com/-/media/Flytap/new-tap-pages/destinations/europe/russia/moscow/destinations-moscow-banner-mobile-1024x553.jpg"
          alt="post-img"
          class="post-img">
      </div>
      <footer class="post-footer">
        <el-button round @click="openPost">Открыть</el-button>

        <span>
          <i class="el-icon-message">12</i>
        </span>
      </footer>
    </el-card>
</template>

<script>
export default {
  methods: {
    openPost() {
      const id = 'test-id'
      this.$router.push(`/post/${id}`)
      console.log('openPost')
    }
  }
}
</script>

<style lang="scss" scoped>
.post {
  margin-bottom: 1.5rem;
}

.post-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.post-img {
  width: 100%;
  height: auto;
}

.post-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem;
}
</style>
