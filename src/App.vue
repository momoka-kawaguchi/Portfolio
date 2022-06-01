<template>
  <transition name="fade" tag="div" class="wrapper" mode="out-in">
    <div class="wrapper" v-if="isLoaded" id="app">
      <LandingPage :user="user" />
      <Description :user="user" :content="findSlug('description')" :links="links" />
      <Experience :content="findSlug('experiences')" />
      <Projects :content="findSlug('projects')" />
      <Footer :user="user" :links="links" />
    </div>
  </transition>
</template>

<script>
import LandingPage from "./components/LandingPage.vue";
import Description from "./components/Description.vue";
import Experience from "./components/Experience.vue";
import Projects from "./components/Projects.vue";
import Footer from "./components/Footer.vue";

import { bucket } from "./cosmic.js";

export default {
  name: "App",
  components: {
    LandingPage,
    Description,
    Experience,
    Projects,
    Footer,
  },
  data: () => ({
    isLoaded: false,
    user: {},
    posts: [],
    links: {
      metadata: {
        facebook: 'https://facebook.com/momochan36',
        github: 'https://github.com/momoka-kawaguchi',
        linkedin: 'https://www.linkedin.com/in/momoka-kawaguchi',
        instagram: 'https://www.instagram.com/momochan36'
      }
    }
  }),
  methods: {
    fetchPosts() {
      return bucket.getObjects({
        type: "portfolio-contents",
        props: "slug,title,metadata",
      });
    },
    fetchUser() {
      return bucket.getObjects({
        type: "portfolio-contents",
        q: "user-data",
        props: "slug,title,metadata",
      });
    },
    fetchObjectTypes() {
      return bucket.getObjectTypes();
    },
    findSlug(slug) {
      return this.posts.find((item) => {
        return item.slug === slug;
      });
    },
    extractFirstObject(objects) {
      if(objects.objects == null)
        return void 0;
      else
        return objects.objects[0];
    }
  },
  created() {
    document.body.classList.add("loading");
    Promise.all([this.fetchPosts(), this.fetchUser()]).then(([posts, user_data]) => {
      user_data = this.extractFirstObject(user_data);
      this.posts = posts.objects;
      this.user = {
        name: 'Momo-blog',
        status:'Welcome to my page!!',
        email: 'momojazz36@gmail.com',
        phone: '080-1225-5890',
        city: 'Yachiyo,Chiba',
        lang: 'Japanese',
        photo: user_data.metadata.photo,
      }
      this.isLoaded = true;
      this.$nextTick(() => document.body.classList.remove("loading"));
    });
  },
};
</script>

<style scoped lang="scss">
@import "@/styles/constants.scss";

#app {
  font-family: Montserrat-Regular, serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.wrapper {
  height: 100%;
}
</style>
