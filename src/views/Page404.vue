<template>
<div class="page-404"> 
  <img class="img-404" src="../assets/404-error.jpg" alt="">
  <h1 class="txt-404">404 - page not found</h1>
</div>
</template>

<script>
export default {

}
</script>

<style>

.page-404{
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.img-404{
  width: 60%;
  height: 60vh;
}

.txt-404{
  display: none;
  color: #6c0404;
}

@media(max-width: 700px){
  .img-404{
    display: none;
  }

  .txt-404{
    display: block;
  }
}
</style>