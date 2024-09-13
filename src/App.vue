<template>
    <div class="app">
        <post-form />
        <post-list :posts="posts" />
    </div>
</template>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

.app {
    padding: 20px;
}
</style>

<script>
import PostList from '@/Components/PostList.vue'
import PostForm from '@/Components/PostForm.vue'




export default {
    components: {
        PostList, PostForm
    },
    data() {
        return {
            posts: [
                { id: 1, title: 'Javascript', body: 'descr ' },
                { id: 2, title: 'Javascript 2', body: 'descr  2' },
                { id: 3, title: 'Javascript 3', body: 'descr  3' },
                { id: 3, title: 'Javascript 4', body: 'descr  4' },
            ],
           
        }
    },
    methods: {
        createPost() {
            

        },


    }

}


</script>
