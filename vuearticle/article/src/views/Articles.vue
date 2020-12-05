<template>
  <div>
    <v-data-table
      :headers="headers"
      :items="article"
      sort-by="calories"
      class="elevation-1"
    >
      <template v-slot:[`item.published`]="{ item }">
        <v-simple-checkbox
          v-model="item.published"
          @click="addPublishedItem(item)"
        ></v-simple-checkbox>
      </template>
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Articles</v-toolbar-title>
          <v-divider class="mx-4" inset vertical></v-divider>
          <v-spacer></v-spacer>

          <v-dialog v-model="dialog" max-width="500px">
            <template v-slot:activator="{ on, attrs }">
              <v-btn
                color="primary"
                dark
                class="mb-2"
                v-bind="attrs"
                @click="openHome()"
              >
                Home
              </v-btn>
            </template>
            <ArticleDetail @close="close()" :selectedItem="selectedItem" />
            <!-- <v-card>
              <v-card-title>
                <span class="headline">Article Details</span>
              </v-card-title>

              <v-card-text>
                <v-container>
                  <v-row>
                    <v-col cols="12" sm="6" md="12">
                      <v-tooltip top>
                        <template v-slot:activator="{ on, attrs }">
                          <v-text-field
                            v-model="selectedItem.title"
                            label="Title"
                            readonly
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <span>{{ selectedItem.title }}</span>
                      </v-tooltip>
                    </v-col>
                    <v-col cols="12" sm="6" md="12">
                      <v-tooltip top>
                        <template v-slot:activator="{ on, attrs }">
                          <v-text-field
                            v-model="selectedItem.body"
                            label="Description"
                            v-bind="attrs"
                            v-on="on"
                          ></v-text-field>
                        </template>
                        <span>{{ selectedItem.body }}</span>
                      </v-tooltip>
                    </v-col>
                  </v-row>
                </v-container>
              </v-card-text>

              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="blue darken-1" text @click="close">
                  Cancel
                </v-btn>
              </v-card-actions>
            </v-card> -->
          </v-dialog>
        </v-toolbar>
      </template>
      <template v-slot:[`item.actions`]="{ item }">
        <v-icon small class="mr-2" @click="selectedArticle(item)">
          mdi-eye
        </v-icon>
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
import ArticleDetail from "../components/ArticleDetail";
export default {
  data: () => ({
    article: article,
    publishedArticle: [],
    selectedPublishedArticle: [],
    dialog: false,
    dialogDelete: false,
    headers: [
      {
        text: "Published",
        value: "published",
        sortable: false,
      },
      {
        text: "ArticeId",
        sortable: false,
        value: "articleId",
      },
      { text: "Name", value: "title" },
      { text: "Description", value: "body" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    desserts: [],
    selectedItem: {},
  }),
  components: {
    ArticleDetail,
  },
  watch: {
    dialog(val) {
      val || this.close();
    },
  },

  created() {},

  methods: {
    openHome() {
      router.push({ name: "Home" });
    },
    addPublishedItem(item) {
      this.selectedPublishedArticle.push(item);
      console.log("article", this.selectedPublishedArticle);
    },
    selectedArticle(item) {
      this.selectedItem = Object.assign({}, item);
      this.dialog = true;
    },

    close() {
      this.dialog = false;
    },
  },
};
</script>
