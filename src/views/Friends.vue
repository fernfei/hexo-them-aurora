<template>
  <div class="flex flex-col">
    <div class="post-header">
      <Breadcrumbs :current="t('menu.friends')" />
      <h1 class="post-title text-white uppercase">{{ t('menu.friends') }}</h1>
    </div>
    <div class="bg-ob-deep-800 px-14 py-16 rounded-2xl shadow-xl block" style="min-height: 600px">
      <div
        style="
          display: flex;
          flex-wrap: wrap;
          justify-content: space-between;
          align-items: center;
        "
      >
        <div v-for="friend in friends" :key="friend.link" class="friend-link">
          <a :href="friend.link" target="_blank">
            <div style="margin-left: 25px">
              <img :src="friend.avatar" alt="avatar" class="avatar-img" />
            </div>
            <div style="margin-left: 15px">
              <div>{{ friend.name }}</div>
              <div style="font-size: 15px">{{ friend.intro }}</div>
            </div>
            <div class="friend-bg">
              <img :src="friend.avatar" alt="avatar" />
            </div>
          </a>
        </div>
        <div class="friend-link" style="visibility: hidden" />
        <div class="friend-link" style="visibility: hidden" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, onMounted, ref } from 'vue'
import Breadcrumbs from '@/components/Breadcrumbs.vue'
import { useI18n } from 'vue-i18n'
import { useAppStore } from '@/stores/app'

export default defineComponent({
  name: 'Friends',
  components: { Breadcrumbs },
  setup() {
    const { t } = useI18n()
    const appStore = useAppStore()
    setInterval(() => {
      let friends = ref(appStore.themeConfig.friends.friends)
      console.log(friends)
    }, 1000)

    return {
      t,
      friends: computed(() => appStore.themeConfig.friends.friends)
    }
  }
})
</script>

<style lang="scss" scoped>
.timeline {
  position: relative;
  z-index: 2;
  line-height: 1.4em;
  list-style: none;
  margin: 0;
  padding: 0;
  width: 100%;

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    margin-top: 0;
  }
}

.friend-link {
  margin-top: 30px;
  width: 432px;
  height: 108px;
  overflow: hidden;
  @apply pb-2 mb-4 text-ob-bright relative text-2xl;
  font-weight: 600;
  border-radius: 20px;
  &:after {
    @apply absolute bottom-0 h-1 w-24 rounded-full;
    content: '';
    left: 0;
  }
  background: linear-gradient(
    130deg,
    rgb(36, 198, 220),
    rgb(84, 51, 255) 41.07%,
    rgb(255, 0, 153) 76.05%
  );
  --text-accent: #24c6dc;
  --text-sub-accent: #ff0099;
  --main-gradient: linear-gradient(
    130deg,
    #24c6dc,
    #5433ff 41.07%,
    #ff0099 76.05%
  );
}

.friend-link > a {
  height: 100%;
  width: 100%;
  display: flex;
  align-content: center;
  align-items: center;
  position: relative;
}
.avatar-img {
  border-radius: 50%;
  width: 60px;
  height: 60px;
  display: inline-block;
}
.friend-bg {
  position: absolute;
  bottom: -45px;
  right: -45px;
  width: 120px;
  height: 120px;
  opacity: 0.3;
  filter: alpha(opacity=3);
}
.friend-bg > img {
  width: 100%;
  height: 100%;
  border-radius: 50%;
}
</style>
