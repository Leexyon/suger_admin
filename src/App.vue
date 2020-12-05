<template>
    <div id="cec">
        <a-table :columns="columns" :data-source="data">
            <a slot="name" slot-scope="text">{{ text }}</a>
            <span slot="customTitle">
                <a-icon type="smile-o" /> Name</span>
            <span slot="tags" slot-scope="tags">
                <a-tag v-for="tag in tags" :key="tag" :color="tag === 'loser' ? 'volcano' : tag.length > 5 ? 'geekblue' : 'green'">
                    {{ tag.toUpperCase() }}
                </a-tag>
            </span>
            <span slot="action" slot-scope="text, record">
                <a>Invite 一 {{ record.name }}</a>
                <a-divider type="vertical" />
                <a>Delete</a>
                <a-divider type="vertical" />
                <a class="ant-dropdown-link"> More actions
                    <a-icon type="down" /> </a>
            </span>
        </a-table>
    </div>
</template>
<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import menu from './components/menu';
import echars from './components/echars';
import $axios from 'axios';
const columns = [
  {
    dataIndex: 'name',
    key: 'name',
    slots: { title: 'customTitle' },
    scopedSlots: { customRender: 'name' },
  },
  {
    title: 'Age',
    dataIndex: 'age',
    key: 'age',
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
    scopedSlots: { customRender: 'tags' },
  },
  {
    title: 'Action',
    key: 'action',
    scopedSlots: { customRender: 'action' },
  },
];

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
@Component({
    components: {
        Menu: menu,
        Echars: echars,
    },
})
export default class App extends Vue {
    public option: any = {
        id: 123456,
        name: '我的名字',
        option: [{
            id: {
                id: 1,
            },
        }, ],
    };
    public data=data 
    public columns = columns
    public tableData = [{
        date: '2016-05-02',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1518 弄'
    }, {
        date: '2016-05-04',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1517 弄'
    }, {
        date: '2016-05-01',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1519 弄'
    }, {
        date: '2016-05-03',
        name: '王小虎',
        address: '上海市普陀区金沙江路 1516 弄'
    }]
    private test: string = '20';

    get testGetter() {
        return 'test';
    }

    public tianji() {
        this.option.option[0].id.id++;
    }

    public add() {
        const formDataPr = new FormData();

        formDataPr.append('username', 'damin');

        // $axios.get('/api/test')
        //     .then(function(response) {
        //         console.log(response);
        //     })
        //     .catch(function(error) {
        //         console.log(error);
        //     });
        // var xhr = new XMLHttpRequest();
        // xhr.withCredentials = true;
        // xhr.open('post', '/target/knowledge_graph/test');
        // xhr.send({user:'123'});
        fetch('/api/test', { method: 'get' })
            .then((response) => {
                response.text();
            })
            .then((response) => {
                console.log(response);
            })
            .catch((ret) => {
                console.log(ret);
            });

    }
}
</script>
<style lang="scss">
</style>