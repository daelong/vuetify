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
      <tbody v-for="(item, index) in items"
          :key="index">
        <tr :class="{ odd : index % 2 === 0}" @click="handleModalItem(item)">
          <td>{{ index }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.brewery_type }}</td>
          <td>{{ item.country }}</td>
          <td>{{ item.website_url }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
    <exam-4-modal :modalItem="selectedItem" v-model="dialog"></exam-4-modal>
  </div>
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
        .then(res =>  this.items = this.items.concat(res))
        .catch(error => console.log(error));
    },
    handleModalItem(item){
      this.selectedItem = item;
      this.dialog = true;
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