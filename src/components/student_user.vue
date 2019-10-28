<template>
    <div id="app">
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
                    学生ユーザー一覧
                    <input type="button" value="スプレッドシート更新" id="updateButton" style="position: absolute; right: 5%">
                </td>
            </tr>
        </table>
        <hr>
        <table align="center">
            <tr id="header">
                <th></th>
                <th width="25">学籍番号</th>
                <th width="22">名前</th>
                <th width="15">性別</th>
                <th width="15">年齢</th>
                <th width="40">所属</th>
                <th width="15">学年</th>
                <th width="30">状況</th>
                <th>感情</th>
            </tr>
            <tr id="table_search">
                <td><img src="../search.png"></td>
                <td><input v-model.number="student_number" size="25" placeholder="学籍番号検索"></td>
                <td width="22"><input v-model="student_name" size="22" placeholder="名前検索"></td>
                <td width="15"><select v-model="student_sex">
                    <option disabled>性別</option>
                    <option>男</option>
                    <option>女</option>
                </select></td>
                <td width="15"><input v-model.number="student_age" size="15" placeholder="年齢検索"></td>
                <td width="40"><input v-model="student_department" size="40" placeholder="所属検索"></td>
                <td width="15"><input v-model.number="student_grade" size="15" placeholder="学年検索"></td>
                <td width="30"><input v-model="student_status" size="30" placeholder="状況検索"></td>
                <td><select v-model="student_emotion">
                    <option disabled selected value>感情</option>
                    <option value="良️">⭕️</option>
                    <option value="悪">✖︎</option>
                </select></td>
            </tr>
            <tr id="table_record">
                <td></td>
                <td width="25"><input type="text" size="25"></td>
                <td width="22"><input type="text" size="22"></td>
                <td width="15"><input type="text" size="15"></td>
                <td width="15"><input type="text" size="15"></td>
                <td width="40"><input type="text" size="40"></td>
                <td width="15"><input type="text" size="15"></td>
                <td width="35"><input type="text" size="35"></td>
                <td>⭕</td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: "student_user",
        props:{
            student_number:Number,
            student_name:String,
            student_sex:String,
            student_age:Number,
            student_department:String,
            student_grade:Number,
            student_status:String,
            student_emotion:String
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