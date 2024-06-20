<script>

export default {
    name:'Score',
    props:[
        'userScore',
        'computerScore'
    ] ,

    data(){
        return{
        }
    }
}
</script>

<template>
    <section class="score-section">
        Player <span class="score">{{userScore}}</span>*<span class="score">{{computerScore}}</span>Computer
    </section>
    <hr>
</template>

<style>
    h3{
        font-weight: 500; 
    }
    .score{
        border: 1px solid pink;
        padding: 5px;
    }
</style>