<template>
  <v-content>
    <site-list :items="sites" :addItem="addSite" />
  </v-content>
</template>

<script>
import SiteList from './components/SiteList.vue'

const sitesKey = 'sites';
const isDomain = /^((?!-))(xn--)?[a-z0-9][a-z0-9-_]{0,61}[a-z0-9]?\.(xn--)?([a-z0-9-]{1,61}|[a-z0-9-]{1,30}\.[a-z]{2,})$/;

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
      if (isDomain.test(site)) {
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
