<template>
    <q-page class="flex flex-center">
        <h4>POSTS</h4>
        <q-list bordered separator>
            <q-item clickable v-ripple v-for="post in posts" :key="post.id" @click="openPost(post)">
                <q-item-section>
                    <q-item-label overline>{{ post.title }}</q-item-label>
                    <q-item-label>{{ post.body }}</q-item-label>
                </q-item-section>
            </q-item>
        </q-list>

        <q-dialog v-model="dialog" persistent v-if="post">
            <q-card>
                <q-card-section class="row items-center">
                    <q-avatar icon="signal_wifi_off" color="primary" text-color="white" />
                    <span class="q-ml-sm">№ {{ post.id }}</span>
                </q-card-section>

                <q-card-section class="row items-center">
                    <span class="q-ml-sm text-bold">{{ post.title }}</span>
                </q-card-section>

                <q-card-section class="row items-center">
                    <span class="q-ml-sm">{{ post.body }}</span>
                </q-card-section>

                <!-- Notice v-close-popup -->
                <q-card-actions align="right">
                    <q-btn flat label="Close" color="primary" v-close-popup />
                </q-card-actions>
            </q-card>
        </q-dialog>

    </q-page>
</template>

<script>
    export default {
        name: 'PagePosts',
        data(){
            return {
                posts: [],
                dialog: false,
                post: null
            }
        },
        created(){
            this.$axios.get('https://jsonplaceholder.typicode.com/posts')
                .then(response => {
                    this.posts = response.data
                })
        },
        methods:{
            openPost(p){
                this.post = p;
                this.dialog = true
            }
        }
    }
</script>
