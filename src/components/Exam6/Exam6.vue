<template>
  <div class="main">
    <v-app id="app">
    <v-data-table
    :headers="headers"
    :items="indexedItems"
    :items-per-page="30"
    hide-default-footer
    >
     <template v-slot:item="{ item }">
            <tr @click="() => { selectedItem = item; dialog = true;}">
                <td>{{item.index + 1}}</td>
                <td>{{item.name}}</td>
                <td>{{item.brewery_type}}</td>
                <td>{{item.country}}</td>
                <td>{{item.website_url}}</td>
            </tr>
            </template>
    </v-data-table>
     <v-dialog
      v-model="visible"
     width="700"
     height="500"
    >
    <template v-slot:activator="{ on, attrs }">
        <v-btn
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Open Dialog
        </v-btn>
      </template>
       <exam-6-input v-model="visible" @submit="onSubmit"></exam-6-input>
       </v-dialog>
    </v-app>
    <exam-4-modal v-if="dialog" :item="selectedItem" v-model="dialog"></exam-4-modal>
  </div>
</template>
name, brewery_type, country, state, city, phone, website_url
<script>
import API from './assets/scripts/api';
import Exam4Modal from './components/Exam4Modal.vue';
import Exam6Input from './components/Exam6Input';

export default {
  name: 'App',
  components: {
    Exam4Modal,
    Exam6Input
  },
  data(){
    return{
      items: [],
      dialog: false,
      visible: false,
      selectedItem: {},
      headers: [
         {
            text: 'Index',
            align: 'start',
            value: 'index',
          },
          {
            text: 'Name',
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
  computed:{
    indexedItems() {
        return this.items.map((item, index) => ({ ...item, index }));
      },
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
    handleModalItem(){
      console.log('hi');
    //  this.fetchData();
    },
    onSubmit(item){
      this.items.push(item);
      console.log(this.items)
    }
  },
};
</script>

<style scoped>
.main{
  width: 100%;
  /* margin: 20px 0 0 20px; */
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
.input-btn{
  float: left;
  width: 300px;
}
</style>