<template>
    <h3>可伸缩列（原始配置）</h3>
    <a-table :columns="columns" :data-source="data" :pagination="false" @resizeColumn="handleResizeColumn">
        <template #headerCell="{ column }">
            <template v-if="column.key === 'name'">
                <span>
                    <smile-outlined />
                    Name
                </span>
            </template>
        </template>

        <template #bodyCell="{ column, record }">
            <template v-if="column.key === 'name'">
                <a>
                    {{ record.name }}
                </a>
            </template>
            <template v-else-if="column.key === 'tags'">
                <span>
                    <a-tag v-for="tag in record.tags" :key="tag" :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'">
                        {{ tag.toUpperCase() }}
                    </a-tag>
                </span>
            </template>
            <template v-else-if="column.key === 'action'">
                <span>
                    <a>Invite 一 {{ record.name }}</a>
                    <a-divider type="vertical" />
                    <a>Delete</a>
                    <a-divider type="vertical" />
                    <a class="ant-dropdown-link">
                        More actions
                        <down-outlined />
                    </a>
                </span>
            </template>
        </template>
    </a-table>

    <h3 style="margin-top:24px">固定宽度表格（所有宽度为定值）</h3>
    <a-table :columns="fixedColumns" :data-source="data" :pagination="false" @resizeColumn="handleResizeColumn">
        <template #headerCell="{ column }">
            <template v-if="column.key === 'name'">
                <span>
                    <smile-outlined />
                    Name
                </span>
            </template>
        </template>

        <template #bodyCell="{ column, record }">
            <template v-if="column.key === 'name'">
                <a>
                    {{ record.name }}
                </a>
            </template>
            <template v-else-if="column.key === 'tags'">
                <span>
                    <a-tag v-for="tag in record.tags" :key="tag" :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'">
                        {{ tag.toUpperCase() }}
                    </a-tag>
                </span>
            </template>
            <template v-else-if="column.key === 'action'">
                <span>
                    <a>Invite 一 {{ record.name }}</a>
                    <a-divider type="vertical" />
                    <a>Delete</a>
                    <a-divider type="vertical" />
                    <a class="ant-dropdown-link">
                        More actions
                        <down-outlined />
                    </a>
                </span>
            </template>
        </template>
    </a-table>

    <h3 style="margin-top:24px">固定宽度对比表格（其中任意一列不指定宽度）</h3>
    <a-table :columns="fixedColumns2" :data-source="data" :pagination="false" @resizeColumn="handleResizeColumn">
        <template #headerCell="{ column }">
            <template v-if="column.key === 'name'">
                <span>
                    <smile-outlined />
                    Name
                </span>
            </template>
        </template>

        <template #bodyCell="{ column, record }">
            <template v-if="column.key === 'name'">
                <a>
                    {{ record.name }}
                </a>
            </template>
            <template v-else-if="column.key === 'tags'">
                <span>
                    <a-tag v-for="tag in record.tags" :key="tag" :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'">
                        {{ tag.toUpperCase() }}
                    </a-tag>
                </span>
            </template>
            <template v-else-if="column.key === 'action'">
                <span>
                    <a>Invite 一 {{ record.name }}</a>
                    <a-divider type="vertical" />
                    <a>Delete</a>
                    <a-divider type="vertical" />
                    <a class="ant-dropdown-link">
                        More actions
                        <down-outlined />
                    </a>
                </span>
            </template>
        </template>
    </a-table>
</template>
<script lang="ts" setup>
import { ref } from 'vue';
import { SmileOutlined, DownOutlined } from '@ant-design/icons-vue';
import type { TableColumnsType } from 'ant-design-vue';

const data = [
    {
        key: '1',
        name: 'John Brown',
        age: 32,
        address: 'New York No. 1 Lake Park',
        tags: ['nice', 'developer'],
    },
    {
        key: '2',
        name: 'Jim Green',
        age: 42,
        address: 'London No. 1 Lake Park',
        tags: ['loser'],
    },
    {
        key: '3',
        name: 'Joe Black',
        age: 32,
        address: 'Sidney No. 1 Lake Park',
        tags: ['cool', 'teacher'],
    },
];

const columns = ref<TableColumnsType>([
    {
        dataIndex: 'name',
        key: 'name',
        resizable: true,
        width: 150,
    },
    {
        title: 'Age',
        dataIndex: 'age',
        key: 'age',
        resizable: true,
        width: 100,
        minWidth: 100,
        maxWidth: 200,
    },
    {
        title: 'Address',
        dataIndex: 'address',
        key: 'address',
    },
    {
        title: 'Tags',
        key: 'tags',
        dataIndex: 'tags',
    },
    {
        title: 'Action',
        key: 'action',
    },
]);

// 固定宽度配置：为每列指定定值宽度
const fixedColumns = ref<TableColumnsType>([
    {
        dataIndex: 'name',
        key: 'name',
        resizable: true,
        width: 150,
    },
    {
        title: 'Age',
        dataIndex: 'age',
        key: 'age',
        resizable: true,
        width: 100,
        minWidth: 100,
        maxWidth: 200,
    },
    {
        title: 'Address',
        dataIndex: 'address',
        key: 'address',
        width: 200,
    },
    {
        title: 'Tags',
        key: 'tags',
        dataIndex: 'tags',
        width: 220,
    },
    {
        title: 'Action',
        key: 'action',
        width: 250,
    },
]);

// 固定宽度对比配置：为每列指定定值宽度，其中任意一列不指定
const fixedColumns2 = ref<TableColumnsType>([
    {
        dataIndex: 'name',
        key: 'name',
        resizable: true,
        width: 150,
    },
    {
        title: 'Age',
        dataIndex: 'age',
        key: 'age',
        resizable: true,
        width: 100,
        minWidth: 100,
        maxWidth: 200,
    },
    {
        title: 'Address',
        dataIndex: 'address',
        key: 'address',
        // width: 200,
    },
    {
        title: 'Tags',
        key: 'tags',
        dataIndex: 'tags',
        width: 220,
    },
    {
        title: 'Action',
        key: 'action',
        width: 250,
    },
]);
function handleResizeColumn(w, col) {
    col.width = w;
}
</script>
