<template>
    <div class="app">
        <h1>Page with posts</h1>
        <div class="app__btns">
            <my-button
            @click="showDialog"
            >
            to create post
            </my-button>
            <my-select
            v-model="selectedSort"
            :options="sortOptions"
            />
        </div>
       
        <my-dialog v-model:show="dialogVisible">
            <post-form @create="createPost" />
        </my-dialog>

        <post-list :posts="posts" @remove='removePost'
        v-if="!isPostsLoading"
         />
         <div v-else>Loading...</div>
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

.app__btns {
    margin: 15px 0;
    display: flex;
    justify-content: space-between;
}
</style>

<script>
import PostList from '@/Components/PostList.vue'
import PostForm from '@/Components/PostForm.vue'
import MyButton from './Components/UI/MyButton.vue';
import axios from 'axios';
import MySelect from '@/Components/UI/MySelect.vue';




export default {
    components: {
        MySelect,
        MyButton,
        PostList,
        PostForm,
    },
    data() {
        return {
            posts: [],
            dialogVisible: false,
            isPostsLoading: false, 
            selectedSort: '',
            sortOptions: [
                {value: 'title', name: "by title"},
                {value: 'body', name: "by content"},
            ]

        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post);
            this.dialogVisible = false;
        },
        removePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        showDialog() {
            this.dialogVisible = true;
        },
        async fetchPosts() {
            try {
                this.isPostsLoading = true;
                    const response = await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=10");
                    this.posts = response.data;
            } catch (e) {
                alert('danger')

            } finally {
                this.isPostsLoading = false;

            }

        }

    },
    mounted(){
        this.fetchPosts();
    }

}


</script>
