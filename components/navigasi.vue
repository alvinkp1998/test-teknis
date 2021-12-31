<template>
  <div class="card shadow-sm">
    <div class="card-body">
      <div class="text-center arrow">
        <button class="btn btn-primary" style="border-radius: 50%">
          &#8592;
        </button>
      </div>
      <div class="text-center">
        <button class="btn btn-light btn-pill mb-3 mt-3">BLOG</button>
      </div>
      <div class="title">
        <p class="p-2">SEMINAR & WORKSHOP</p>
      </div>
      <div class="content" v-for="data in listSeminar" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}/`">{{ data.title }}</nuxt-link>
        </p>
      </div>

      <div class="title">
        <p class="p-2">ACHIEVEMENT</p>
      </div>
      <div class="content" v-for="data in listAchiev" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}`">{{ data.title }}</nuxt-link>
        </p>
      </div>
      <div class="title">
        <p class="p-2">NEWS</p>
      </div>
      <div class="content" v-for="data in listNews" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}`">{{ data.title }}</nuxt-link>
        </p>
      </div>
      <div class="title">
        <p class="p-2">PARTNERSHIP</p>
      </div>
      <div class="content" v-for="data in listPartner" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}`">{{ data.title }}</nuxt-link>
        </p>
      </div>
      <div class="title">
        <p class="p-2">Kompetisi MAPID</p>
      </div>
      <div class="content" v-for="data in listKompetisi" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}`">{{ data.title }}</nuxt-link>
        </p>
      </div>
      <div class="title">
        <p class="p-2">Weekly MAPID Blog</p>
      </div>
      <div class="content" v-for="data in listWeekly" :key="data.id">
        <p class="p-2 mt-2">
          <nuxt-link :to="`/blog/${data.link}`">{{ data.title }}</nuxt-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      listData: [],
      listEditorState: [],
    };
  },
  methods: {
    async GET_DATA() {
      try {
        const DATA = await this.$axios.get("/");
        console.log(DATA);
        this.listData = DATA.data;
      } catch (error) {
        console.log(error);
      }
    },
    async GET_EDITOR_STATE() {
      try {
        const DATA = await this.$axios.get("/");
        console.log(DATA);
        let data = DATA.data[0].editorState;
        let parseData = JSON.parse(data);
        this.listEditorState = parseData;
      } catch (error) {
        console.log(error);
      }
    },
    toContent(title) {
      this.$router.push(`/blog/${title}`);
    },
  },
  mounted() {
    this.GET_DATA();
    this.GET_EDITOR_STATE();
  },
  computed: {
    listSeminar() {
      return this.listData.filter((data) => data.sub_bracket === "seminar");
    },
    listAchiev() {
      return this.listData.filter((data) => data.sub_bracket === "achievement");
    },
    listNews() {
      return this.listData.filter((data) => data.sub_bracket === "news");
    },
    listPartner() {
      return this.listData.filter((data) => data.sub_bracket === "partnership");
    },
    listKompetisi() {
      return this.listData.filter(
        (data) => data.sub_bracket === "teknis_kompetisi_mapid"
      );
    },
    listWeekly() {
      return this.listData.filter(
        (data) => data.sub_bracket === "weekly_mapid_blog"
      );
    },
  },
};
</script>

<style scoped>
.card {
  z-index: 999;
  position: fixed;
  bottom: 0;
  background-color: #e4e4e4;
  border-radius: 15px;
  width: 300px;
  height: 500px;
  overflow: auto;
  margin-left: 40px;
}
.card::-webkit-scrollbar {
  width: 12px;
  height: 150px;
}

.card::-webkit-scrollbar-track {
  background: #e4e4e4;
}

.card::-webkit-scrollbar-thumb {
  background-color: #dddada;
  border-radius: 20px;
}
.card::-webkit-scrollbar-thumb:hover {
  background-color: #2196f3;
}

.btn-pill {
  border-radius: 20px;
  padding: 5px 20px 5px 20px;
}

.arrow {
  position: fixed;
  margin-left: 105px;
  margin-top: -40px;
}

.title {
  color: white;
  background-color: #2196f3;
  margin-bottom: -6px;
  font-size: 14px;
}

.content {
  background-color: white;
  margin-bottom: -6px;
  font-size: 14px;
}

.container-fluid {
  height: 2000px;
}

a {
  color: black;
}

a:active {
  color: blue;
}
</style>
