<template>
    <div id="app">
        <v-app id="inspire">
            <v-card
                    class="text-start"
                    min-width="480"
            >
                <v-list three-line subheader min-width="480">
                    <v-list-item-group v-model="item" color="primary">
                        <v-list-item
                                v-for="(item, i) in projects"
                                :key="i"
                                three-line
                                @click="$router.push('/project/' + item.projectId)"
                        >
                            <v-list-item-content>
                                <v-list-item-title>{{item.description}}</v-list-item-title>
                                <v-list-item-subtitle v-html="item.projectId"></v-list-item-subtitle>
                                <v-list-item-subtitle v-html="item.projectName"></v-list-item-subtitle>
                            </v-list-item-content>
                        </v-list-item>
                    </v-list-item-group>
                </v-list>
            </v-card>
        </v-app>
    </div>
</template>

<script>
    import {mapMutations} from 'vuex'
    import {mapActions} from 'vuex'
    import {mapGetters} from 'vuex'

    export default {
        data () {
            return {
                item: 1,
            }
        },
        methods: {
            ...mapGetters(['getUser','getTasks', 'getProjects']),
            ...mapMutations(['emptyProjects', 'setProjects']),
            ...mapActions(['getUserTasks', 'getProjectsByIdList']),
        },
        computed: {
            projects () {
                return this.getProjects()
            }
        },
        created () {
            console.log("Created UserProfileProjects()")
            this.emptyProjects()
            this.getProjectsByIdList(this.getTasks().map(a => a.project))
        }
    }
</script>

<style scoped>

</style>