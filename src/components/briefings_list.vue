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
                    <router-link to="/briefings_list">説明会管理</router-link>
                    &nbsp;&nbsp;&nbsp;
                    <router-link to="/calendar">カレンダー</router-link>
                    <router-link to="/briefing_add" style="position: absolute; right: 15%;">新規説明会追加</router-link>
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
                <th v-for="(value , key) in columns" @click="sortBy(key)">
                    {{value}}
                    <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'"></span>
                </th>
                <th></th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(briefing,index) in filteredBriefings">
                <td v-for="(value,key) in columns">
                    <input v-model="briefings[index][key]">
                </td>
                <td>
                    <button v-on:click="click_update(briefing)">更新</button>
                </td>
            </tr>
            </tbody>
        </table>
        <!--{{briefings}}-->
    </div>
</template>

<script>
    export default {
        name: "briefings_list",
        data:function(){
            let columns = {
                joboffer_number:'求人No.',
                division:'区分',
                company_name:'企業名',
                content:'内容',
                event_date:'開催日時',
                occupation:'職種',
                target:'対象',
                international_flg:'留学生',
                disability_flg:'障がい者',
            };
            let sortOrders = {};
            Object.keys(columns).forEach(function (key) {
                sortOrders[key] = 1
            });
            return {
                briefings:[],
                columns:columns,
                searchWord:'',
                sortKey:'',
                sortOrders:sortOrders,
            }
        },
        methods:{
            sortBy: function (key) {
                this.sortKey = key;
                this.sortOrders[key] = this.sortOrders[key] * -1;
            },
            click_update:function (array) {
                alert(array.event_number + "番目を更新します");
                let update_briefing = {
                    event_number:array.event_number,
                    division:array.division,
                    joboffer_number:array.joboffer_number,
                    event_date:array.event_date,
                    start_time:array.start_time,
                    finish_time:array.finish_time,
                    company_name:array.company_name,
                    venue:array.venue,
                    occupation:array.occupation,
                    content:array.content,
                    bring_item:array.bring_item,
                    briefing_deadline:array.briefing_deadline,
                    exam_deadline:array.exam_deadline,
                    workplace:array.workplace,
                    briefing_number:array.briefing_number,
                    exam_number:array.exam_number,
                    offer_number:array.offer_number,
                    target:array.target,
                    international_flg:array.international_flg,
                    disability_flg:array.disability_flg,
                    supplementary:array.supplementary,
                };
                console.log(update_briefing);
                const json_data = JSON.stringify(update_briefing);
                fetch('http://ec2-18-177-93-10.ap-northeast-1.compute.amazonaws.com/assignDB/event/event_update.php',{
                    method:'POST',
                    body:json_data,
                    headers:{'Content-Type':'application'}
                })
                    .then(function (response){
                        return response.json();
                    })
                    .then(function (data) {
                        console.log(data);
                    })
                    .catch(function (error) {
                        console.log(error)
                    })
            },
        },
        computed:{
            filteredBriefings:function(){
                let data = this.briefings;

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
            fetch('http://ec2-18-177-93-10.ap-northeast-1.compute.amazonaws.com/assignDB/all_post.php')
                .then(function(response) {
                    return response.json();
                })
                .then(function(res) {
                    const obj_data = res['data'];
                    console.log(obj_data);
                    obj_data.forEach(data => {
                        let briefing_item = {
                            event_number: data['event_number'],
                            finish_flg: data['finish_flg'],
                            division: data['division'],
                            joboffer_number: data['joboffer_number'],
                            event_date:data['event_date'],
                            start_time:data['start_time'],
                            finish_time: data['finish_time'],
                            company_name:data['company_name'],
                            venue:data['venue'],
                            occupation:data['occupation'],
                            content:data['content'],
                            bring_item:data['bring_item'],
                            briefing_deadline:data['briefing_deadline'],
                            exam_deadline:data['exam_deadline'],
                            workplace:data['workplace'],
                            briefing_number:data['briefing_number'],
                            exam_number:data['exam_number'],
                            offer_number:data['offer_number'],
                            target:data['target'],
                            international_flg:data['international_flg'],
                            disability_flg:data['disability_flg'],
                            supplementary:data['supplementary'],
                            update_date:data['update_date'],
                        };
                        hoge.briefings.push(briefing_item)
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