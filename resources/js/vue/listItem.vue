<template>
    <div class="ListItem">
        <input
            type="checkbox"
            @change="updateCheck()"
            v-model="item.completed"
        />
        <span :class="[item.completed ? 'completed' : '', 'itemText']">{{
            item.name
        }}</span>
        <button @click="removeItem()" class="trashcan">
            <font-awesome-icon icon="trash" />
        </button>
    </div>
</template>

<script>
export default {
    props: ["item"],
    methods: {
        updateCheck() {
            axios
                .put("api/item/" + this.item.id, {
                    item: this.item,
                })
                .then((response) => {
                    if (response.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch((error) => console.error(error));
        },
        removeItem() {
            axios
                .delete("api/item/" + this.item.id)
                .then((response) => {
                    if (response.status == 200) {
                        this.$emit("itemchanged");
                    }
                })
                .catch((error) => console.error(error));
        },
    },
};
</script>
<style scoped>
.completed {
    text-decoration: line-through;
    color: #999999;
}
.itemText {
    width: 100%;
    margin-left: 20px;
}
.ListItem {
    display: flex;
    align-items: center;
    justify-content: center;
}
.trashcan {
    background: #e6e6e6;
    border: none;
    color: red;
    outline: none;
    font-size: 1.25rem;
}
</style>
