<template>
  <div>
    <main id="main">
      <input
        type="hidden"
        id="page"
        value="1
    "
      />
      <div class="movie" v-for="title in news" v-bind:key="title.id">
        <a style="text-decoration: none; color: #000" :href="title.url">
          <div>
            <img
              class="test"
              :src="title.urlToImage"
              style="border: 3px solid #fff; border-radius: 6px"
            />
          </div>
          <div class="movie-info">
            <h3>{{ title.title }}</h3>
          </div>
          <div class="description">
            <h3>Content</h3>
            {{ title.content }}
          </div>
          <div class="flx">
            <span class="prov">Author : "{{ title.author }}"</span>
            <br />
            <br />
            <span class="prov">Published At : {{ title.publishedAt }}</span>
          </div>
        </a>
      </div>
      <nav aria-label="Page navigation example">
        <ul class="pagination justify-content-center">
          <li class="page-item">
            <a @click="prevPage()" class="page-link">Previous</a>
          </li>
          <li class="page-item">
            <a class="page-link" v-on:click="nextPage()">Next</a>
          </li>
        </ul>
      </nav>
    </main>
  </div>
</template>
<script src="https://unpkg.com/axios@1.1.2/dist/axios.min.js"></script>
<script>
const API_URL =
  "https://newsapi.org/v2/everything?q=tesla&from=2022-10-18&sortBy=publishedAt&apiKey=44260ed9dafe458b9d2cdd740fcf785b" +
  "&page=  ";

  getNews(API_URL, "1"),
</script>
<script>
export default {
  data() {
    return {
      news: [],
    };
  },
  created() {
    this.$axios
      .get(
        "https://newsapi.org/v2/everything?q=tesla&from=2022-10-18&sortBy=publishedAt&apiKey=44260ed9dafe458b9d2cdd740fcf785b"
      )
      .then((res) => {
        this.news = res.data.articles;
        console.log(res.data.articles);
      });
  },
  methods: {
    getNews(ex, page) {
      if (page) {
        ex = ex + page;
      }
    },
    nextPage() {
      var a = parseInt(document.getElementById("page").value);
      var b = a + 1;
      a = b;
      document.getElementById("page").value = b;
      console.log(b);
      getNews(API_URL, b);
    },
    prevPage() {
      var c = parseInt(document.getElementById("page").value);
      1;
      if (c > 1) {
        var d = c - 1;
        c = d;
        document.getElementById("page").value = d;
        console.log(d);
        getNews(API_URL, d);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;1,100;1,200;1,300;1,400&display=swap");

* {
  box-sizing: border-box;
  font-family: "Poppins", sans-serif;
}

main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.movie {
  width: 300px;
  margin: 1rem;
  border-radius: 6px;
  box-shadow: 10px 10px 66px -28px rgba(5, 5, 5, 1);
  background: #0000c9;
  position: relative;
  overflow: hidden;
}

.movie img {
  width: 100%;
  border-radius: 6px;
}

.movie-info {
  color: #fff;
  align-items: center;
  justify-content: space-between;
  padding: 0.5rem 1rem 1rem;
  letter-spacing: 0.5px;
}

.movie-info h3 {
  margin-top: 0;
  font-size: 20px;
}

.prov {
  background-color: #d31c1c;
  padding: 0.25rem 0.5rem;
  border-radius: 3px;
  font-weight: bold;
}

.description {
  bottom: 0;
  right: 0;
  left: 0;
  background: #0000c9;
  color: #fff;
  padding: 1rem;
  max-height: 100%;
}
.flx {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  margin-top: 20px;
}
</style>