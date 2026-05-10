<template>
    <section class="score">
        Player <span>{{ playerScore }}</span> | Computer <span>{{ computerScore }}</span>
    </section>
</template>

<script>
export default {
    props: [
        'playerScore',
        'computerScore'
    ]
    
  
}
</script>

<style lang="scss">
    section.score{
        
        padding: 20px;
        border-bottom: 1px solid black; 
    }

    .score span{
        border: 1px solid gray;
        padding: 5px;
    }
</style>