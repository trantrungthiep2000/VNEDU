<template>
    <div class="t-scorelookup t-student-class">
        <div class="header-scorelookup">
            <div class="box-scorelookup">
                <div class="combobox-scorelookup flex-combobox">
                    <div class="name-combobox">Chọn năm học</div>
                    <div class="box-combobox">
                        <div class="box-combobox-header" @click="clickBtnDownSchoolYear()">
                            <input class="input-data" type="text" readonly="true" :value="schoolyearName">
                            <div class="box-icon">
                                <div class="icon-down"></div>
                            </div>
                        </div>
                        <div class="box-combobox-content" v-show="isShowSelectSchoolYear">
                            <div v-for="schoolyear in schoolyears" :key="schoolyear.SchoolYearId" class="item-combobox" @click="clickItemSelectSchoolYear(schoolyear.SchoolYearId, schoolyear.SchoolYearName)">{{schoolyear.SchoolYearName}}</div>
                        </div>
                    </div>
                </div>
                <div class="combobox-scorelookup flex-combobox">
                    <div class="name-combobox">Chọn học kì</div>
                    <div class="box-combobox">
                        <div class="box-combobox-header" @click="clickBtnDownSemester()">
                            <input class="input-data" type="text" readonly="true" :value="semesterName">
                            <div class="box-icon">
                                <div class="icon-down"></div>
                            </div>
                        </div>
                        <div class="box-combobox-content" v-show="isShowSelectSemester">
                            <div v-for="semester in semesters" :key="semester.SemesterId" class="item-combobox" @click="clickItemSelectSemester(semester.SemesterId, semester.SemesterName)">{{semester.SemesterName}}</div>
                        </div>
                    </div>
                </div>
                <div class="combobox-scorelookup flex-combobox">
                    <div class="name-combobox">Chọn lớp học</div>
                    <div class="box-combobox">
                        <div class="box-combobox-header" @click="clickBtnDownClass()">
                            <input class="input-data" type="text" readonly="true" :value="className">
                            <div class="box-icon">
                                <div class="icon-down"></div>
                            </div>
                        </div>
                        <div class="box-combobox-content" v-show="isShowSelectClass">
                            <div v-for="Class in Classs" :key="Class.ClassId" class="item-combobox" @click="clickItemSelectClass(Class.ClassId, Class.ClassName)">{{Class.ClassName}}</div>
                        </div>
                    </div>
                </div>
                 <div class="combobox-scorelookup flex-combobox">
                    <div class="name-combobox">Chọn môn học</div>
                    <div class="box-combobox">
                        <div class="box-combobox-header" @click="clickBtnDownSubject()">
                            <input class="input-data" type="text" readonly="true" :value="subjectName">
                            <div class="box-icon">
                                <div class="icon-down"></div>
                            </div>
                        </div>
                        <div class="box-combobox-content" v-show="isShowSelectSubject">
                            <div v-for="subject in subjects" :key="subject.SubjectId" class="item-combobox" @click="clickItemSelectSubject(subject.SubjectId, subject.SubjectName)">{{subject.SubjectName}}</div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="box-see" style="margin-top: 11px;">
                <button class="btn-see" @click="clickBtnSee()">Xem</button>
            </div>
        </div>
        <div class="bottom-studentclass" v-show="isShowStudentClass">
            <div class="box-search box-filter">
                <div class="box-input-text input-student">
                    <input type="text" class="input-text" placeholder="Tìm kiếm theo mã học sinh, tên học sinh" v-model="SearchValue">
                    <div class="box-icon-search" @click="clickBtnSearch()">
                        <div class="icon-search"></div>
                    </div>
                </div>
            </div>
            <div class="between-schoolyear table-studet-class">
                <table class="m-table" border="1">
                    <thead>
                        <tr>
                            <th class="text-align-center" style="width: 50px">STT</th>
                            <th class="text-align-left" style="width: 100px">Mã học sinh</th>
                            <th class="text-align-left">Tên học sinh</th>
                            <th class="text-align-center" style="width: 80px">Giới tính</th>
                            <th class="text-align-center" style="width: 90px">Ngày sinh</th>
                            <th class="text-align-center" style="width: 110px">Điểm miệng</th>
                            <th class="text-align-center" style="width: 110px">Điểm 15 phút</th>
                            <th class="text-align-center" style="width: 110px">Điểm 1 tiết</th>
                            <th class="text-align-center" style="width: 110px">Điểm cuối kì</th>
                            <th class="text-align-center" style="width: 120px">Chức năng</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(student_class,i) in student_classs" :key="student_class.DetailedTableScoreId">
                            <th class="text-align-center">{{++i}}</th>
                            <th class="text-align-left">{{student_class.StudentCode}}</th>
                            <th class="text-align-left">{{student_class.FullName}}</th>
                            <th class="text-align-center">{{FomatGender(student_class.Gender)}}</th>
                            <th class="text-align-center">{{FomatDate(student_class.DateOfBirth)}}</th>
                            <th class="text-align-center">{{student_class.FirstOralScore}} {{student_class.SecondOralScore}} {{student_class.ThirdOralScore}}</th>
                            <th class="text-align-center" >{{student_class.First15minutesScore}} {{student_class.Second15minutesScore}} {{student_class.Third15minutesScore}}</th>
                            <th class="text-align-center" >{{student_class.OnePeriodScore}}</th>
                            <th class="text-align-center" >{{student_class.FinalScore}}</th>
                            <th class="text-align-center">
                                <div class="box-function">
                                    <div class="btn-edit" @click="clickBtnUpdate(student_class.DetailedTableScoreId)"></div>
                                </div>
                            </th>
                        </tr>  
                        
                    </tbody>
                </table>
            </div>
            <div class="bottom-schoolyear box-type-paging paging-student-class">
                <div class="box-sum">Tổng số: {{student_classs.length}} bản ghi</div>
                <div class="box-paging">
                    <div class="pri" @click="clickPagePri()">
                        <div class="page-pri"></div>
                    </div>
                    <div class="page-number">
                        <div v-for="i in pagings" :key="i" :class="{ active: pageNumber == i }" class="number" @click="clickPageNumber(i)" >{{i}}</div>
                    </div>
                    <div class="next" @click="clickPageNext()">
                        <div class="page-next" ></div>
                    </div>
                </div>
                <div class="box-size">
                    <input type="text" class="box-size-input" readonly :value="pagename">
                    <div class="box-select-size" @click="clickBtnSelectSize()">
                        <div class="icon-size"></div>
                    </div>
                    <div class="box-size-item" v-show="isShowBoxItemSize">
                        <div v-for="page in pages" :key="page.index" class="item-size" @click="clickItemSize(page.index, page.name)">{{page.name}}</div>
                    </div>
                </div>
            </div>
        </div>
        <detailed-table-score-infor></detailed-table-score-infor>
    </div>
