<template>
  <footer class="site-footer outer">
    <div class="site-footer-content inner">
      <section class="copyright"><a :href="$withBase('/')">{{ blog.title }}</a> &copy; {{ year }}</section>
      <nav class="site-footer-nav">
        <a v-for="(item, index) in footer"
          :key="index"
          :href="item.external ? item.link : $withBase(item.link)"
          :target="item.external ? '_blank' : '_top'"
          rel="noopener"
        >{{ item.text }}</a>
      </nav>
      <div class="social-links">
        <social-link
          v-for="(channel, index) in social"
          :url="channel.url"
          :type="channel.type"
          :key="index"
        />
      </div>
    </div>
  </footer>

</template>

<script>
  import { mapGetters } from 'vuex'

  import SocialLink from "./SocialLink";

  export default {
    components: { SocialLink },
    computed: {
      ...mapGetters(['blog', 'footer', 'social']),
      year () {
        return new Date().getFullYear()
      }
    }
  }
</script>
