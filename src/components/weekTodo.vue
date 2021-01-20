<template>
    <div class="main shadow-lg">
        <h3 class="title">
            فعالیت های هفتگی
        </h3>
        <div class="addNew" dir="rtl" data-toggle="modal" data-target="#addweek">
            افزودن برنامه
        </div>
        <div class="modal fade" id="addweek" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
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
                        <input id="name0" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">بخش</span>
                        </div>
                        <input id="part0" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">میزان مطالعه</span>
                        </div>
                        <input id="sum0" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                    <div class="input-group mb-3">
                        <div class="input-group-prepend">
                            <span class="input-group-text" id="">روز مطالعه</span>
                        </div>
                        <input id="date0" type="text" class="form-control" aria-label="Sizing example input" aria-describedby="inputGroup-sizing-default">
                    </div>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-primary" style="background: #3c6382" @click="addTodo()">افزودن</button>
                    <button type="button" class="btn btn-secondary" data-dismiss="modal" style="background: #d63031">بستن</button>
                </div>
                </div>
            </div>
        </div>
        <div class="line"></div>
        <div class="weekData">
            <table class="table table-hover table-bordered" dir="rtl">
                <thead>
                    <tr>
                    <th scope="col">نام درس</th>
                    <th scope="col">بخش</th>
                    <th scope="col">میزان مطالعه</th>
                    <th scope="col">روز مطالعه</th>
                    <th scope="col">انجام شده؟</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="index in this.todo" :key="index">
                        <th scope="row">
                            {{
                                index.lesson
                            }}
                        </th>
                        <td>
                            {{
                                index.part
                            }}
                        </td>
                        <td>
                            {{
                                index.hours
                            }}
                        </td>
                        <td>
                            {{
                                index.day
                            }}
                        </td>
                        <td @click="completeIT(index)">
                            {{
                                index.done
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
    methods: {
        completeIT(object){
            const id = object.id
            var requestOptions = {
                method: 'PUT',
                redirect: 'follow'
            };

            fetch(`http://localhost:3000/todo/week/${id}`, requestOptions)
            .then(response => response.text())
            .then(result => {
                console.log(result)
                window.location.reload()
            })
            .catch(error => console.log('error', error));
        },
        addTodo(){
            var myHeaders = new Headers();
            myHeaders.append("Content-Type", "application/x-www-form-urlencoded");

            var urlencoded = new URLSearchParams();
            const name = document.getElementById('name0').value
            const part = document.getElementById('part0').value
            const hours = document.getElementById('sum0').value
            const date = document.getElementById('date0').value
            console.log(name)
            console.log(part)
            console.log(hours)
            console.log(date)

            urlencoded.append("lesson", name);
            urlencoded.append("hours", hours);
            urlencoded.append("day", date);
            urlencoded.append("part", part);
            urlencoded.append("done", "نه");

            var requestOptions = {
                method: 'POST',
                headers: myHeaders,
                body: urlencoded,
                redirect: 'follow'
            };

            fetch("http://localhost:3000/todo/week/Add", requestOptions)
            .then(response => response.text())
            .then(result => {
                if (JSON.parse(result).msg == 'Todo Inserted'){
                    $('#addweek').modal('hide')
                    window.location.reload()
                }
            })
            .catch(error => console.log('error', error));
        }
    }
}
</script>
<style scoped>
.line {
  width: 100%;
  height: 0;
  border: 1px solid #0a3d62;
  margin: 3px;
  display:inline-block;
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
</style>