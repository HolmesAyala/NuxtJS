<template>
<div>
    <nuxt-link to="/"> Volver </nuxt-link>

    <h2>Comment</h2>

    <div v-if="comment">
        <h3>From: {{ comment.email }}</h3>

        <h4>Name: {{ comment.name }}</h4>

        <p>{{ comment.body }}</p>
    </div>
</div>
</template>

<script>
import VueRouter from "vue-router"
import Axios from "axios"
import ENVIRONMENT from "~/config/environment.js"

export default {
    created() {
        this.loadComment(this.$route.params.id)
    },
    data() {
        return {
            comment: null
        }
    },
    methods: {
        async loadComment(id) {
            try {
                this.comment = (await Axios.get(`${ENVIRONMENT.URL_API}/comments/${id}`)).data

                console.log(this.comment);
            } catch (error) {
                console.log(error.message);
            }
        }
    }
}
</script>
