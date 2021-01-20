<template>
    <div class="main shadow-lg">
        <div class="myContent">
            <h3 class="title">
                آزمون بعدی
            </h3>
            <div class="addNew" dir="rtl" data-toggle="modal" data-target="#exampleModal">
                آزمون جدید
            </div>
            <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document" dir="rtl">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">آزمون جدید</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">نام آزمون</span>
                        </div>
                        <input id="name" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">توضیحات</span>
                        </div>
                        <input id="desc" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">زمان آزمون</span>
                        </div>
                        <input type="date" name="dateofbirth" id="date">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">تعداد پیمانه</span>
                        </div>
                        <input id="peymane" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="line"></div>
                    <div class="lessons">
                        <div class="lesson" v-for="index in this.lessons" :key="index">
                            <h3>
                                {{
                                    index.fa
                                }}
                            </h3>
                            <div class="input-group mb-3">
                                <div class="input-group-prepend">
                                    <span class="input-group-text" id="">بودجه بندی صفحات</span>
                                </div>
                                <input :id="index.en + '0'" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                            </div>
                            <div class="input-group mb-3">
                                <div class="input-group-prepend">
                                    <span class="input-group-text" id="">بودجه بندی فصلی</span>
                                </div>
                                <input :id="index.en + '1'" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                            </div>
                            <div class="input-group mb-3">
                                <div class="input-group-prepend">
                                    <span class="input-group-text" id="">هدف</span>
                                </div>
                                <input :id="index.en + '2'" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                            </div>
                            <div class="line"></div>
                        </div>
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" style="background: #3c6382" @click="addAzmoon()">افزودن</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal" style="background: #d63031">بستن</button>
                </div>
                </div>
            </div>
            </div>

        </div>
        <div class="line"></div>
        <div class="azmoon">
            <div class="titles">
                <h3 class="azTitle">
                    {{
                        this.lastAzmoon.name
                    }}
                </h3>
                <h3 class="remain" dir="rtl">
                    {{
                        this.getRemain()
                    }}
                </h3>
                <h5 class="desc">
                    {{
                        this.lastAzmoon.description + "  -  " + this.lastAzmoon.peymane
                    }}
                </h5>
            </div>
            <div class="azDatas">
                <table class="table table-hover table-bordered" dir="rtl">
                    <thead>
                        <tr>
                            <th scope="col">نام درس</th>
                            <th scope="col">بودجه بندی صفحات</th>
                            <th scope="col">بودجه بندی فصلی</th>
                            <th scope="col">هدف</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                        <th>حسابان</th>
                        <td>
                            {{
                                this.lastAzmoon.hesaban0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.hesaban1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.hesaban2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>فیزیک</th>
                        <td>
                            {{
                                this.lastAzmoon.fizik0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.fizik1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.fizik2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>شیمی</th>
                        <td>
                            {{
                                this.lastAzmoon.shimy0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.shimy1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.shimy2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>آمار</th>
                        <td>
                            {{
                                this.lastAzmoon.amar0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.amar1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.amar2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>هندسه</th>
                        <td>
                            {{
                                this.lastAzmoon.hendese0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.hendese1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.hendese2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>فارسی</th>
                        <td>
                            {{
                                this.lastAzmoon.farsi0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.farsi1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.farsi2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>دینی</th>
                        <td>
                            {{
                                this.lastAzmoon.dini0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.dini1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.dini2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>زبان</th>
                        <td>
                            {{
                                this.lastAzmoon.zaban0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.zaban1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.zaban2
                            }}
                        </td>
                        </tr>
                        <tr>
                        <th>عربی</th>
                        <td>
                            {{
                                this.lastAzmoon.arabi0
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.arabi1
                            }}
                        </td>
                        <td>
                            {{
                                this.lastAzmoon.arabi2
                            }}
                        </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        lastAzmoon: {}
    },
    data(){
        return {
            lessons: [
                {
                    fa:'حسابان',
                    en:'hesaban'
                },
                {
                    fa:'فیزیک',
                    en:'fizik'
                },
                {
                    fa:'شیمی',
                    en:'shimy'
                },
                {
                    fa:'آمار',
                    en:'amar'
                },
                {
                    fa:'هندسه',
                    en:'hendese'
                },
                {
                    fa:'فارسی',
                    en:'farsi'
                },
                {
                    fa:'دینی',
                    en:'dini'
                },
                {
                    fa:'زبان',
                    en:'zaban'
                },
                {
                    fa:'عربی',
                    en:'arabi'
                },
            ]
        }
    },
    methods: {
        getRemain(){
            const days = new Date(this.lastAzmoon.date).getDate() - new Date().getDate() - 1
            
            return this.toFarsiNumber(days) + " روز باقی مانده"
        },
        toFarsiNumber(n) {
            const farsiDigits = ['۰', '۱', '۲', '۳', '۴', '۵', '۶', '۷', '۸', '۹'];

            return n
                .toString()
                .replace(/\d/g, x => farsiDigits[x]);
        },
        addAzmoon(){
            var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

            var urlencoded = new URLSearchParams();
            const name = document.getElementById('name').value
            const desc = document.getElementById('desc').value
            const peymane = document.getElementById('peymane').value
            const date = document.getElementById('date').value
            const arabi0 = document.getElementById('arabi0').value
            const arabi1 = document.getElementById('arabi1').value
            const arabi2 = document.getElementById('arabi2').value
            const farsi0 = document.getElementById('farsi0').value
            const farsi1 = document.getElementById('farsi1').value
            const farsi2 = document.getElementById('farsi2').value
            const dini0 = document.getElementById('dini0').value
            const dini1 = document.getElementById('dini1').value
            const dini2 = document.getElementById('dini2').value
            const zaban0 = document.getElementById('zaban0').value
            const zaban1 = document.getElementById('zaban1').value
            const zaban2 = document.getElementById('zaban2').value
            const hesaban0 = document.getElementById('hesaban0').value
            const hesaban1 = document.getElementById('hesaban1').value
            const hesaban2 = document.getElementById('hesaban2').value
            const hendese0 = document.getElementById('hendese0').value
            const hendese1 = document.getElementById('hendese1').value
            const hendese2 = document.getElementById('hendese2').value
            const amar0 = document.getElementById('amar0').value
            const amar1 = document.getElementById('amar1').value
            const amar2 = document.getElementById('amar2').value
            const fizik0 = document.getElementById('fizik0').value
            const fizik1 = document.getElementById('fizik1').value
            const fizik2 = document.getElementById('fizik2').value
            const shimy0 = document.getElementById('shimy0').value
            const shimy1 = document.getElementById('shimy1').value
            const shimy2 = document.getElementById('shimy2').value

            urlencoded.append("name", "آزمون ۲۸ آذر");
            urlencoded.append("desc", "بسیار مهم");
            urlencoded.append("date", "2020/12/12");
            urlencoded.append("peymane", "۳ پیمانه");
            urlencoded.append("farsi0", farsi0);
            urlencoded.append("farsi1", farsi1);
            urlencoded.append("farsi2", farsi2);
            urlencoded.append("dini0", dini0);
            urlencoded.append("dini1", dini1);
            urlencoded.append("dini2", dini2);
            urlencoded.append("arabi0",arabi0);
            urlencoded.append("arabi1",arabi1);
            urlencoded.append("arabi2",arabi2);
            urlencoded.append("zaban0",zaban0);
            urlencoded.append("zaban1",zaban1);
            urlencoded.append("zaban2",zaban2);
            urlencoded.append("amar0",amar0);
            urlencoded.append("amar1",amar1);
            urlencoded.append("amar2",amar2);
            urlencoded.append("hendese0",hendese0);
            urlencoded.append("hendese1",hendese1);
            urlencoded.append("hendese2",hendese2);
            urlencoded.append("hesaban0",hesaban0);
            urlencoded.append("hesaban1",hesaban1);
            urlencoded.append("hesaban2",hesaban2);
            urlencoded.append("fizik0",fizik0);
            urlencoded.append("fizik1",fizik1);
            urlencoded.append("fizik2",fizik2);
            urlencoded.append("shimy0",shimy0);
            urlencoded.append("shimy1",shimy1);
            urlencoded.append("shimy2",shimy2);

            var requestOptions = {
                method: 'POST',
                headers: myHeaders,
                body: urlencoded,
                redirect: 'follow'
            };

            fetch("http://localhost:3000/azmoon/Add", requestOptions)
            .then(response => response.text())
            .then(result => {
                if (JSON.parse(result).msg == 'Azmoon Created'){
                    $('#exampleModal').modal('hide')
                    window.location.reload()
                }
            })
            .catch(error => console.log('error', error));
        }
    }
}
</script>
<style scoped>
.lessons {
    margin-top: 15px;
}
.lesson h3 {
    text-align: right;
}
.azDatas {
    margin-top: 20px;
}
.titles {
    margin-top: 10px;
}
.titles::after {
    content: '';
    display: table;
    clear: both;
}
.azTitle {
    text-align: right;
    float: right;
    width: 85%;
    display: inline-block;
}
.remain {
    float: right;
    text-align: left;
    display: inline-block;
    font-weight: bold;
}
.desc {
    text-align: right;
    display: inline-block;
    float: right;
}
.peymane {
    float: right;
}
.line {
  width: 100%;
  height: 0;
  border: 1px solid #0a3d62;
  margin: 3px;
  display:inline-block;
}
.main {
    margin: 30px 20px 0 20px;
    border-radius: 7px;
    padding: 30px;
}
.title {
    text-align: right;
    float: right;
    width: 90%;
    padding: 10px;
}
.addNew {
    float: right;
    width: 10%;
    font-size: 20px;
    background: #0a3d62;
    color: white;
    border-radius: 6px;
    padding: 10px;
    cursor: pointer;
}
.main::after {
    display: table;
    content: '';
    clear: both;
}
</style>