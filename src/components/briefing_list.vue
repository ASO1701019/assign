<template>
    <div id="app">
        <!--ヘッダー-->
        <table border="1" width="100%">
            <tr>
                <th>
                    <router-link to="/student_user">ユーザー管理</router-link>
                </th>
                <th>
                    <router-link to="/briefing_list">説明会管理</router-link>
                </th>
            </tr>
            <tr>
                <td colspan="2" class="colspan">
                    <router-link to="/briefing_list">説明会管理</router-link>
                    &nbsp;&nbsp;&nbsp;
                    <router-link to="/calendar">カレンダー</router-link>
                    <router-link to="/briefing_add" style="position: absolute; right: 15%;">新規説明会追加</router-link>
                    <input type="button" value="スプレッドシート更新" id="updateButton" style="position: absolute; right: 5%">
                </td>
            </tr>
        </table>
        <hr>
        <table align="center">
            <input type="text" v-model="searchWord" placeholder="キーワード検索">
            <thead>
            <tr>
                <th></th>
                <th v-for="(value,key) in columns" @click="sortBy(key)">
                    {{value}}
                    <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
                </th>
                <th></th>
            </tr>
            </thead>
            <tr id="table_search">
                <td width="10"><img src="../search.png"></td>
                <td width="22"><input v-model="job_offer_no" size="22" placeholder="求人No.検索"></td>
                <td width="15"><select v-model="district">
                    <option disabled value="">区分検索</option>
                    <option value="福岡校">福岡校</option>
                    <option value="北九州校">北九州校</option>
                </select></td>
                <td width="40"><input v-model="company_name" size="40" placeholder="企業名検索"></td>
                <td width="15"><select v-model="content">
                    <option disabled value="">内容検索</option>
                    <option value="説明会">説明会</option>
                    <option value="セミナー">セミナー</option>
                    <option value="OB会">OB会</option>
                </select></td>
                <td width="20"><input v-model="briefing_date" size="20"></td>
                <td width="40"><input v-model="occupation" size="40" placeholder="職種検索"></td>
                <td width="20"><input v-model="target" size="20" placeholder="対象検索"></td>
                <td width="10"><select v-model="international">
                    <option disabled value="">留学生</option>
                    <option value="◯">◯</option>
                    <option value="×">×</option>
                </select></td>
                <td width="10"><select v-model="disability">
                    <option disabled value="">障がい者</option>
                    <option value="◯">◯</option>
                    <option value="×">×</option>
                </select></td>
                <td></td>
            </tr>
<!--            <tr id="table_record">-->
<!--                <td></td>-->
<!--                <td width="22"><input v-model="job_offer_no" size="22"></td>-->
<!--                <td width="15"><input v-model="district" size="15"></td>-->
<!--                <td width="40"><input v-model="company_name" size="40"></td>-->
<!--                <td width="15"><input v-model="content" size="15"></td>-->
<!--                <td width="20"><input v-model="briefing_date" size="20"></td>-->
<!--                <td width="40"><input v-model="occupation" size="40"></td>-->
<!--                <td width="20"><input v-model="target" size="20"></td>-->
<!--                <td width="10"><input v-model="international" size="10"></td>-->
<!--                <td width="10"><input v-model="disability" size="10"></td>-->
<!--                <td></td>-->
<!--            </tr>-->
            <tbody>
            <tr id="table_record" v-for="task in filteredTasks">
                <td></td>
                <td v-for="(value,key) in columns">
                    {{task[key]}}
                </td>
                <td></td>
            </tr>
            </tbody>
        </table>

    </div>
</template>

<script>
    export default {
        name: "briefing_list",
        // props:{
        //     job_offer_no:Number,
        //     district:String,
        //     company_name:String,
        //     content:String,
        //     briefing_date:Date,
        //     occupation:String,
        //     target:String,
        //     international:String,
        //     disability:String,
        // },
        data:function () {
            let columns = {
                job_offer_no:'求人No.',
                district:'区分',
                company_name:'企業名',
                content:'内容',
                briefing_date:'開催日時',
                occupation:'職種',
                target:'対象',
                international:'留学生',
                disability:'障がい者',
            };
            let sortOrders  ={};
            Object.keys(columns).forEach(function (key) {
                sortOrders[key] = 1
            });

            return{
                columns:columns,
                searchWord:'',
                tasks:[
                    {
                        job_offer_no:100001,
                        district:'福岡',
                        company_name:'麻生情報ビジネス',
                        content:'セミナー',
                        briefing_date:'2019-11-01',
                        occupation:'SE',
                        target:'情報系',
                        international:'◯',
                        disability:'◯'
                    },
                    {
                        job_offer_no:100002,
                        district:'福岡',
                        company_name:'麻生情報ビジネス',
                        content:'セミナー',
                        briefing_date:'2019-10-01',
                        occupation:'SE',
                        target:'情報系',
                        international:'◯',
                        disability:'◯'
                    },
                    {
                        job_offer_no:100003,
                        district:'福岡',
                        company_name:'麻生情報ビジネス',
                        content:'セミナー',
                        briefing_date:'2019-12-01',
                        occupation:'SE',
                        target:'情報系',
                        international:'◯',
                        disability:'◯'
                    },
                ],
                sortKey:'',
                sortOrders:sortOrders
            }
        },
        methods: {
            sortBy: function (key) {
                this.sortKey = key;
                this.sortOrders[key] = this.sortOrders[key] * -1;
            }
        },
        computed:{
            filteredTasks:function(){
                let data = this.tasks;

                let sortKey = this.sortKey;
                let order = this.sortOrders[sortKey] || 1;

                let filterWord = this.searchWord && this.searchWord.toLowerCase();

                if(filterWord){
                    data  =data.filter(function (row) {
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
        }
    }
</script>

<style scoped>
    table{
        border-collapse: collapse;
        border-left: gray;
        border-right: gray;
    }
    tr#table_record{
        border-right: solid 1px gray;
        border-left: solid 1px gray;
        border-bottom: solid 1px gray;
    }
    tr#table_search{
        border: solid 1px gray;
    }
</style>