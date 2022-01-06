<template>
    <div class="container">
        <div class="heading">
            <h2 class="title">Shopping List</h2>
            <add-item-form v-on:reloadlist="getList()" />
        </div>
        <list-view :items="items" v-on:reloadlist="getList()" />
    </div>
</template>

<script>
import addItemForm from "./addItemForm.vue";
import listView from "./listView.vue";
export default {
    components: {
        addItemForm,
        listView,
    },
    data() {
        return {
            items: [],
        };
    },
    methods: {
        getList() {
            axios
                .get("api/items")
                .then((response) => (this.items = response.data))
                .catch((error) => console.error(error));
        },
    },
    created() {
        this.getList();
    },
};
</script>
<style scoped>
.container {
    font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
    width: 400px;
    margin: auto;
}

.heading {
    background: #e6e6e6;
    padding: 10px;
}

.title {
    text-align: center;
}
</style>
