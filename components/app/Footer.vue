<template>
    <footer class="footer">
        <div class="container">
                <div class="footer-block">
                    <div class="title">Бажаєте отримувати більше новин?</div>
                    <form action="post">
                        <div class="inputs">
                            <div class="input-field" :class="{invalid : error.email > 0, valid : error.email === 0}">
                                <label for="email">Email</label>
                                <input type="email" v-model="email" @input="InputEmail" placeholder="placeholder">
                                <span v-if="error.email === 3">Ведіть коректний емейл</span>
                                <span v-if="error.email === 1">Символів потрібно більше 2</span>
                                <span v-if="error.email === 2">Символів потрібно менше 100</span>
                            </div>
                            <div class="input-field" :class="{invalid : error.name > 0, valid : error.name === 0}">
                                <label for="name">Ваше ім’я</label>
                                <input type="text" @input="InputName" v-model="name" placeholder="placeholder">
                                <span v-if="error.name === 1">Символів потрібно більше 2</span>
                                <span v-if="error.email === 2">Символів потрібно менше 100</span>
                            </div>
                        </div>
                        <div @click="Send" class="btn-subscribe">
                            <p>підписатися</p>
                        </div>
                    </form>
                    <div class="logotipe">
                        <div class="logo">
                            <img src="~/assets/img/logo.png" alt="GoodSale Logo">
                        </div>
                        <div class="name">
                            <img src="~/assets/img/GOODSALE.png" alt="GoodSale Logo">
                        </div>
                    </div>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {
        name:'Footer',
        data:()=>({
            email:'',
            name:'',
            error: {
                name:null,
                email:null
            }
        }),
        methods:{
            InputName(e){   
                if(e.target.value.lenght < 100){
                    var re = /[А-Яа-яїЇіІёЁ'-]/gm;
                    var foo = e.target.value
                    foo = foo.match(new RegExp(re)) 
                    if(foo != null){
                        console.log(true)
                        this.name = foo.join('');
                    }else{
                        this.name = ''
                    }    
                }
            },
            InputEmail(e){
                if(e.target.value.lenght < 100){
                    var re = /^[A-Z0-9._%+-]+@[A-Z0-9-]+.+.[A-Z]{2,4}$/i;
                    var foo = e.target.value
                    foo = foo.match(new RegExp(re)) 
                    if(foo != null){
                        console.log(true)
                        this.email = foo.join('');
                    }else{
                        this.email = ''
                    } 
                }
                
            },
            checkValues(){
                this.name.length < 2 ? this.error.name = 1 : this.name.length > 100 ? this.error.name = 2 : this.error.name = 0;
                const regex = new RegExp(/^[A-Z0-9._%+-]+@[A-Z0-9-]+.+.[A-Z]{2,4}$/i)
                let result = regex.test(this.email)
                result === false ? this.error.email = 3 : this.email.length < 2 ? this.error.email = 1 : this.email.length > 100 ? this.error.email = 2 : this.error.email = 0
            },
            Send(){
              this.checkValues();
              if(this.error.email === 0 && this.error.name === 0){
                  alert('WOOOOOHOOOOO!!!')
              }  
            }
        }
    }
</script>

<style lang="scss" scoped>
    .footer{
        width: 100%;
        background: #363D41;

        .container{
            width:1346px;
            margin: 0 auto;
        }
        &-block{
            width: 100%;
            padding:41px 0 22px 0;
            display: flex;
            flex-direction: column;
            .title{
                width: 100%;
                font-family: Montserrat;
                font-style: normal;
                font-weight: 800;
                font-size: 24px;
                line-height: 29px;
                color:#FFFFFF;
                align-self: flex-start;
                border-bottom: 1px solid;
                padding-bottom: 8px;
            }
            form{
                padding-top: 15px;
                display: flex;
                justify-content: space-between;
                .inputs{
                    display: flex;
                }
                .input-field{
                    display: flex;
                    flex-direction: column;
                    width: 404px;
                    &.valid{
                        label{
                            color:greenyellow;
                        }
                        input{
                            color:greenyellow;
                            border-color: greenyellow;
                        }
                        span{
                            display: none;
                        }
                    }
                    &.invalid{
                        label{
                            color:red;
                        }
                        input{
                            border-color: red;
                        }
                        span{
                            display: block;
                            color:red;
                        }
                    }
                    &:first-child{
                        margin-right: 64px;
                    }
                    label{
                        margin-bottom: 8.22px;
                        font-family: 'Raleway', sans-serif;
                        font-style: normal;
                        font-weight: normal;
                        font-size: 12px;
                        line-height: 14px;

                        color: #FFFFFF;
                    }
                    span{
                        display: none;
                    }
                    input{
                        width: 100%;
                        height: 47px;
                        background: transparent;
                        border:1px solid #C4C4C4;
                        outline: none;
                        font-family: Raleway;
                        font-style: italic;
                        font-weight: normal;
                        font-size: 14px;
                        line-height: 16px;
                        color: #C4C4C4;
                        padding-left: 15px;
                        &::placeholder{
                            color: #C4C4C4;
                        }
                    }
                }
                .btn-subscribe{
                    cursor: pointer;
                    margin-top: 22px;
                    width: 210px;
                    height: 70px;
                    background: #CC9966;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                    transition: 0.3s;
                    &:hover{
                        background: #d3802d;
                    }
                    p{
                        font-family: 'Montserrat', sans-serif;
                        font-style: normal;
                        font-weight: 800;
                        font-size: 14px;
                        line-height: 17px;
                        display: flex;
                        align-items: center;
                        text-align: center;

                        color: #FFFFFF;
                    }
                }
            }
            .logotipe{
                display: flex;
                justify-content: center;
                margin-top: 29px;

                .logo{
                    width:100px;
                    height: 52px;
                    img{
                        width: 100%;
                        height: 100%;
                    }
                }
                .name{
                    width: 188px;
                    height: 22px;
                    align-self: center;
                    img{
                        width: 100%;
                        height: 100%;
                    }
                }
            }
        }
    }
    @media(max-width:1346px){
        .footer{
            .container{
                width: 95%;
            }
            &-block{
                form{
                    flex-direction: column;

                    .inputs{
                        flex-direction: row;
                        .input-field{
                            padding-top: 18px;
                            width: 100%;
                        }
                    }
                    .btn-subscribe{
                        margin-top: 42px;
                        align-self: center;
                        width: 175px;
                        height: 45px;
                    }
                }
                .logotipe{
                    margin-top: 42px;
                    .logo{
                        width: 70px;
                        height: 38px;
                    }
                    .name{
                        width: 134px;
                        height: 16px;
                    }
                }
            }
        }
    }
    @media (max-width:765px) {
        .footer{
            &-block{
                form{
                    .inputs{ flex-direction: column;}
                }
            }
        }
    }
</style>