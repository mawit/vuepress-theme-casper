<template>
  <nav class="site-nav" style="overflow: visible;" :class="siteNavFixed">
    <div class="site-nav-left-wrapper" style="height: 100%">
      <div class="site-nav-left" style="margin-top: auto;">
        <router-link v-if="!isHome && blog.logo" class="site-nav-logo" to="/">
          <img :src="$withBase(blog.logo)" :alt="blog.title" />
        </router-link>
        <router-link v-if="!isHome && !blog.logo" class="site-nav-logo" to="/">
          {{ blog.title }}
        </router-link>
        <div class="site-nav-content">
          <ul class="nav" v-if="nav" role="menu">
            <li v-for="(item, index) in nav" role="menuitem" :key="index">
              <router-link :class="{ active: item.active }" :to="item.link">{{
                item.text
              }}</router-link>
            </li>
          </ul>
          <span class="nav-post-title" v-if="isPost">{{ current.title }}</span>
        </div>
      </div>
    </div>
    <div class="site-nav-right">
      <SearchBox v-if="blog.search" />
      <div class="social-links">
        <social-link
          v-for="(channel, index) in social"
          :url="channel.url"
          :type="channel.type"
          :key="index"
        />
      </div>
    </div>
  </nav>
</template>

<script>
import { mapGetters } from "vuex";

import SocialLink from "./SocialLink";
import SearchBox from '@SearchBox'

export default {
  props: {
    'siteNavFixed': String
  },
  components: { SocialLink, SearchBox },
  computed: {
    ...mapGetters(["blog", "type", "social", "nav", "current"]),
    isHome() {
      return this.type === "home";
    },
    isPost() {
      return this.type === "post";
    }
  }
};
</script>
