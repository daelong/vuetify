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
        <tr class="row-color">
            <td @click="() => { selectedItem = item; dialog.modal = true;}">{{item.index + 1}}</td>
            <td @click="() => { selectedItem = item; dialog.modal = true;}">{{item.name}}</td>
            <td @click="() => { selectedItem = item; dialog.modal = true;}">{{item.brewery_type}}</td>
            <td @click="() => { selectedItem = item; dialog.modal = true;}">{{item.country}}</td>
            <td @click="() => { selectedItem = item; dialog.modal = true;}">{{item.website_url}}</td>
            <td><v-btn
                  @click="() => { selectedItem = item; dialog.update = true;}"
                  class="btn"
                  color="primary"
                >
                  Edit
                </v-btn>
            </td>
             <td><v-btn
              @click="items.splice(item.index,1)"
              class="btn"
              color="primary"
            >
              Delete
            </v-btn>
            </td>
        </tr>
      </template>
    </v-data-table>
    <v-dialog
      v-model="dialog.input"
     width="700"
     height="500"
    >
    <template v-slot:activator="{ on, attrs }">
      <div class="btn-box">
        <v-btn
          class="btn"
          color="primary"
          dark
          v-bind="attrs"
          v-on="on"
        >
          Add Item
        </v-btn>
        </div>
      </template>
       <exam-7-input v-model="dialog.input" @submit="onSubmit"></exam-7-input>
       </v-dialog>
    </v-app>
    <exam-7-modal v-if="dialog.modal" :item="selectedItem" v-model="dialog.modal"></exam-7-modal>
    <exam-7-update v-if="dialog.update" :item="selectedItem" v-model="dialog.update"></exam-7-update>
  </div>
</template>

<script>
import API from './assets/scripts/api';
import Exam7Modal from './components/Exam7Modal.vue';
import Exam7Input from './components/Exam7Input';
import Exam7Update from './components/Exam7Update';

export default {
  name: 'App',
  components: {
    Exam7Modal,
    Exam7Input,
    Exam7Update
  },
  data(){
    return{
      items: [],
      dialog: { 
        modal: false,
        input: false,
        update: false
        },
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
          {},
          {}
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
    },
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
.btn-box{
  display: flex;
  justify-content: flex-end;
  width: 100%;
}
.btn{
  width: 10%;
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
.row-color:nth-child(even){
  background-color: #bdc3c7;
}
</style>