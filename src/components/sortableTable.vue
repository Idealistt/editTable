<template>
    <div ref="wrapper">
        <div :key="tableKey">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    import sortable from "sortablejs";
    export default {
        name: "SortableTable",
        data() {
            return {
                tableKey: 0
            };
        },
        methods: {
            makeTableSortAble() {
                const table = this.$children[0].$el.querySelector(
                    ".el-table__body-wrapper tbody"
                );
                sortable.create(table, {
                    animation: 150,
                    onEnd: ({ newIndex, oldIndex }) => {
                        this.keepWrapperHeight(true);
                        this.tableKey = Math.random();
                        const arr = this.$children[0].data;
                        const targetRow = arr.splice(oldIndex, 1)[0];
                        arr.splice(newIndex, 0, targetRow);
                        this.refrashFunction();
                    }
                });
            },
            keepWrapperHeight(keep) {
                const wrapper = this.$refs.wrapper;
                if (keep) {
                    wrapper.style.minHeight = `${wrapper.clientHeight}px`;
                } else {
                    wrapper.style.minHeight = `auto`;
                }
            }
        },
        mounted() {
            this.makeTableSortAble();
        },
        watch: {
            tableKey() {
                this.$nextTick(() => {
                    this.makeTableSortAble();
                    this.keepWrapperHeight(false);
                });
            }
        },
        props: ['refrash-function']
    };
</script>