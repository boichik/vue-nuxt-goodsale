<template>
    <header class="header">
        <nuxt-link to="/" class="header-block">
            <div class="header-block__logo">
                <img src="~/assets/img/logo.png" alt="GoodSale Logo">
            </div>
            <div class="header-block__name">
                <img src="~/assets/img/GOODSALE.png" alt="GoodSale Logo">
            </div>
        </nuxt-link>
    </header>
</template>

<script>
    export default {
        name:'Header'
    }
</script>

<style lang="scss" scoped>
    .header{
        widows: 100%;
        height: 112px;
        background: #363D41;
        
        &-block{
            max-width: 1346px;
            height: 100%;
            margin: auto;
            display: flex;
            justify-content: center;
            align-items: center;
            &__logo{
                max-width: 136px;
                max-height: 72px;
                img{
                    width: 100%;
                }
            }
            &__name{
                width:260px;
                height: 30px;
                img{
                    width: 100%;
                    height: 100%;
                }
            }
        }
    }
    @media (max-width:480px){
        .header{
            height: 70px;
            &-block{
                &__logo{
                    width: 70px;
                    height: 38px;
                }
                &__name{
                    width: 134px;
                    height: 16px;
                }
            }
        }
    }
</style>