<template>
  <v-container>
      <GithupRepo @reposelected="onRepoSelected"/>
     <GithubIssues :repo="repo"/>
  </v-container>
  </template>
  
<script>
import GithubIssues from './GithubIssues';
import GithupRepo from './GithupRepo';
export default {
    components: {
    GithupRepo,
    GithubIssues
},
    data: () => ({
        repo: null
    }),
    methods: {
        onRepoSelected (repo){
            this.repo = repo
        }
    }
}
</script>