</template>

<script>
import axios from 'axios';
import { mapGetters } from 'vuex';
import { eventBus } from '../../main';
import moment from 'moment';
import DetailedTableScoreInfor from './DetailedTableScoreInfor.vue';
export default {
  components: { DetailedTableScoreInfor },
    data() {
        return {
            isShowStudentClass: false,
            isShowSelectSemester: false,
            isShowSelectSchoolYear: false,
            isShowSelectClass: false,
            isShowBoxItemSize: false,
            isShowSelectSubject: false,
            schoolyears: [
               
            ],
            semesters: [
               
            ],
            Classs:[

            ],
            subjects: [],
            subjectName: null,
            subjectId: null,
            semesterName: null,
            semesterId: null,
            className: null,
            classId: null,
            schoolyearName: null,
            schoolyearId: null,
            student_classs: [

            ],
            pages: [
                {
                    index: 10,
                    name: "10 bản ghi trên 1 trang"
                },
                {
                    index: 20,
                    name: "20 bản ghi trên 1 trang"
                },
                {
                    index: 30,
                    name: "30 bản ghi trên 1 trang"
                },
                {
                    index: 50,
                    name: "50 bản ghi trên 1 trang"
                },
                {
                    index: 100,
                    name: "100 bản ghi trên 1 trang"
                }
            ],
            SearchValue: '',
            pageSize: 10, 
            pageNumber: 1,
            totalRecord: null,
            totalPage: null,
            pagename: "10 bản ghi trên 1 trang",
        }
    },

    computed:{
        ...mapGetters(['URLAPI']),
        pagings() {
            let numShown = 5;
            numShown = Math.min(numShown, this.totalPage);
            let first = this.pageNumber - Math.floor(numShown / 2);
            first = Math.max(first, 1);
            first = Math.min(first, this.totalPage - numShown + 1);
            return [...Array(numShown)].map((k,i) => i + first);
        }
    },
    methods: {
        clickPageNumber(i){
            var m = this;
            m.pageNumber = i;
            m.loadDataScore();
        },
        clickPageNext(){
            var m = this;
            if(m.pageNumber < m.totalPage)
            {
                m.pageNumber++;
                m.loadDataScore();
                console.log(m.pageNumber);
            }
            else
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Đã đến trang cuối cùng");
            }
        },
        clickPagePri(){
            var m = this;
            if(m.pageNumber > 1)
            {
                m.pageNumber--;
                m.loadDataScore();
                console.log(m.pageNumber);
            }
            else
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Đã đến trang đầu tiên");
            }
        },
        /**
         * click vào btn tìm kiếm 
         * CreatedBy: TTThiep (04/01/2022)
         */
        clickBtnSearch(){
            this.pageNumber = 1;
            this.loadDataScore();
            eventBus.$emit("isShowToastMessageWas", true);
            eventBus.$emit("TitleToastMessageWas", "Tìm kiếm học sinh thành công");
        },
        /**
         * Định dạng lại ngày sinh để hiển thị 
         * CreatedBy: TTThiep (09/02/2022)
         */
        FomatDate(value){
            if (value){
                return moment(String(value)).format('DD-MM-YYYY');
            }
        },
        /**
         * Định dạng lại giới tính 
         * CreatedBy: TTThiep (09/02/2022)
         */
        FomatGender(value){
            if (value != null){
                if(value == 0)
                {
                    return "Nữ";
                }
                else if(value == 1)
                {
                    return "Nam";
                }
                else if(value == 2){
                    return "Khác";
                }
            }
            else{
                return "";
            }
        },

        /**
         * click vào btn hiện box size
         * CreatedBy: TTThiep(08/02/2022)
         */
        clickBtnSelectSize(){
            this.isShowBoxItemSize = !this.isShowBoxItemSize;
        },
        /**
         * click vào chọn số bản ghi trên 1 trang
         * CreatedBy: TTThiep(08/02/2022)
         */
        clickItemSize(index, name){
            this.pageSize = index;
            this.pagename = name;
            this.loadDataScore();
            this.isShowBoxItemSize = false;
        },
        /**
         * click vào btn down gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickBtnDownSemester(){
            if(this.schoolyearId == null)
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn năm học trước");
            }
            else{
                this.isShowSelectSemester = !this.isShowSelectSemester;
            }
            
        },

        /**
         * click vào item gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickItemSelectSubject(subjectId, subjectName)
        {
            this.isShowSelectSubject = !this.isShowSelectSubject;
            this.subjectName = subjectName;
            this.subjectId = subjectId;
            this.isShowStudentClass = false;
        },

        clickBtnDownSubject(){
            if(this.classId == null)
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn lớp học trước");
            }
            else{
                this.isShowSelectSubject = !this.isShowSelectSubject;
            }
            
        },

        /**
         * click vào item gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickItemSelectSemester(semesterId, semesterName)
        {
            this.isShowSelectSemester = !this.isShowSelectSemester;
            this.semesterName = semesterName;
            this.semesterId = semesterId;
            this.isShowStudentClass = false;
        },

        /**
         * click vào btn down gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickBtnDownClass(){
            if(this.semesterId == null)
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn học kì trước");
            }
            else{
                this.isShowSelectClass = !this.isShowSelectClass;
            }
        },

        /**
         * click vào item gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickItemSelectClass(classId, className)
        {
            this.isShowSelectClass = !this.isShowSelectClass;
            this.className = className;
            this.classId = classId;
            this.isShowStudentClass = false;
        },
        /**
         * click vào btn down gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickBtnDownSchoolYear(){
            this.isShowSelectSchoolYear = !this.isShowSelectSchoolYear;
        },

        /**
         * click vào item gender
         * CreatedBy: TTThiep(11/01/2022)
         */
        clickItemSelectSchoolYear(schoolyearId, schoolyearName)
        {
            var m = this;
            this.isShowSelectSchoolYear = !this.isShowSelectSchoolYear;
            this.schoolyearName = schoolyearName;
            this.schoolyearId = schoolyearId;
            this.isShowStudentClass = false;
            axios
            .get(`${m.URLAPI}/api/v1/Classs/GetBySchoolYearId?SchoolYearId=${schoolyearId}`)
            .then(function (response){
                if(response && response.data)
                { 
                    m.Classs = response.data;
                    if(m.Classs.length == 0)
                    {
                        eventBus.$emit("isShowFormWaningWas", true);
                        eventBus.$emit("errorWas", "Năm học này chưa có lớp học vui lòng chọn năm học khác");
                    }
                }
            })
            .catch(function (res){
                console.log(res);
            });
        },

        /**
         * lấy tất cả năm học
         * CreatedBy: TTThiep(25/01/2022)
         */
        getDataSchoolYear(){
            var m = this;
            axios
            .get(`${m.URLAPI}/api/v1/SchoolYears`)
            .then(function (response){
                if(response && response.data)
                { 
                   m.schoolyears = response.data;
                }
            })
            .catch(function (res){
                console.log(res);
            });
        },

        /**
         * lấy tất cả học kì
         * CreatedBy: TTThiep(25/01/2022)
         */
        getDataSemester(){
            var m = this;
            axios
            .get(`${m.URLAPI}/api/v1/Semesters`)
            .then(function (response){
                if(response && response.data)
                { 
                   m.semesters = response.data;
                }
            })
            .catch(function (res){
                console.log(res);
            });

        },

        /**
         * lấy tất cả môn học
         * CreatedBy: TTThiep(25/01/2022)
         */
        getDataSubject(){
            var m = this;
            axios
            .get(`${m.URLAPI}/api/v1/Subjects`)
            .then(function (response){
                if(response && response.data)
                { 
                   m.subjects = response.data;
                }
            })
            .catch(function (res){
                console.log(res);
            });

        },
        /**
         * click vào btn xem
         * CreatedBy: TTThiep(25/01/2022)
         */
        clickBtnSee(){
            var m = this;
            if(m.schoolyearId == null || m.schoolyearId == "")
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn năm học cần xem");
            }
            else if(m.Classs.length == 0)
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Năm học này chưa có lớp học vui lòng chọn năm học khác");
            }
            else if(m.semesterId == null || m.semesterId == "")
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn học kì cần xem");
            }
            else if(m.classId == null || m.classId == "")
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn lớp học cần xem");
            }
            else if(m.subjectId == null || m.subjectId == "")
            {
                eventBus.$emit("isShowFormWaningWas", true);
                eventBus.$emit("errorWas", "Vui lòng chọn môn học cần xem");
            }
            else{
                m.isShowStudentClass = true;
                m.pageNumber = 1;
                axios
                .get(`${m.URLAPI}/api/v1/Student_Subjects/GetPagingStudentClassBySchoolYearSemesterSubjectClass?SchoolYearId=${m.schoolyearId}&SemesterId=${m.semesterId}&SubjectId=${m.subjectId}&ClassId=${m.classId}&ValueFilter=${m.SearchValue}&PageIndex=${m.pageNumber}&PageSize=${m.pageSize}`)
                .then(function (response){
                    if(response && response.data.Data)
                    {
                        m.student_classs = response.data.Data;
                        m.totalRecord = response.data.TotalRecord;
                        m.totalPage = response.data.TotalPage;
                        eventBus.$emit("isShowToastMessageWas", true);
                        eventBus.$emit("TitleToastMessageWas", "Xem thành công");
                    }
                })
                .catch(function (res){
                    console.log(res);
                });
            }
        },
        loadDataScore(){
            var m = this;
            axios
            .get(`${m.URLAPI}/api/v1/Student_Subjects/GetPagingStudentClassBySchoolYearSemesterSubjectClass?SchoolYearId=${m.schoolyearId}&SemesterId=${m.semesterId}&SubjectId=${m.subjectId}&ClassId=${m.classId}&ValueFilter=${m.SearchValue}&PageIndex=${m.pageNumber}&PageSize=${m.pageSize}`)
            .then(function (response){
                if(response && response.data.Data)
                {
                    m.student_classs = response.data.Data;
                    m.totalRecord = response.data.TotalRecord;
                    m.totalPage = response.data.TotalPage;
                }
            })
            .catch(function (res){
                console.log(res);
            });
        },
        /**
         * click btn cập nhật
         * CreatedBy: TTThiep(08/02/2022)
         */
        clickBtnUpdate(detailedTableScoreId){
            eventBus.$emit("isShowDetailedTableScoreInforWas", true);
            eventBus.$emit("detailedTableScoreIdWas", detailedTableScoreId);
            eventBus.$emit('thisWas', this);
            var m = this;
            axios
            .get(`${m.URLAPI}/api/v1/DetailedTableScores/${detailedTableScoreId}`)
            .then(function (response){
                if(response && response.data)
                {
                    eventBus.$emit('detailedtablescoreWas', response.data);
                }
            })
            .catch(function (res){
                console.log(res);
            });
        },
    },

    created() {
        var m = this;
        m.getDataSchoolYear();
        m.getDataSemester();
        m.getDataSubject();
    },
}
</script>

<style>

</style>