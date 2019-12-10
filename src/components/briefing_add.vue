<template>
    <div id="app">
        <!--ヘッダー-->
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
                    <router-link to="/briefing_list">説明会管理</router-link>
                    &nbsp;&nbsp;&nbsp;
                    <router-link to="/calendar">カレンダー</router-link>
                    <router-link to="/briefing_add" style="position: absolute; right: 15%;">新規説明会追加</router-link>
                    <input type="button" value="スプレッドシート更新" id="updateButton" style="position: absolute; right: 5%">
                </td>
            </tr>
        </table>
        <hr>

        <!--body-->
        <div id="insert_data_area">
            <table>
                <tr v-for="(value,key,index) in row">
                    <th>{{value}}</th>
                    <td><input v-bind:key="key"></td>
                </tr>
                <input type="button" id="insert_data_btn" value="追加" @click="data_insert">
            </table>
        </div>

<!--        <div style="border: 1px solid #cccccc; padding: 10px;">-->
<!--            <table align="center">-->
<!--                <tr>-->
<!--                    <td width="22"><input v-model="job_offer_no" size="22" placeholder="求人No."></td>&lt;!&ndash;求人No.&ndash;&gt;-->
<!--                    <td width="15"><select v-model="district" name="district">&lt;!&ndash;区分 &ndash;&gt;-->
<!--                        <option disabled value="">区分</option>-->
<!--                        <option value="福岡校">福岡校</option>-->
<!--                        <option value="北九州校">北九州校</option>-->
<!--                    </select></td>-->
<!--                    <td width="40"><input v-model="company_name" size="40" placeholder="企業名"></td>  &lt;!&ndash; 企業名&ndash;&gt;-->
<!--                    <td width="15"><select v-model="content" name="Content">                    &lt;!&ndash;内容 &ndash;&gt;-->
<!--                        <option disabled value="">内容</option>-->
<!--                        <option value="説明会">説明会</option>-->
<!--                        <option value="セミナー">セミナー</option>-->
<!--                        <option value="OB会">OB会</option>-->
<!--                    </select></td>-->
<!--                    <td width="20"><input v-model="briefing_date" size="20"></td>&lt;!&ndash;開催日&ndash;&gt;-->
<!--                    <vuejs-datepicker v-model="briefing_date" ></vuejs-datepicker>-->
<!--                    <td width="40"><input type="text" size="40" placeholder="職種"></td>    &lt;!&ndash;職種 &ndash;&gt;-->
<!--                    <td width="20"><input type="text" size="20" placeholder="対象"></td>    &lt;!&ndash;対象 &ndash;&gt;-->
<!--                    <td width="10"><select name="International" id="International">        &lt;!&ndash;留学生 &ndash;&gt;-->
<!--                        <option disabled selected value>留学生</option>-->
<!--                        <option value="◯">◯</option>-->
<!--                        <option value="×">×</option>-->
<!--                    </select></td>-->
<!--                    <td width="10"><select name="Disability" id="Disability">        &lt;!&ndash;障がい者 &ndash;&gt;-->
<!--                        <option disabled selected value>障がい者</option>-->
<!--                        <option value="◯">◯</option>-->
<!--                        <option value="×">×</option>-->
<!--                    </select></td>-->
<!--                    <td></td>-->
<!--                </tr>-->
<!--            </table>-->
<!--        </div>-->
<!--        <div align="left" style="border: 2px solid #cccccc; padding: 10px; margin: 0 5% 5px 5%;">-->
<!--            <table>-->
<!--                <tr>-->
<!--                    <th>開催時間</th>-->
<!--                    <td>-->
<!--                        <select name="Start_time" id="Start_time">&lt;!&ndash; 開始時間&ndash;&gt;-->
<!--                            <option disabled selected value>&#45;&#45;&#45;&#45;</option>-->
<!--                            <option v-for="start_hour of time" v-bind:key="start_hour.value">-->
<!--                                {{start_hour.value}}-->
<!--                            </option>-->
<!--                        </select>-->
<!--                        <span> 〜 </span>-->
<!--                        <select name="last_time" id="last_time">&lt;!&ndash; 開始時間&ndash;&gt;-->
<!--                            <option disabled selected value>&#45;&#45;&#45;&#45;</option>-->
<!--                            <option v-for="last_hour of time" v-bind:key="last_hour.value">-->
<!--                                {{last_hour.value}}-->
<!--                            </option>-->
<!--                        </select>-->
<!--&lt;!&ndash;                        <select name="Last_time" id="Last_time">&ndash;&gt;-->
<!--&lt;!&ndash;                            <option disabled selected value>&#45;&#45;&#45;&#45;</option>&ndash;&gt;-->
<!--&lt;!&ndash;                            <option v-for="last_hour of time" v-bind:key="last_hour.value">&ndash;&gt;-->
<!--&lt;!&ndash;                                {{last_hour.value}}&ndash;&gt;-->
<!--&lt;!&ndash;                            </option>&ndash;&gt;-->
<!--&lt;!&ndash;                        </select>&ndash;&gt;-->
<!--                        <v-hour-minute></v-hour-minute>-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>開催場所</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Briefing_place" size="40"><br>&lt;!&ndash;開催場所&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>持参物</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Briefing_Bring" size="40"><br>&lt;!&ndash;持参物&ndash;&gt;-->

