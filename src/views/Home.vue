<template>
  <div>
    <Header :step="step"
      @go-to-home="handleGoToHome"
      @next-step="step++"
      @share-post="handleSharePost"
    />
    <Container :step="step"
      :posts="posts"
      :filters="filters"
      :image="image"
      v-model="caption"
      @selected-filter="handleSelectedFilter"
    />
    <Footer :step="step"
      @go-to-home="handleGoToHome"
      @upload-image="handleUploadImage"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Container from '@/components/Container.vue'
import Footer from '@/components/Footer.vue'
import posts from '@/data/posts'
import filters from '@/data/filters'
import userImage from '@/data/userImage'

export default {
  name: 'Home',
  data () {
    return {
      posts,
      filters,
      caption: '',
      image: '',
      step: 1
    }
  },
  components: {
    Header,
    Container,
    Footer
  },
  methods: {
    handleGoToHome () {
      this.caption = ''
      this.image = ''
      this.step = 1
    },
    handleSharePost () {
      const post = {
        username: 'VueVixens',
        userImage: userImage.data,
        postImage: this.image,
        likes: 0,
        caption: this.caption,
        filter: this.filterType
      }
      this.posts.unshift(post)
      this.handleGoToHome()
    },
    handleUploadImage (ev) {
      const files = ev.target.files
      if (!files.length) return

      const reader = new FileReader()
      reader.readAsDataURL(files[0])
      reader.onload = ev => {
        this.image = ev.target.result
        this.step = 2
      }
      document.querySelector('#file').value = ''
    },
    handleSelectedFilter (ev) {
      this.filterType = ev.filter
    }
  }
}
</script>
