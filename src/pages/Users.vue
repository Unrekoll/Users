<template>
  <div class="wrapper-content wrapper-content--fixed">
    <section>
      <div class="container">
        <table>
          <thead>
            <tr>
              <th @click="sort('name')">Name &#8595;</th>
              <th @click="sort('age')">Age &#8595; </th>
              <th @click="sort('gender')">Gender &#8595;</th>
            </tr>
          </thead>

          <tbody>
            <tr v-for="user in usersSort" :key="user.id">
              <td>{{ user.name }}</td>
              <td>{{ user.age }}</td>
              <td>{{ user.gender }}</td>
            </tr>
          </tbody>
        </table>
          <p style="text-align:center;">
            <span> debug:sort: {{currentSort}},dir: {{currentSortDir}}</span>
            <p>page: {{this.page.current}}, length: {{this.page.length}} </p>
      </div>
    </section>
    <section>
      <div class="container">
        <div class="button-list">
          <div class="btn btnPrimary" @click='prevPage'>&#8592;</div>
          <div class="btn btnPrimary" @click='nextPage'>&#8594;</div>
        </div>
      </div>
    </section>
  </div>
</template>


<script>
import axios from 'axios'
export default {
  data() {
    return {
      users: [
        {"name": "Alpha", "age":19, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"male"},
        {"name": "Beta", "age":22, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"male"},
        {"name": "Gamma", "age":23, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"female"},
        {"name": "Axios", "age":25, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"female"},
        {"name": "Dzen", "age":22, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"male"},
        {"name": "Thor", "age":28, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"male"},
        {"name": "Ralf", "age":27, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"female"},
        {"name": "Rit", "age":26, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"female"},
        {"name": "Akva", "age":20, "img":"https://tocode.ru/static/c/vue-pro/assets/userCRM/1.jpg","gender":"male"}
      ],
      currentSort: 'name',
      currentSortDir: "asc",
      page: {
        current: 1,
        length: 4
      }
    };
  },
  computed: {
    usersSort () {
      return this.users.sort((a,b)=>{
        let mod = 1
        if (this.currentSortDir === 'desc') mod = -1
        if (a[this.currentSort] < b [this.currentSort]) return -1 * mod 
        if (a[this.currentSort] < b [this.currentSort]) return 1 * mod 
        return 0
      }).filter((row,index) => {
        let start = (this.page.current -1)*this.page.length
        let end = this.page.current * this.page.length
        if (index >= start && index < end) return true
      })
    }
  },
  methods: {
    sort (e) {
      if (e === this.currentSort) {
        this.currentSortDir = this.currentSortDir === 'asc' ? 'desc': 'asc'
      }
      this.currentSort = e
    },
    prevPage () {
      if(this.page.current > 1) this.page.current-=1
    },
    nextPage () {
      if((this.page.current * this.page.length) < this.users.length) this.page.current+=1
    }
  }
};
</script>

<style lang="scss" scoped>
img {
  width: 60px;
  height: auto;
  border-radius: 50%;
  margin-right: 16px;
}
.button-list {
  width: 100%;
  text-align: center;

  .btn {
    border-radius: 60px;
    margin: 0 20px;
  }
}

</style>