<template>
  <!-- <ul class="columns is-multiline">
    <li class="project column is-half" v-for="(p, i) in projects" :key="p.id">
      <a @click="goToProject(p.id)">
        <div>
          <img-wrapper :src="p.thumb"></img-wrapper>
        </div>
        <div class="content">
          <strong>
            {{p.title}}
          </strong>
          <span class="short-desc">{{p.shortDesc}} </span>
        </div>
      </a>
    </li>
  </ul> -->
  <div>
    <ul class="columns is-multiline">
      <li
        v-for="(p, i) in projects"
        :key="p.id"
        class="column is-one-third project"
      >
        <a @click="goToProject(p.id)">
          <img-wrapper :src="p.thumb"></img-wrapper>
          <div class="content">
            <p>
              <strong>{{ p.title }}</strong>
              <span class="short-desc" v-html="p.shortDesc"></span>
              <!-- <span>→</span> -->
              <!-- <span class="icon">
                <i class="fa fa-arrow-right"></i>
              </span> -->
            </p>
            <div class="tags">
              <span v-for="role in p.roles" class="tag">{{ role }}</span>
            </div>
          </div>
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
import ImgWrapper from '~/components/ImgWrapper'

export default {
  components: {
    ImgWrapper,
  },
  props: ['projects'],
  methods: {
    goToProject(projectId) {
      const webLink = this.projects.find((p) => p.id === projectId).link
      if (webLink) return window.open(webLink)
      const screen = document.getElementById('screen')
      screen.classList.add('is-transition')
      screen.classList.remove('pulled-up')
      setTimeout(() => {
        this.$router.push(`/projects/${projectId}`)
      }, 600)
    },
  },
}
</script>

<style lang="scss" scoped>
.project {
  font-size: 0.9em;
  margin-bottom: 3rem;
  .columns {
    // align-items: center;
    transition: all 300ms;
  }
  .short-desc {
    color: #4a4a4a;
    margin-top: 20px;
    &::after {
      // font: normal 16px StripeIcons;
      content: '\2192';
      padding-left: 5px;
      color: tomato;
      font-size: 1rem;
    }
  }
  .icon {
    font-size: 0.6rem;
  }
}
</style>
