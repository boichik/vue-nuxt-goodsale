<template>
    <div class="container">
        <LazyAppLoader v-if="loading"/>
        <LazyAppListItem v-else :items="products"/>
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
        name:'Search',
        async asyncData({$axios, route, redirect}){
            let item = null
            if(Object.keys(route.params).length !== 0){
                if(Object.keys(route.query).length !== 0){
                    item = await $axios.$get(`https://gorest.co.in/public-api/products?categories=${route.params.id}&page=${route.query.page}`,)
                }else{
                    item = await $axios.$get(`https://gorest.co.in/public-api/products?categories=${route.params.id}`)
                }
                console.log(item)
                console.log(route.params.id)
                return{
                    categoryId: route.params.id,
                    products: item.data,
                    pageNow: item.meta.pagination.page,
                    pageTotal: item.meta.pagination.pages,
                }
            }else{
                redirect('/');
            }
            

        },
        data:()=>({
            loading:true,
            products:[],
            pageNow:null,
            pageTotal:null,
            categoryId:null,
        }),
        mounted(){
            this.loading= false;
        },
        components:{
            Paginate: ()=> import('vuejs-paginate')
        },
        watch: {
            '$route'() {
                this.loading = true
                this.getProducts();
            },
        },
        methods:{
            async getProducts(){
            let id = this.$route.query.page;

            let item = await this.$axios.$get(`https://gorest.co.in/public-api/products?categories=${this.categoryId}${id > 0 ? `&page=${id}` : ''}`);

            this.products= item.data;
            this.pageNow= item.meta.pagination.page;
            this.pageTotal = item.meta.pagination.pages;
            this.loading = false;
            },
            pageChange(pageNum){
                this.$router.push(`/search/${this.categoryId}?page=${pageNum}`)
                this.loading=true
            }
        }
    }
</script>