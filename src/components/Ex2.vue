<script>
    // Import BlogPost component
    import BlogPost from './subcomponents/BlogPost.vue';
	import axios from 'axios'
    export default {
        data() {
            return {
                posts: [] // array of post objects
            }  
        },
        computed: {
            baseUrl() {
                if (window.location.hostname=='localhost')
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
        components:{
            BlogPost
        }
    }
</script>

<template>
   <!-- TODO: make use of the 'blog-post' component to display the blog posts -->
    <BlogPost v-for="post of posts" :mood="post.mood">
        <template v-slot:subject>{{ post.subject }}</template>
        <template v-slot:entry>{{ post.entry }}</template>
    </BlogPost>
</template>

