<template>
    <div class="t-dialog" v-show="isShowDeleteAdministration">
        <div class="m-form">
            <div class="form-title">
                <div class="title-icon"></div>
                <div class="title-name">{{titleName}}</div>
            </div>
            <div class="form-btn">
                <div class="form-btn-cancle" @click="clickBtnNo()">Không</div>
                <div class="form-btn-delete" @click="clickBtnYes()">Có</div>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';
import { eventBus } from '../../main'
import { mapGetters } from 'vuex'
export default {
    data() {
        return {
            isShowDeleteAdministration: false,
            UserId: null,
            titleName: null,
            m2: null,
        }
    },
    computed: {
        ...mapGetters(['URLAPI']),
    },
    methods: {
        /**
         * click Btn không
         * CreatedBy: TTThiep(28/01/2022)
         */
        clickBtnNo(){
            this.isShowDeleteAdministration = !this.isShowDeleteAdministration;
        },
        /**
         * click Btn có
         * CreatedBy: TTThiep(28/01/2022)
         */
        clickBtnYes(){
            var m = this;
            axios
            .delete(`${m.URLAPI}/api/v1/Useds/${m.UserId}`)
            .then(function(response){
                console.log(response);
                // gửi dữ liệu sang component FormToastMessage là 'true'
                eventBus.$emit("isShowToastMessageWas", true);
                // gửi dữ liệu sang component FormToastMessage là 'xóa người dùng thành công'
                eventBus.$emit("TitleToastMessageWas", "Xóa người dùng thành công");
                m.m2.loadDataAdministration();
                m.isShowDeleteAdministration = !m.isShowDeleteAdministration;
            })
            .catch(function(res){
                console.log(res);
            })
        },
    },
    created() {
        var  m = this;
        eventBus.$on("isShowDeleteAdministrationWas", (isShowDeleteAdministrationData) =>{
            m.isShowDeleteAdministration = isShowDeleteAdministrationData;
        });
        eventBus.$on("administrationIdWas", (UserIdData) =>{
            m.UserId = UserIdData;
        });
        eventBus.$on("titlenameWas", (titlenameData) =>{
            m.titleName = titlenameData;
        });
        eventBus.$on("thisWas", (thisData) =>{
            m.m2 = thisData;
        });
    },
}
</script>