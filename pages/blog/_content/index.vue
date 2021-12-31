<template>
  <div>
    <navigasi />

    <div class="jumbotron">
      <h1 class="display-4" style="font-weight: 900; color: black">
        {{ oneObject.title }}
      </h1>
    </div>
    <div class="row">
      <div class="col-md-4"></div>
      <div
        class="col-md-4 documentContainer"
        v-for="(author, i) in oneObject.authors"
        :key="i"
      >
        <div class="author mb-3 d-flex">
          <img
            :src="author.user.profile_picture.url"
            alt="profile-picture"
            class="shadow"
            width="80px"
            height="80px"
            style="border: 1px solid gray; border-radius: 50%"
          />
          <div class="ml-2">
            <p style="margin-top: 15px; font-size: 17px">
              {{ author.user.full_name }}
            </p>
            <p style="font-size: 12px; color: gray; margin-top: -15px">
              {{ convertDate(oneObject.date) }}
            </p>
          </div>
        </div>
        <div
          v-for="(text, i) in jsonParse(oneObject.editorState).blocks"
          :key="i"
          class="mb-3"
        >
          {{ text.text }}

          <div v-if="text.type === 'atomic'">
            <div>
              <img
                :src="jsonParse(oneObject.editorState).entityMap[0].data.src"
                alt=""
                width="500px"
                height="400px"
              />
            </div>
          </div>
        </div>
      </div>

      <div class="col-md-4"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dataEditorState: [],
      listData: [],
    };
  },
  methods: {
    jsonParse(parse) {
      let item = parse;
      let data = JSON.parse(item);
      return data;
    },
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
        let data = this.oneObject().editorState;
        let parseData = JSON.parse(data);
        this.dataEditorState = data;
      } catch (error) {
        console.log(error);
      }
    },
    convertDate(date) {
      const data = moment(`${date}`).format("MMMM DD YYYY");
      return data;
    },
  },
  computed: {
    oneObject() {
      const obj = this.listData.find(
        (data) => data.link === this.$route.params.content
      );
      var new_obj = Object.assign({}, obj);
      return new_obj;
    },
  },
  mounted() {
    this.GET_DATA();
    this.GET_EDITOR_STATE();
  },
};
</script>

<style scoped>
.jumbotron {
  height: 400px;
}

.display-4 {
  margin-top: 200px;
  margin-left: 50px;
}

.container-sm {
  width: 400px;
}

.author {
  width: 100%;
}

.documentContainer {
  height: 100%;
  margin-bottom: 100px;
}
</style>
