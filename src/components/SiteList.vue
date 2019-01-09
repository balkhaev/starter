<style>
  .site-card {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
</style>

<template>
  <v-container grid-list-xl>
    <v-layout wrap class="site-layout">
      <v-flex xs3 v-for="item in items" :key="item.href">
        <v-card :href="item.href">
          <v-tooltip bottom>
            <v-card-text class="site-card" slot="activator">
              <v-layout>
                <v-flex xs1>
                  <v-img width="16" height="16" :src="item.origin + '/favicon-16x16.png'"></v-img>
                </v-flex>
                <v-flex xs10>{{item.host}}</v-flex>
                <v-btn small icon>
                  <v-icon small>close</v-icon>
                </v-btn>
              </v-layout>
            </v-card-text>
            <span>{{item.href}}</span>
          </v-tooltip>
        </v-card>
      </v-flex>
      <v-flex xs3>
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
