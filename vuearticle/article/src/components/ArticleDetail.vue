<template>
  <v-card>
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
      <v-btn color="blue darken-1" text @click="close"> Cancel </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
    name:"ArticleDetail",
    props: {
      selectedItem:Object
    },
    methods:{
      close() {
      console.log(this.$parent);  
      this.dialog = false;
      this.$emit('close');
    },

    }
}
</script>