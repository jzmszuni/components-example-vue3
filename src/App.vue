<template>
  <div class="" style="width: 100vw;">
    <!-- <h1>APP</h1> -->
    <nav class="navbar navbar-light bg-light">
      <div class="container-fluid">
        <span class="navbar-brand mb-0 h1">APP</span>
      </div>
    </nav>
    <loading-spinner
      v-if="loading"
    />
    <div class="container-fluid d-flex flex-column align-items-center mt-5 w-50" v-else>
      <div class=" text-center text-light">
        <h2>Mis post favoritos: {{ favorito }}</h2>
      </div>
      <paginate-post 
        @preview = "preview"
        @next = "next"
        :start = "start"
        :end = "end"
        :dataLength = "posts.length"
      />

      <!-- Al ponerle : al id ":id" lo detecta de tipo numérico, de lo contrario lo detecta de timpo String -->
      <!-- .slice no incluye el elemento de cierre, es decir slice(0, 10) => 0, ..., 9 -->
      <blog-post
        v-for       = "post in posts.slice(start, end)"
        :key        = "post.id"
        :id         = "post.id"
        :title      = "post.title"
        :body       = "post.body"
        @cFavorite  = "cambiarFavorito"
      >

      </blog-post>

    </div>
  </div>

</template>

<script setup>
  import { onMounted, ref }   from 'vue'
  import BlogPost             from './components/BlogPost.vue';
  import LoadingSpinner       from './components/LoadingSpinner.vue';
  import PaginatePost         from './components/PaginatePost.vue';

  // loading
  const loading = ref(true)

  // request/data
  const posts = ref([
    {
      id:1,
      title:"Post 1",
      body:"Lorem ipsum dolor sit amet.1", 
    },
    {
      id:2,
      title:"Post 2",
      body:"Lorem ipsum dolor sit amet.2", 
    },
    {
      id:3,
      title:"Post 3",
    },
    {
      id:4,
      title:"Post 4",
      body:"Lorem ipsum dolor sit amet.4", 
    },
    {
      id:5,
      body:"Lorem ipsum dolor sit amet.5", 
    }
  ])

  // paginación
  const postForPage = 10
  const start = ref(0)
  const end = ref(postForPage) 

  // pagination / next
  const next = () => {
    start.value += postForPage;
    end.value += postForPage;
  }

  // pagination / preview
  const preview = () => {
    start.value += - postForPage;
    end.value += - postForPage;
  }

  // favorites
  const favorito = ref('')
  const cambiarFavorito = (title) => {
    favorito.value = title;
  }

  // get api data -> Al crear el dom
  const getData = async () =>{
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value = await res.json()
    } catch (error) {
      console.error(error);
    } finally {
      setTimeout(() => {
        loading.value=false
      }, 2000)
    }
  }
  onMounted( ()=>{
    getData();
  } )

  // get api data -> Al montar el dom
  // onMounted(async() => {
  //   try {
  //     const res = await fetch('https://jsonplaceholder.typicode.com/posts')
  //     posts.value = await res.json()
  //   } catch (error) {
  //     console.error(error);
  //   } finally {
  //     setTimeout(() => {
  //       loading.value=false
  //     }, 2000)
  //   }
  // })

  // get api data -> Al crear el dom 2da opción (FETCH)
  // fetch('https://jsonplaceholder.typicode.com/posts')
  // .then(res => res.json())
  // .then(data => {
  //   posts.value = data
  // })
  // .catch((e) => console.error(e))
  // // .finally(() => {
  // //   setTimeout(() => {
  // //     loading.value=false

  // //   }, 2000)
  // // })
  // .finally(() => loading.value = false)

</script>

<style>

</style>