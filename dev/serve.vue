<script>
import Vue from "vue";
import VueMorphTable from "@/vue-morph-table.vue";

let fields = [
  { key: "hello_1", label: "Hello 1", check: true },
  { key: "hello_2", label: "Hello 2", check: true },
  { key: "hello_3", label: "Hello 3", check: true },
  { key: "hello_4", label: "Hello 4", check: true },
  { key: "hello_5", label: "Hello 5", check: true },
];

let items = [
  { hello_1: 1, hello_2: 2, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 5, hello_2: 1, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 7, hello_2: 2, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 8, hello_2: 5, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 1, hello_2: 2, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 5, hello_2: 1, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 7, hello_2: 2, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 8, hello_2: 5, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
  { hello_1: 1, hello_2: 2, hello_3: 3, hello_4: 4, hello_5: 5, check_bulk: false },
];

let actions = [
  { key: "edit", name: "Edit" },
  { key: "delete", name: "Delete" },
];

export default Vue.extend({
  name: "ServeDev",
  data() {
    return {
      fields,
      items,
      actions,
      load: false
    };
  },
  components: {
    VueMorphTable,
  },
  methods: {
    sortHandle(e) {
      const { column, asc } = e;
      this.items = this.items.sort(function (item1, item2) {
        return asc
          ? item1[column] - item2[column]
          : item2[column] - item1[column];
      });
    },
    changeCurrentPage(e) {
      console.log(e)
    },
    changeNumOfRows(e) {
      console.log(e)
    },
    clickRow(e) {
      console.log(e)
    },
    edit(item) {
      console.log(item);
    }
  },
});
</script>

<template>
  <div id="app">
    {{ items }}
    <vue-morph-table
      :fields.sync="fields"
      :items.sync="items"
      :actions="actions"
      alias="table"
      striped
      hover
      border
      sorter
      bulkAction
      :loading="load"
      :num-of-rows="[10, 20, 30, 50, 100]"
      pagination
      :items-length="items.length"
      @sort="sortHandle($event)"
      @changeCurrentPage="changeCurrentPage($event)"
      @changeNumOfRows="changeNumOfRows($event)"
      @clickRow="clickRow($event)"
    >
      <template #edit={item}>
        <td width="1%" @click.stop="edit(item)">edit</td>
      </template>
      <template #delete>
        <td width="1%">delete</td>
      </template>
    </vue-morph-table>
  </div>
</template>
