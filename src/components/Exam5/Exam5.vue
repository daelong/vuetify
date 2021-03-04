<template>
  <div class="main">
    <v-app id="app">
    <v-data-table
    :headers="headers"
    :items="items"
    hide-default-footer
    >
     <template v-slot:item="{ item }">
            <tr class="row-color" @click="() => { selectedItem = item; dialog = true;}">
                <td>{{item.name}}</td>
                <td>{{item.brewery_type}}</td>
                <td>{{item.country}}</td>
                <td>{{item.website_url}}</td>
            </tr>
            </template>
    </v-data-table>
     <v-pagination
      v-model="page"
      :length="10"
    ></v-pagination>
    </v-app>
    <exam-4-modal v-if="dialog" :item="selectedItem" v-model="dialog"></exam-4-modal>
  </div>
</template>
name, brewery_type, country, state, city, phone, website_url
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
      headers: [
          {
            text: 'Name',
            align: 'start',
            value: 'name',
          },
          { text: 'Brewery_type', value: 'brewery_type' },
          { text: 'Country', value: 'country' },
          { text: 'Website_url', value: 'website_url' },
        ],
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
      console.log(item);
      console.log(this.selectedItem)
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
.row-color:nth-child(even){
  background-color: #bdc3c7;
}
</style>