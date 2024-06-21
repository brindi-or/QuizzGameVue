<script>
export default {
    name:'Header',
    props: ['name']
}
</script>
<template>
    <div class="header">
        <h4>
            Good Luck : {{ name }} !!!
        </h4>
    </div>
</template>

<style>
.header{
  text-align: start;
}
.header h4{
  font-weight: bold;
  font-style: italic;
  color: purple;
}
</style>