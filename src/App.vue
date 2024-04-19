<script setup>
  import { computed } from "@vue/reactivity"
  import { ref } from "vue"
  // import AboutView from './views/AboutView.vue'
  import BlogPost from './components/Blogpost.vue';
  import PaginatePost from './components/PaginationPost.vue';
  const miFavorito = ref("");
  const posts = ref([]);
  const postXpage = 10;
  const inicio = ref(0);
  const fin = ref(postXpage);

  // const posts = ref([
  //   { id: 1, title: "Post 01", body: "Descrión del post 01" },
  //   { id: 2, title: "Post 02", body: "Descrión del post 02" },
  //   { id: 3, title: "Post 03" },
  // ]);

  // const miFavorito = ref("");

  // const fijarFavorito = (title) => { 
  //     miFavorito.value = title;
  // };

fetch("https://jsonplaceholder.typicode.com/posts")
    .then((res) => res.json())
    .then((data) => (posts.value = data));

const fijarFavorito = (title) => {
    miFavorito.value = title;
};
const next = () => {
    inicio.value = inicio.value + postXpage;
    fin.value = fin.value + postXpage;
};

const prev = () => {
    inicio.value = inicio.value - postXpage;
    fin.value = fin.value - postXpage;
};

const maxLength = computed(() => posts.value.length);

</script>

<template>
  <!-- <h1>Here is a child component!</h1><br>
  <AboutView /> <br>
  <AboutView /> <br>
  <AboutView /> <br> -->
  <!-- <BlogPost title="My journey with Vue" />
  <BlogPost title="Blogging with Vue" />
  <BlogPost title="Why Vue is so fun" /> -->
  <!-- <BlogPost 
    title="Post 01" 
    body="Descrión del post 01"
    :id="1"
  />
  <BlogPost 
    title="Post 02" 
    body="Descrión del post 02"
    :id="2"
  />
  <BlogPost 
    title="Post 03" 
    body="Descrión del post 03"
    :id="3"
  /> -->
  <!-- <div class="container">
        <h1>Blog</h1>
        <BlogPost
            v-for="post in posts"
            :key="post.title"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            class="mb-2"
            aclarar esto va en BlogPost @fijarFavorito="fijarFavorito"
        />
  </div> -->
  <!-- <div class="container">
        <h1>{{ miFavorito || "Sin favorito" }}</h1>

        <div>
            <BlogPost
                v-for="post in posts"
                :key="post.title"
                :title="post.title"
                :id="post.id"
                :body="post.body"
                class="mb-2"
                :fijarFavorito="fijarFavorito"
            />
        </div>
    </div> -->
    <div class="container">
        <h1>{{ miFavorito || "Sin favorito" }}</h1>

        <PaginatePost
            @next="next"
            @prev="prev"
            :inicio="inicio"
            :fin="fin"
            :maxLength="maxLength"
            class="mb-2"
        ></PaginatePost>

        <BlogPost
            v-for="post in posts.slice(inicio, fin)"
            :key="post.title"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            class="mb-2"
            @fijarFavorito="fijarFavorito"
        >
        </BlogPost>
    </div>
</template>


