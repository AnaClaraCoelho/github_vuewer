<template>
    <div>
        <v-row>
            <v-col cols="12">
                <v-simple-table>
                    <template v-slot:default>
                    <thead>
                        <tr>
                            <th class="text-left">
                                Number
                            </th>
                            <th class="text-left">
                                Title
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="issue in issues" :key="issue.number"                        >
                            <td>{{ issue.number }}</td>
                            <td>{{ issue.title }}</td>
                        </tr>
                    </tbody>
                    </template>
                </v-simple-table>
            </v-col>
        </v-row>
        <v-row>
            <v-col cols="12">
                <v-progress-circular
                indeterminate
                color="primary"
                v-if="loading">
                </v-progress-circular>
                <v-btn color="primary" v-if="maisPaginas" @click="listaIssues"> MAIS</v-btn>
            </v-col>
        </v-row>
    </div>
  </template>
  
<script>

import {api} from '~api'

    export default {
        props: ['repo'],
        data: () => ({
            issues: [],
            loading: false,
            maisPaginas: false,
            currentPage: 1
        }),
        methods: {
            async listaIssues () {
                this.loading = true
                const maisIssues = await api.listaIssues(this.repo.owner.login, this.repo.name, this.currentPage)
                this.issues = this.issues.concat(maisIssues)
                this.currentPage ++
                this.loading = false
                this.maisPaginas = maisIssues.length > 0
            }
        },
        watch: {
            repo() {
                this.isses = []
                if (this.repo){
                    this.maisPaginas = false
                    this.currentPage = 1
                    this.listaIssues()
                } else {
                    this.issues = []
                    this.maisPaginas = false
                    this.currentPage = 1
                }
            }
        }
    }
</script>