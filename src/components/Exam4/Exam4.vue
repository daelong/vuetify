<template>
<v-app id="app">
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
      <tbody v-for="(item, index) in items"
          :key="index">
        <tr :class="{ odd : index % 2 === 0}" @click="() => {selectedItem = item; dialog = true;}">
          <td>{{ index+1 }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.brewery_type }}</td>
          <td>{{ item.country }}</td>
          <td>{{ item.website_url }}</td>
        </tr>
      </tbody>
    </template>
    </v-simple-table>
     <v-pagination
      v-model="page"
      :length="10"
    ></v-pagination>
    <exam-4-modal v-if="dialog" :item="selectedItem" v-model="dialog"></exam-4-modal>
  </div>
</v-app>
</template>

<script>
import API from './assets/scripts/api';
import Exam4Modal from './components/Exam4Modal.vue';

export default {
  name: 'App',
  components: {
    Exam4Modal
  },
  data(){
    return{
      items: [],
      page: 1,
      dialog: false,
      selectedItem: {},
    }
  },
  mounted() {
    this.fetchData();
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
        .then(res =>  this.items = res)
        .catch(error => console.log(error));
    },
    handleModalItem(item){
      this.selectedItem = item;
      this.dialog = true;
    }
  },
  watch:{
    page: function(){
      console.log(this.page);
      this.fetchData(this.page, 20);
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
.odd{
  background-color: #95afc0;
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