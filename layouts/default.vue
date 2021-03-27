<template>
  <div class="page">
    <Header/>
    <Nuxt />
    <Footer/>
  </div>
</template>
<script>
export default {
    components:{
      Header: ()=> import('../components/app/Header'),
      Footer: ()=> import('../components/app/Footer')
    }
}
</script>
<style>
html {
  font-family:
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
}

.page{
  display: grid;
  grid-template-rows: auto 1fr auto;
  min-height: 100vh;
}

</style>
