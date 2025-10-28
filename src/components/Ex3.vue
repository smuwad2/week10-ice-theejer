<script setup>
// Import BlogPost component
import BlogPost from './subcomponents/BlogPost2.vue';
import axios from 'axios'
</script>

<script>
export default {
    data() {
        return {
            posts: [] // array of post objects
        }
    },
    computed: {
        baseUrl() {
            if (window.location.hostname == 'localhost')
                return 'http://localhost:3000'
            else {
                const codespace_host = window.location.hostname.replace('5173', '3000')
                return `https://${codespace_host}`;
            }
        }
    },
    created() { // created is a hook that executes as soon as Vue instance is created
        axios.get(`${this.baseUrl}/posts`)
            .then(response => {
                // this gets the data, which is an array
                this.posts = response.data
                console.log(response.data)
            })
            .catch(error => {
                this.posts = [{ entry: 'There was an error: ' + error.message }]
            })
    },
    methods: {
        async deletePost(id) {
            // TODO: Complete the delete method
            try {
                const response = await axios.get(`${this.baseUrl}/deletePost`, {
                    params: {
                        id: id
                    }
                })
                console.log(response.data)
                axios.get(`${this.baseUrl}/posts`)
                    .then(response => {
                        // this gets the data, which is an array
                        this.posts = response.data
                        console.log(response.data)
                    })
                    .catch(error => {
                        this.posts = [{ entry: 'There was an error: ' + error.message }]
                    })
            } catch (e) {
                console.error(e);
            }
        }
    },
    components: {
        BlogPost,
    }
}
</script>

<template>
    <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <BlogPost v-for="post of posts" :mood="post.mood">
        <template v-slot:subject>{{ post.subject }}</template>
        <template v-slot:entry>{{ post.entry }}</template>
        <template v-slot:deleteButton>
            <button class="btn btn-danger" @click="deletePost(post.id)">
                Delete
            </button>
        </template>
    </BlogPost>
</template>
