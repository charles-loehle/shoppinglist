<template>
    <div class="App container">
        <div class="flex flex-jcc flex-aic flex-dir-col">
            <div class="heading">
                <h2 class="title">Shopping List</h2>
                <div class="form-container">
                    <add-item-form v-on:reloadlist="getList()" />
                </div>
            </div>
            <list-view :items="items" v-on:reloadlist="getList()" />
        </div>
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
.heading {
    background: #e6e6e6;
}

.title {
    text-align: center;
}
</style>
