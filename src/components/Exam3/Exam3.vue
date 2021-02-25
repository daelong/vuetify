<template>
  <div class="main">
    <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            index
          </th>
          <th class="text-left">
            Name
          </th>
          <th class="text-left">
            brewery_type
          </th>
          <th class="text-left">
            Country
          </th>
          <th class="text-left">
            website_url
          </th>
        </tr>
      </thead>
      <tbody  v-for="(item, index) in items"
          :key="index" @click="handleAlert(item)">
        <tr>
          <td>{{ index }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.brewery_type }}</td>
          <td>{{ item.country }}</td>
          <td>{{ item.website_url }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
  </div>
</template>

<script>
import API from './assets/scripts/api';

export default {
  name: 'App',
  components: {
  },
  data(){
    return{
      items: [],
      page: 1,
    }
  },
  mounted() {
    window.addEventListener('scroll', this.onScroll);
    this.fetchData();
  },
  destroyBefore() {
    window.removeEventListener('scroll', this.onScroll);
  },
  methods:{
    async fetchData(page, perPage){
      await API.fetchAPIData(page, perPage)
      .then(res => res.data)
      .then(data => data.map( data => {
        return {
          ...data,
          visible: true
          }
        }))
        .then(res =>  this.items = this.items.concat(res))
        .catch(error => console.log(error));
    },
    onScroll() {
        const docEl = document.documentElement;
        const top = docEl.scrollTop;
        const scrollHeight = docEl.scrollHeight;
        const clientHeight = docEl.clientHeight;
        // console.log(top, scrollHeight, scrollHeight - top, clientHeight);
        if (scrollHeight - top === clientHeight) {
          console.log('fetch');
          // scrolled to bottom
          this.page += 1;
          this.fetchData(this.page, 20);
        }
    },
    handleAlert(item){
      alert(`
      name: ${item.name}
      brewery_type: ${item.brewery_type}
      country: ${item.country}
      state: ${item.state}
      city: ${item.city}
      phone: ${item.phone}
      website_url: ${item.website_url}`);
    }
  }
};
</script>

<style scoped>
.main{
  width: 100%;
  margin: 20px 0 0 20px;
}
li{
  list-style: none;
}
.mx-auto{
  margin: 20px;
  width: 400px;
  height: 250px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.top-box{
  width: 100%;
  display: flex;
  justify-content: space-between;
}
.card-text{
  padding-left: 20px;
}
.btn{
  display: flex;
  justify-content: flex-end;
}
.foldedBox{
  height: 50px;
}
.folded{
  display: none;
}
</style>