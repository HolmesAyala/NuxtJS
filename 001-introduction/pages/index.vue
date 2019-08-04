<template>
<div>
    <h1>Hello from NuxtJS</h1>    

    <h4>Comments</h4>

    <div v-for="comment in comments" :key="comment.id">
        <p>{{ comment.name }}</p>
        <a :href="'/comment/' + comment.id"> view </a>
    </div>
</div>
</template>
 
<script>

import ENVIRONMENT from "~/config/environment.js"
import Axios from "axios"

export default {
    created() {
        this.getGetComments()
    },
    data() {
        return {
            comments: []
        }
    },
    methods: {
        async getGetComments() {
            try {
                let data = (await Axios.get(`${ENVIRONMENT.URL_API}/comments`)).data

                this.comments = data.slice(0, 20)
            } catch (error) {
                console.log(error);
            }
        }
    }
}
</script>
 
<style scoped>

</style>
