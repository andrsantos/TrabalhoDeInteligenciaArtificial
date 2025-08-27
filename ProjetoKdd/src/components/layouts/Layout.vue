<script setup></script>

<template>

 <header>
    <div class="header-container">
        <h3 class="text-gradient">Sobre o projeto</h3>
        <h3 class="text-gradient">Bot no telegram</h3>
    </div>
  
 </header>

 <main>
  <slot/>
 </main>

 <footer>
   <small>Created by Andrey Santos, Bryan Young and Mayara Lima</small>
 </footer>
</template>

<style scoped>
.header-container{
    display: flex;
    justify-content: start;
    padding: 20px;
    margin-right: 2px;
}
</style>
