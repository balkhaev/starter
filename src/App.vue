<style>
  html, body {
    overflow: hidden;
  }
  body {
    background-image: url("assets/bg-2.jpg");
    background-size: cover;
  }
</style>

<template>
  <v-content>
    <site-list :items="sites" :addItem="addSite" />
  </v-content>
</template>

<script>
import SiteList from './components/SiteList.vue'

const sitesKey = 'sites';

export default {
  name: 'app',
  components: {
    SiteList,
  },
  data: () => ({
    sites: JSON.parse(localStorage.getItem(sitesKey)) || [],
  }),
  methods: {
    addSite(site) {
      if (!site.startsWith('http')) {
        site = 'http://' + site;
      }

      const url = new URL(site);
      this.sites.push({
        href: site,
        host: url.host.replace('www.', ''),
        hash: url.hash,
        search: url.search,
        origin: url.origin,
        pathname: url.pathname,
      });
      localStorage.setItem(sitesKey, JSON.stringify(this.sites));
    }
  }
}
</script>
