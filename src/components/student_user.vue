<template>
    <div id="app">

        <!--header-->

        <table border="1" width="100%">
            <tr>
                <th>
                    <router-link to="/student_user">ユーザー管理</router-link>
                </th>
                <th>
                    <router-link to="/briefings_list">説明会管理</router-link>
                </th>
            </tr>
            <tr>
                <td colspan="2" class="colspan">
                    学生ユーザー一覧
<!--                    <input type="button" value="スプレッドシート更新" id="updateButton" style="position: absolute; right: 5%">-->
                </td>
            </tr>
        </table>
        <hr>

        <!--body-->

        <input type="text" v-model="searchWord" placeholder="キーワード検索">

        <table align="center">
            <thead>
            <tr>
                <th v-for="(value,key) in columns" @click="sortBy(key)">
                    {{value}}
                    <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
                </th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(student,index) in filteredStudents">
                <td v-for="(value,key) in columns">
                    <input v-model="students[index][key]">
                </td>
            </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
    export default {
        name: "student_user",
        data:function() {
            const columns = {
                student_number: '学籍番号',
                student_name: '氏名',
                student_sex: '性別',
                student_age: '年齢',
                student_belong: '所属',
                student_grade: '学年',
                student_status: '状況',
                student_emotion: '感情',
            };

            let sortOrders = {};
            Object.keys(columns).forEach(function (key) {
                sortOrders[key] = 1
            });

            return{
                students:[],
                columns:columns,
                searchWord:'',
                sortKey:'',
                sortOrders:sortOrders
            }
        },

        methods:{
            sortBy: function (key) {
                this.sortKey = key;
                this.sortOrders[key] = this.sortOrders[key] * -1;
            },
        },
        computed:{
            filteredStudents:function(){
                let data = this.students;

                let sortKey = this.sortKey;
                let order = this.sortOrders[sortKey] || 1;

                let filterWord = this.searchWord && this.searchWord.toLowerCase();

                if(filterWord){
                    data = data.filter(function (row) {
                        return Object.keys(row).some(function (key) {
                            return String(row[key]).toLowerCase().indexOf(filterWord) > -1
                        })
                    })
                }

                if(sortKey){
                    data = data.slice().sort(function (a,b) {
                        a = a[sortKey];
                        b = b[sortKey];
                        return (a === b ? 0 : a > b ? 1 : -1) * order;
                    })
                }
                return data;
            }
        },
        created(){
            let hoge = this;
            fetch('http://ec2-18-177-93-10.ap-northeast-1.compute.amazonaws.com/assignDB/student_all_post.php')
                .then(function(response) {
                    return response.json();
                })
                .then(function(res) {
                    console.log(res);
                    // let obj=JSON.parse(res);
                    // const obj_data = obj['data'];
                    const obj_data = res['data'];
                    console.log(obj_data);
                    obj_data.forEach(data => {
                        let student_item = {
                            student_number: data['student_number'],
                            student_slack_token: data['student_slack_token'],
                            student_name: data['student_name'],
                            student_sex: data['student_sex'],
                            student_age: data['student_age'],
                            student_belong: data['student_belong'],
                            student_grade: data['student_grade'],
                            student_status: data['student_status'],
                            student_emotion: data['student_emotion'],
                            student_login: data['student_login'],
                        };
                        // console.log(student_item)
                        hoge.students.push(student_item)
                    });

                })

        },

    }
</script>

<style scoped>
    table{
        border-collapse: collapse;
    }
    tr{
        border: solid 1px gray;
    }
</style>