<template>
  <el-form
    :model="controls"
    :rules="rules"
    ref="form"
    @submit.native.prevent="onSubmit"
  >

    <h2 class="mb1">Создать новый пост</h2>

    <el-form-item label="Введите название поста" prop="title">
      <el-input
        resize="none"
        :rows="10"
        v-model.trim="controls.title"
      />
    </el-form-item>

    <el-form-item label="Текст в формате .md или .html" prop="text">
      <el-input
        type="textarea"
        resize="none"
        :rows="10"
        v-model="controls.text"
      />
    </el-form-item>

    <el-button class="mb1" type="success" plain @click="previewDialog = true">
      Предпросмотр
    </el-button>

    <el-dialog title="Предпросмотр" :visible.sync="previewDialog">
      <div :key="controls.text">
        <vue-markdown>{{ controls.text }}</vue-markdown>
      </div>
    </el-dialog>

    <el-upload
      class="mb1"
      ref="upload"
      drag
      action="https://jsonplaceholder.typicode.com/posts/"
      :on-change="handleImageChange"
      :auto-upload="false"
    >
      <i class="el-icon-upload"></i>
      <div class="el-upload__text">Перетащите картинку <em>или выбирайте</em></div>
      <div class="el-upload__tip" slot="tip">файлы с расширением jpg/png</div>
    </el-upload>

    <el-form-item>
      <el-button
        type="primary"
        native-type="submit"
        round
        :loading="loading"
      >Создать пост
      </el-button>
    </el-form-item>
  </el-form>
</template>

<script>
export default {
  layout: 'admin',
  middleware: ['admin-auth'],
  data() {
    return {
      image: null,
      previewDialog: false,
      loading: false,
      controls: {
        title: '',
        text: ''
      },
      rules: {
        title: [
          {required: true, message: 'Поле название не должен быть пустым', trigger: 'blur'}
        ],
        text: [
          {required: true, message: 'Текст не должен быть пустым', trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    onSubmit() {
      this.$refs.form.validate(valid => {
        if (valid && this.image) {
          this.loading = true

          try {
            const formData = {
              title: this.controls.title,
              text: this.controls.text,
              image: this.image
            }

            this.$store.dispatch('post/create', formData)
            this.controls.title = ''
            this.controls.text = ''
            this.image = null
            this.$refs.upload.clearFiles()
            this.$message.success('Пост создан')
          } catch (e) {
          } finally {
            this.loading = false
          }
        } else {
          this.$message.warning('Форма не валидна')
        }
      })

    },
    handleImageChange(file, fileList) {
      this.image = file.raw
    }
  }
}
</script>

<style lang="scss" scoped>
form {
  width: 600px;
}
</style>
