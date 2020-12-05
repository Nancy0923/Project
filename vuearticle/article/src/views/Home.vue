<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="publishedArticle"
      sort-by="calories"
      class="elevation-1"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Home</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>
          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                color="primary"
                dark
                class="mb-2"
                v-bind="attrs"
                @click="openArticles()"
              >
                Articles
              </v-btn>
            </template>
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:no-data>
        <v-btn color="primary" @click="initialize"> Reset </v-btn>
      </template>
    </v-data-table>
  </div>
</template>

 <script>
import { article } from "../data";
import router from "@/router/index";

export default {
  name:"Home",
  data: () => ({
    article: article,
    publishedArticle: [],
    dialog: false,
    headers: [
      {
        text: "ArticeId",
        sortable: false,
        value: "articleId",
      },
      { text: "Name", value: "title" },
      { text: "Description", value: "body" },
    ],
  }),


  watch: {
    dialog(val) {
      val || this.close();
    },
  },

  created() {
     localStorage.setItem("articles", JSON.stringify(this.article));
    this.initialize();
  },

  methods: {
    initialize() {
      this.article.forEach((item) => {
        if (item.published) {
          this.publishedArticle.push(item);
          console.log(this.publishedArticle);
        }
      });
    },
    openArticles() {
      router.push({ name: "Articles" });
    },

    deleteItemConfirm() {
      this.desserts.splice(this.editedIndex, 1);
      this.closeDelete();
    },

    close() {
      this.dialog = false;
    },
  },
};
</script>
