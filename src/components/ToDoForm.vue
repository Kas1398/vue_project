<template>
    <form @submit="onSubmit">
        <label for="new-todo-input">What are you doning?</label>
        <input type="text"
            id="new-todo-input"
            name="new-todo"
            autocomplete="off"
            v-model="label"  />
        <button type="submit">More</button>
    </form>
</template>

<script>
    export default {
        methods: {
            onSubmit() {
                console.log("labelin arvo: ", this.label);
            },
        },
    data() {
        return {
            label: "",
        };
    },
    };
</script>