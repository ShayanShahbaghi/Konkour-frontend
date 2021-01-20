<template>
    <div class="main shadow-lg">
        <h3 class="title">
            برنامه ریزی درس به درس
        </h3>
        <div class="addNew" dir="rtl" data-toggle="modal" data-target="#add">
            افزودن برنامه
        </div>
        <div class="modal fade" id="add" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document" dir="rtl">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">برنامه جدید</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">نام درس</span>
                        </div>
                        <input id="name" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">بخش</span>
                        </div>
                        <input id="part" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">مجموع ساعت مطالعه</span>
                        </div>
                        <input id="sum" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">از ابتدای روز</span>
                        </div>
                        <input id="from" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">تا انتهای روز</span>
                        </div>
                        <input id="to" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" style="background: #3c6382" @click="addLesson()">افزودن</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal" style="background: #d63031">بستن</button>
                </div>
                </div>
            </div>
        </div>
        <div class="line"></div>
        <div class="lessonData">
            <table class="table table-hover table-bordered" dir="rtl">
                <thead>
                    <tr>
                    <th scope="col">نام درس</th>
                    <th scope="col">بخش</th>
                    <th scope="col">مجموع ساعت مطالعه</th>
                    <th scope="col">از ابتدای روز</th>
                    <th scope="col">تا آخر روز</th>
                    
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="index in this.todo" :key="index">
                        <th scope="row">
                            {{
                                index.name
                            }}
                        </th>
                        <td>
                            {{
                                index.part
                            }}
                        </td>
                        <td>
                            {{
                                index.sum
                            }}
                        </td>
                        <td>
                            {{
                                index.fromWhen
                            }}
                        </td>
                        <td>
                            {{
                                index.toWhen
                            }}
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        todo: []
    },
    methods:{
        addLesson(){
            var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

            var urlencoded = new URLSearchParams();
            const name = document.getElementById('name').value
            const part = document.getElementById('part').value
            const sum = document.getElementById('sum').value
            const to = document.getElementById('to').value
            const from = document.getElementById('from').value
            urlencoded.append("name", name);
            urlencoded.append("part", part);
            urlencoded.append("sum", sum);
            urlencoded.append("to", to);
            urlencoded.append("from", from);

            var requestOptions = {
                method: 'POST',
                headers: myHeaders,
                body: urlencoded,
                redirect: 'follow'
            }

            fetch("http://localhost:3000/todo/lesson/Add", requestOptions)
            .then(response => response.text())
            .then(result => {
                console.log(result)
                if (JSON.parse(result).msg == 'Todo Inserted'){
                    $('#add').modal('hide')
                    window.location.reload()
                }
            })
            .catch(error => console.log('error', error));
        }
    }
}
</script>
<style scoped>
.lessonData {
    margin-top: 10px;
}
.main {
    margin: 50px 20px 0 20px;
    border-radius: 7px;
    padding: 30px;
}
.main::after {
    content: '';
    display: table;
    clear: both;
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
.line {
  width: 100%;
  height: 0;
  border: 1px solid #0a3d62;
  margin: 3px;
  display:inline-block;
}
</style>