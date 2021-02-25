<template>
  <div class="main">
  <ul>
      <li v-for="(item, index) in items" :key="index">
        <v-card
          class="mx-auto"
          max-width="344"
          :class="{ folded: !item.visible }"
        >
        <div class="top-box">
           <v-card-title class="card-text">
              {{ item.name }}
            </v-card-title>
            <div class="btn">
              <v-btn depressed @click="item.visible = !item.visible">
                접기
              </v-btn>
            </div>
        </div>
        <div :class="{ hide : !item.visible }">
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
          </div>
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
.folded{
  height: 50px;
}
.hide{
  display: none;
}
</style>