<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>説明会入力〆切</th>-->
<!--                    <td>-->
<!--                        <input type="date" name="Deadline_year" id="Deadline_year">&lt;!&ndash; 説明会入力〆切 &ndash;&gt; &lt;!&ndash;〆切年 &ndash;&gt;-->
<!--&lt;!&ndash;                        <vuejs-datepicker></vuejs-datepicker>&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>受験確認入力〆切</th>-->
<!--                    <td>-->
<!--                        <input type="date" name="Exam_year" id="Exam_year">&lt;!&ndash; 受験確認入力〆切 &ndash;&gt; &lt;!&ndash;〆切年 &ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>勤務地</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Work_Location" size="20">&lt;!&ndash;勤務地&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>説明会参加数</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Briefing_Number" size="10">&lt;!&ndash;説明会参加数&ndash;&gt; &lt;!&ndash; DBから読み込む &ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>受験参加数</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Exam_Number" size="10">&lt;!&ndash;受験参加数&ndash;&gt; &lt;!&ndash;DBから読み込む&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>内定数</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Offer_Number" size="10"> &lt;!&ndash;内定数&ndash;&gt; &lt;!&ndash;DBから読み込む&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--                <tr>-->
<!--                    <th>備考</th>-->
<!--                    <td>-->
<!--                        <input type="text" id="Briefing_Remarks" size="150">&lt;!&ndash;備考&ndash;&gt;-->
<!--                    </td>-->
<!--                </tr>-->
<!--            </table>-->
<!--        </div>-->
<!--        <input type="button" id="Briefing_Join" value="追加" style="position: absolute; right: 5%;">-->
    </div>
</template>

<script>
    export default {
        name: "briefing_add",
        data:function(){
            let row={
                joboffer_number:'求人No.',
                division:'区分',
                company_name:'企業名',
                content:'内容',
                event_date:'開催日時',
                occupation:'職種',
                target:'対象',
                international_flg:'留学生',
                disability_flg:'障がい者',
                start_time:'開始時間',
                finish_time:'終了時間',
                venue:'開催場所',
                bring_item:'持参物',
                briefing_deadline:'説明会〆切',
                exam_deadline:'受験〆切',
                workplace:'勤務地',
                briefing_number:'説明会参加者数',
                exam_number:'受験者数',
                offer_number:'内定数',
                supplementary:'備考',
            };
            return{
                row:row,
                briefing:[],
                time:[
                    {value:"8:00"},
                    {value:"9:00"},
                    {value:"10:00"},
                    {value:"11:00"},
                    {value:"12:00"},
                    {value:"13:00"},
                    {value:"14:00"},
                    {value:"15:00"},
                    {value:"16:00"},
                    {value:"17:00"},
                    {value:"18:00"},
                    {value:"19:00"},
                    {value:"20:00"},
                    {value:"21:00"},
                    {value:"22:00"},
                ]
            }
        },
        methods:{
            data_insert:function (array) {
                alert(
                    array.division + "\n" +
                    array.joboffer_number + "\n" +
                    array.event_date + "\n" +
                    array.start_time + "\n" +
                    array.finish_time + "\n" +
                    array.company_name + "\n" +
                    array.venue + "\n" +
                    array.occupation + "\n" +
                    array.content + "\n" +
                    array.bring_item + "\n" +
                    array.briefing_deadline + "\n" +
                    array.exam_deadline + "\n" +
                    array.workplace + "\n" +
                    array.briefing_number + "\n" +
                    array.exam_number + "\n" +
                    array.offer_number + "\n" +
                    array.target + "\n" +
                    array.international_flg + "\n" +
                    array.disability_flg + "\n" +
                    array.supplementary + "\n"
                )
            }
        }
    }
</script>

<style scoped>
    div #insert_data_area{
        border: 2px solid #cccccc;
        padding: 10px;
        margin: 0 5% 5px 5%;
    }
    input #insert_data_btn{
        margin-right: 5%;
    }

</style>