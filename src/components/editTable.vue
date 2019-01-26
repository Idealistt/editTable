<template>
    <div>
        <div>
            <SortableTable :refrash-function="refrash">
                <el-table
                        :data="tableData"
                        style="width: 550px"
                        max-height="250">
                    <el-table-column
                            prop="name"
                            label="Name"
                            width="120">
                        <template slot-scope="scope">
                            <el-input v-model="scope.row.name" @change="refrash"></el-input>
                        </template>
                    </el-table-column>
                    <el-table-column
                            prop="value"
                            label="Value"
                            width="120">
                        <template slot-scope="scope">
                            <el-input v-model="scope.row.value" @change="refrash"></el-input>
                        </template>
                    </el-table-column>
                    <el-table-column
                            fixed="right"
                            label="Operations"
                            width="150px">
                        <template slot-scope="scope">
                            <el-button
                                    @click.native.prevent="deleteRow(scope.$index, tableData)"
                                    type="text"
                                    size="small">
                                Delete
                            </el-button>
                        </template>
                    </el-table-column>
                </el-table>
            </SortableTable>
        </div>
        <div>
            <el-row class="lf">
                <el-button type="success" plain @click.native.prevent="creatRow()">Input
                </el-button>
            </el-row>
        </div>
        <div>
            <el-input
                    type="textarea"
                    :rows="4"
                    placeholder="Please input"
                    v-model="jsonString"
                    @change="rerefrash">
            </el-input>
        </div>
        <el-row class="lf">
            <el-button type="primary" plain @click.native.prevent="download()" value="test.txt">Download
            </el-button>
        </el-row>
    </div>
</template>
<script>
    import SortableTable from './sortableTable'
    export default {
        components: {
            SortableTable
        },
        methods: {
            deleteRow(index, rows) {
                rows.splice(index, 1);
                this.jsonString = JSON.stringify(this.tableData);
            },
            creatRow() {
                this.tableData.unshift({name: '', value: ''});
                this.refrash();
            },
            refrash() {
                this.jsonString = JSON.stringify(this.tableData)
            },
            rerefrash() {
                this.tableData = JSON.parse(this.jsonString)
            },
            download() {
                let element = document.createElement('a');
                element.setAttribute('href', 'data:text/plain;charset=utf-8,' + encodeURIComponent(this.jsonString));
                element.setAttribute('download', 'logfile');
                element.style.display = 'none';
                document.body.appendChild(element);
                element.click();
                document.body.removeChild(element);
            },
        },
        data() {
            const tableData = [{name: 'Chuck Norris', value: 'increble'},
                {name: 'Bruce Lee', value: 9000},
                {name: 'Jackie Chan', value: 7000},
                {name: 'Jet Li', value: 8000},
                {name: 'Xin', value: 800}];
            return {
                tableData,
                jsonString: JSON.stringify(tableData),
            }
        }
    }
</script>
