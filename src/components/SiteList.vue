<style>
  .site-card {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  .site-card__text {
    font-size: 13px;
  }
</style>

<template>
  <v-container grid-list-xl>
    <v-layout wrap class="site-layout">
      <v-flex xs2 v-for="item in items" :key="item.href">
        <v-card :href="item.href">
          <v-card-text class="site-card">
            <v-layout>
              <v-flex xs1>
                <v-img width="16" height="16" :src="item.origin + '/favicon.ico'"></v-img>
              </v-flex>
              <v-flex xs10 class="site-card__text">{{item.host}}</v-flex>
              <v-btn small icon>
                <v-icon small>close</v-icon>
              </v-btn>
            </v-layout>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex xs2>
        <v-text-field v-model="newSite" solo hide-details label="New site..." @keyup.enter="submitItem"></v-text-field>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    props: ['items', 'addItem'],
    data: () => ({
      newSite: '',
    }),
    methods: {
      submitItem() {
        this.addItem(this.newSite);
        this.newSite = '';
      }
    }
  };
</script>
