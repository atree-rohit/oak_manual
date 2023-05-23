<style scoped>
.table-of-contents-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border: 1px solid pink;
  padding: 1rem;
  border-radius: 1rem;
  /* width: 50%; */
}
.json-container{
    display:flex;
    flex-direction: column;
    margin: auto;
    overflow: auto;
    width: 100%;
    border: 1px solid blue;
    border-radius: 1rem;
}

.page-title{
    background: violet;
    padding: .5rem;
    font-size: 1.75rem;
    text-align: center;
}

.table{
    border-collapse: collapse;
}
.table th{
    padding: .25rem 1rem;
}
.table th, .table tr{
    border: 1px solid pink;
    padding: .25rem 1rem;
}
.table tr td:not(:has(table)){
    border: 1px solid pink;
}
.title-row{
    background: hsl(0, 100%, 75%);
    font-size: 1.25rem;
    font-weight: 600;
}
.align-center{
    text-align: center;
}

@media (prefers-color-scheme: dark) {
    .table th, .table tr{
        border: 1px solid green;
    }
}
</style>

<template>
  <div class="table-of-contents-container">
    <h1>Table of Contents</h1>
    <div class="json-container" v-for="(value, key1) in data" :key="key1">
        <div class="page-title" @click="selected_table = selected_table == key1 ? '' : key1">
            {{capatilizeWords(key1)}}
        </div>
        <div class="page-content" v-if="selected_table == key1">
            <table class="table">
                <thead>
                    <tr>
                        <th>Section</th>
                        <th>Page</th>
                    </tr>
                </thead>
                <tbody>
                    <tr
                        v-for="row in value"
                        :key="row.id"
                        :class="{'title-row': row.data == undefined}"
                    >
                        <td class="align-center">{{row.id}}</td>
                        <td :colspan="row.data == undefined ? 2 : 1">{{row.title}}</td>
                        <td v-if="row.data">
                            <table class="row-table">
                                <tbody>
                                    <table-row v-for="(data, key) in row.data" :data="data" :key="key"/>
                                </tbody>
                            </table>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import TableRow from './TableRow.vue'
import table_of_contents from '../assets/data/contents.json'

export default defineComponent({
  name: 'TableOfContents',
  components: {
    TableRow
  },
  data() {
    return {
        data: table_of_contents,
        selected_table: 'plantation_method'
    }
  },
  methods:{
    capatilizeWords(str: string){
        return this.replaceUnderscore(str).map((w) => this.capatilizeWord(w)).join(' ')
    },
    capatilizeWord(str: string){
        return str.charAt(0).toUpperCase() + str.slice(1);
    },
    replaceUnderscore(str: string){
        return str.replace(/_/g, ' ').split(" ");
    },
  }
})
</script>