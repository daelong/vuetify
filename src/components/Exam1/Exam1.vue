<template>
  <div class="main">
    <ul>
      <li v-for="(item, index) in items" :key="index">
        <v-card
          class="mx-auto"
          max-width="344"
        >
        <div class="top-box">
           <v-card-title class="card-text">
              {{ item.name }}
            </v-card-title>
            <div class="btn">
              <v-btn depressed @click="item.visible = !item.visible">
                닫기
              </v-btn>
            </div>
        </div>
          <v-card-text>
            <p class="display-1 text--primary">
              brewery_type: {{ item.brewery_type}}
            </p>
            <p class="display-1 text--primary">
              country: {{ item.country}}
            </p>
          </v-card-text>
          <v-card-actions>
            <v-btn
              text
              color="deep-purple accent-4"
            >
              {{ item.website_url }}
            </v-btn>
          </v-card-actions>
        </v-card>
      </li>
    </ul>
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
      datalist: []
    }
  },
  computed:{
    items(){
      return this.datalist.filter(item => item.visible);
    }
  },
  mounted(){
    this.fetchDate();
  },
  methods:{
    async fetchDate(){
      await API.fetchAPIData()
      .then(res => res.data)
      .then(data => data.map( data => {
        return {
          ...data,
          visible: true
          }
        }))
        .then(data => this.datalist = data)
        .catch(error => console.log(error));
      
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
  float: left;
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
</style>