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
            <tr id="table_header">
                <th></th>
                <th>求人No</th>
                <th>区分</th>
                <th>企業名</th>
                <th>内容</th>
                <th>日付</th>
                <th>職種</th>
                <th>対象</th>
                <th>留学生</th>
                <th>障がい者</th>
                <th></th>
            </tr>
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
            <tr id="table_record">
                <td></td>
                <td width="22"><input v-model="job_offer_no" size="22"></td>
                <td width="15"><input v-model="district" size="15"></td>
                <td width="40"><input v-model="company_name" size="40"></td>
                <td width="15"><input v-model="content" size="15"></td>
                <td width="20"><input v-model="briefing_date" size="20"></td>
                <td width="40"><input v-model="occupation" size="40"></td>
                <td width="20"><input v-model="target" size="20"></td>
                <td width="10"><input v-model="international" size="10"></td>
                <td width="10"><input v-model="disability" size="10"></td>
                <td></td>
            </tr>
        </table>

    </div>
</template>

<script>
    export default {
        name: "briefing_list",
        props:{
            job_offer_no:Number,
            district:String,
            company_name:String,
            content:String,
            briefing_date:Date,
            occupation:String,
            target:String,
            international:String,
            disability:String,
        },
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