<template>
  <div>
    <Header />
    <Container />
    <Footer />
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Container from '@/components/Container.vue'
import Footer from '@/components/Footer.vue'

export default {
  name: 'Home',
  components: {
    Header,
    Container,
    Footer
  }
}
</script>
