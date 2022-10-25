<template>
    <h1>Test Page</h1>
    <p>{{ aaa }}</p>
</template>

<script>
export default {
    data: function() {
        return { 
            aaa: 'ABC' 
        }
    },
    mounted: function() {
        // reload 後不會不見，除非手動replace掉
        console.log(history.state);
        history.replaceState({ ...history.state, userName: 'Jack'}, '');
        console.log(history.state);
    }
}
</script>