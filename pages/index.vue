<template>
  <div class="container">
      <LazyAppLoader v-if="loading"/>
      <LazyAppListItem v-if="!loading" :items="products"/>
      <paginate
        v-if="!loading"
        v-model="pageNow"
        :margin-pages="0"
        :page-count="pageTotal"
        :click-handler="pageChange"
        :page-range="3"
        :prev-text="'НАЗАД'"
        :next-text="'ВПЕРЕД'"
        :container-class="'pagination'"
        :page-class="'pagination__page-item'"
        :prev-class="'pagination__page-item prev'"
        :next-class="'pagination__page-item next'"
      />
  </div>
</template>

<script>
export default { 
   name:'Main',
   async asyncData({$axios, route}){
     let item = null
     if(Object.keys(route.query).length !== 0){
        item = await $axios.$get(`https://gorest.co.in/public-api/products?page=${route.query.page}`)
     }else{
       item = await $axios.$get('https://gorest.co.in/public-api/products')
     }
     return{
       products: item.data,
       pageNow: item.meta.pagination.page,
       pageTotal: item.meta.pagination.pages,
     }

   },
   data:()=>({
     loading:true,
     products:[],
     pageNow:null,
     pageTotal:null
   }),
   mounted(){
     this.loading= false;
   },
   watch: {
      '$route'() {
          this.loading = true
          this.getProducts();
      },
    },
   components:{
      Paginate: ()=> import('vuejs-paginate'),
   },
   methods:{
     async getProducts(){
      let id = this.$route.query.page;
      let item = await this.$axios.$get(`https://gorest.co.in/public-api/products?page=${id}`);

      this.products= item.data;
      this.pageNow= item.meta.pagination.page;
      this.pageTotal = item.meta.pagination.pages;
      this.loading = false;
     },
     pageChange(pageNum){
       this.$router.push(`/?page=${pageNum}`)
     }
   }

}
</script>
