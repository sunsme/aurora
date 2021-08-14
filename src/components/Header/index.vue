<template>
  <header>
    <RouterLink class="title" to="/">{{ $config.title }}</RouterLink>
    <span class="subtitle">{{ hitokoto }}</span>
    <nav>
      <RouterLink v-for="menu in displayMenu" :key="menu.path" :to="menu.path">
        <i :class="['icon', `icon-${menu.icon}`]" />
        {{ menu.title }}
      </RouterLink>
    </nav>
  </header>
</template>

<script>
export default {
  name: 'Header',
  data() {
    const { archiveOpts, categoryOpts, tagOpts, inspirationOpts, bookOpts, friendOpts, aboutOpts } = this.$config
    return {
      hitokoto: null,
      menu: [
        { path: '/', display: true, icon: 'shop', title: '首页' },
        { path: '/archive', display: archiveOpts.display, icon: 'inbox', title: '归档' },
        { path: '/category', display: categoryOpts.display, icon: 'bookmark-empty', title: '分类' },
        { path: '/tag', display: tagOpts.display, icon: 'tag', title: '标签' },
        { path: '/book', display: bookOpts.display, icon: 'pencil', title: '书单' },
        { path: '/inspiration', display: inspirationOpts.display, icon: 'comment', title: '灵感' },
        { path: '/friend', display: friendOpts.display, icon: 'heart', title: '友链' },
        { path: '/about', display: aboutOpts.display, icon: 'universal-access', title: '关于' },
      ],
    }
  },
  computed: {
    displayMenu() {
      return this.menu.filter((o) => o.display)
    },
  },
  async mounted() {
    const res = await fetch("https://v1.hitokoto.cn/");
    const json = await res.json();
    this.hitokoto = `${json.hitokoto} - ${json.from}`;
  }
}
</script>

<style lang="scss" scope>
@import './index.scss';

.subtitle{
  font-size: 1rem !important;
  font-family: "Microsoft YaHei" !important;
}
</style>
