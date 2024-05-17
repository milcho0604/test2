<template>
    <div id="BookListView">
      <h1>도서 목록</h1>
      <table>
        <tr><td>id</td><td>도서명</td><td>저자</td><td>가격</td><td>출판사</td><td>카테고리</td></tr>
        <tr v-for="book in books" v-bind:key="book.id" v-on:click="goEdit(book.id)">
          <td>{{ book.id }}</td>
          <td>{{ book.title }}</td>
          <td>{{ book.author }}</td>
          <td>{{ book.price }}</td>
          <td>{{ book.publisher}}</td>
          <td>{{ book.category }}</td>
        </tr>
      </table>
      <button type="button" @click="goEdit(0)">등록</button>
  
    </div>
  </template>
  
  <script>
  import { loadBooks } from '../bookService';
  
  export default {
    name: "BookListView",
    data() {
      return {
        books: [ ]
      }
    },
    async mounted() {
     this.books = await loadBooks();
    },
    methods: { 
    async reload(){
        this.products = await loadBooks();
      }, 
      goEdit(id) {
        this.$router.push("/edit/" + id);
      }
    }
  }
  </script>
  
  <style scoped>
  h1 { border-bottom: 1px solid gray; }
  button { padding: 5px 20px; margin-right: 250px; }
  table { border-collapse: collapse; margin: 20px 0; width: 100%; }
  tr:nth-child(1) { background-color: #eee; text-align: center; }
  td { border: 1px solid gray; padding: 6px; }
  td:nth-child(1) { text-align: center; width: 30px; }
  tr:hover { background-color: #ffd; cursor: pointer }
  </style>
  