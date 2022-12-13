<template>
    <div id="modal-add" class="modal" v-if="isHide">
        <div class="form-modal">
            <div class="modal-header">{{ tittle }} danh hiệu thi đua
                <div class="modal-icon">
                    <div class="modal-help" title="Hướng dẫn"></div>
                    <div class="modal-close" title="Đóng" @click="closeForm()"></div>
                </div>
            </div>
            <div class="modal-content custom1">
                <div class="row1-name">
                    <label for="" class="label-tittle">Tên danh hiệu thi đua <span class="red">*</span></label>
                    <input type="text" class="base-input ce-name-input" v-focus v-click-outside="validateName"
                        placeholder="Nhập tên danh hiệu thi đua" v-model="nameInput" tabindex="0">
                    <label for="" class="label-tittle red" v-show="!ceName">
                        Tên danh hiệu thi đua không được để trống.</label>
                </div>
                <div class="row2-selection custom2">
                    <div class="row2 custom3">
                        <label for="" class="label-tittle">Mã danh hiệu <span class="red">*</span></label>
                        <input type="text" v-click-outside="validateCode" class="base-input ce-code-input"
                            placeholder="Nhập mã danh hiệu" v-model="codeInput" />
                        <label class="label-tittle red" v-show="!ceCode">
                            Mã danh hiệu không được để trống.</label>
                    </div>
                    <div class="row2">
                        <label for="" class="label-tittle">Đối tượng khen thưởng
                            <span class="red">*</span>
                        </label>
                        <div class="row-checkbox">
                            <div class="checkbox1">
                                <label class="c-checkbox custom-position">
                                    <input type="checkbox" v-model="isSingle" @change="valueOutput">
                                    <span class="checkmark"></span>
                                </label>
                                <label class="mg-left">Cá nhân</label>
                            </div>
                            <div class="checkbox1">
                                <label class="c-checkbox custom-position">
                                    <input type="checkbox" v-model="isGroup" @change="valueOutput">
                                    <span class="checkmark"></span>
                                </label>
                                <label class="mg-left">Tập thể</label>
                            </div>
                        </div>
                        <label for="" class="label-tittle red" v-show="!ceObject">Đối
                            tượng khen thưởng
                            không được để trống.
                        </label>
                    </div>
                </div>
                <div class="row2-selection">
                    <div class="row2 custom4">
                        <label for="" class="label-tittle">Cấp khen thưởng <span class="red">*</span></label>
                        <div class="c-combobox combobox-level">
                            <input class="page-limit input-level" type="text" v-model="level"
                                v-click-outside="validateLevel">
                            <div class="icon-limit" @click="clickLevel()"></div>
                            <div class="dropdown-panel position-level" v-show="isShowLevel">
                                <div class="dropdown-body scroll">
                                    <ul class="dropdown-items">
                                        <li class="combobox-item" v-for="(item, index) in levelOption" :key="index"
                                            @click="chooseLevel(index + 1)"
                                            :class="{ 'chooseItem': isSelectedLevel == index + 1 }">
                                            <div class="combobox-item-con">
                                                <div class="combobox-item--text">{{ item }} </div>
                                                <div class="selected-container">
                                                    <div class="icon24 mi-checkbox-active"
                                                        v-if="(isSelectedLevel == index + 1)">
                                                    </div>
                                                </div>
                                            </div>
                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <label for="" class="label-tittle red" v-show="!ceLevel">
                            Cấp khen thưởng không được để trống.</label>
                    </div>
                    <div class="row2">
                        <label for="" class="label-tittle">Loại phong trào áp dụng
                            <span class="red">*</span>
                        </label>
                        <div class="row-checkbox">
                            <div class="checkbox1">
                                <label class="c-checkbox custom-position">
                                    <input type="checkbox" v-model="isFrequent" @change="valueOutput">
                                    <span class="checkmark"></span>
                                </label>
                                <label class="mg-left">Thường xuyên</label>
                            </div>
                            <div class="checkbox1">
                                <label class="c-checkbox custom-position">
                                    <input type="checkbox" v-model="isBatched" @change="valueOutput">
                                    <span class="checkmark"></span>
                                </label>
                                <label class="mg-left">Theo đợt</label>
                            </div>
                        </div>
                        <label for="" class="label-tittle red" v-show="!ceType">
                            Loại phong trào không được để trống.
                        </label>
                    </div>
                </div>
                <div class="row1-name custom5">
                    <label for="" class="label-tittle">Ghi chú</label>
                    <textarea class="base-input ce-notes-input" placeholder="Nhập ghi chú" v-model="notes"></textarea>
                </div>
                <div class="row4 custom5" v-show="(typeForm == 2)">
                    <label for="" class="label-tittle">Trạng thái</label>
                    <div class="flex">
                        <label class="c-radio">
                            <input type="radio" value="1" name="status" v-model="statusEdit">
                            <span class="checkmark2"></span>
                            <label>Sử dụng</label>
                        </label>
                        <label class="c-radio">
                            <input type="radio" value="0" name="status" v-model="statusEdit">
                            <span class="checkmark2"></span>
                            <label>Ngừng sử dụng</label>
                        </label>
                    </div>

                </div>
            </div>
            <div class="modal-footer">
                <div class="flex-row">
                    <div class="flex"></div>
                    <div class="flex-buttons">
                        <button class="btn btn-cancel" @click="closeForm()">Huỷ</button>
                        <button class="btn btn-save btn-edit" v-show="(typeForm == 2)" @click="saveEdit()">Lưu thay
                            đổi</button>
                        <button class="btn btn-save-add" v-show="(typeForm == 1)" @click="closeForm()"
                            title="Ctrl + Shift + S">Lưu & thêm mới</button>
                        <button class="btn btn-save" v-show="(typeForm == 1)" @click="saveData()"
                            title="Ctrl + S">Lưu</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script scoped>
import emitter from '../js/event-bus.js'
import { ClickOutside } from "vue-click-outside-of";
const focus = {
    mounted: (el) => el.focus()
}
export default {
    data() {
        return {
            typeForm: null,
            isHide: false,
            tittle: null,
            ceName: true,
            ceCode: true,
            ceObject: true,
            ceLevel: true,
            ceType: true,
            nameInput: null,
            codeInput: null,
            isSingle: true,
            level: "Cấp Nhà nước",
            levelOption: ["Cấp Nhà nước", "Cấp Tỉnh/tương đương", "Cấp Huyện/tương đương", "Cấp Xã/tương đương"],
            isGroup: false,
            isFrequent: true,
            isBatched: false,
            notes: null,
            isShowLevel: false,
            isSelectedLevel: 1,
            setLevel: "Cấp Nhà nước",
            dataSave: [],
            outObject: 1,
            outType: 1,
            statusEdit: 3,
        }
    },
    created() {
        /**
        * Nhận sự kiện click vào Thêm mới
        * @author : Đào Trọng Khang 
        * @created : ( 2/12/2022 )
        */
        emitter.on('addOnClick', (val) => {
            this.isHide = val[0];
            this.tittle = val[1];
            if (this.tittle == "Thêm") {
                this.typeForm = 1
            }
            if (this.tittle == "Sửa") {
                this.typeForm = 2
            }
        })
        /**
        * Nhận sự kiện click vào Sửa
        * @author : Đào Trọng Khang 
        * @created : ( 2/12/2022 )
        */
        emitter.on('editOnClick', (val) => {
            this.isHide = val[0];
            this.tittle = val[1];
            if (this.tittle == "Thêm") {
                this.typeForm = 1
            }
            if (this.tittle == "Sửa") {
                this.typeForm = 2
            }
            this.nameInput = val[2].name;
            this.codeInput = val[2].code;
            this.outObject = val[2].object;
            this.outType = val[2].type;
            this.statusEdit = val[2].status;
            this.notes = val[2].notes;
            this.level = val[2].level;
            this.inputLevel(this.level)
            this.valueInput()
        })
    },
    methods: {
        /**
        * event : Click btn chọn cấp
        * result : hiện dropdown-menu chọn limit-record/page
        * @author : Đào Trọng Khang ( 27/11/2022 )
        */
        clickLevel() {
            this.isShowLevel = !this.isShowLevel;
        },

        /**
        * event : Click item trong dropdown-menu cấp khen thg
        * result : highlight + hiện icon active + ẩn dropdown
        * @author : Đào Trọng Khang ( 27/11/2022 )
        */
        chooseLevel(number) {
            this.isSelectedLevel = number;
            this.isShowLevel = false
            this.level = this.levelOption[number - 1]
        },
        /**
        * event : Click btn Huỷ
        * result : đóng và reset các vùng dữ liệu về mặc định
        * @author : Đào Trọng Khang 
        * @Created : 12/12/2022
        */
        closeForm() {
            this.nameInput = "";
            this.codeInput = "";
            this.isSingle = true;
            this.isSelectedLevel = 1;
            this.isGroup = false;
            this.isFrequent = true;
            this.isBatched = false;
            this.notes = "";
            this.isHide = false;
        },
        /**
        * event : Click btn Lưu 
        * result : đóng và gửi dữ liệu về component Content.vue
        * @author : Đào Trọng Khang 
        * @Created : 12/12/2022
        */
        saveData() {
            let objData = {
                name: this.nameInput,
                code: this.codeInput,
                object: this.outObject,
                level: this.level,
                type: this.outType,
                notes : this.notes,
                status: 1
            }
            this.nameInput = "";
            this.codeInput = "";
            this.isSingle = true;
            this.isSelectedLevel = 1;
            this.isGroup = false;
            this.isFrequent = true;
            this.isBatched = false;
            this.notes = "";
            this.dataSave.push(objData)
            emitter.emit('sendData', objData)
            this.isHide = false;
        },
        /**
        * event : Click btn Lưu thay đổi
        * result : đóng và gửi dữ liệu đã sửa về component Content.vue
        * @author : Đào Trọng Khang 
        * @Created : 12/12/2022
        */
        saveEdit(){
            let objData = {
                name: this.nameInput,
                code: this.codeInput,
                object: this.outObject,
                level: this.level,
                type: this.outType,
                notes : this.notes,
                status: parseInt(this.statusEdit)
            }
            this.nameInput = "";
            this.codeInput = "";
            this.isSingle = true;
            this.isSelectedLevel = 1;
            this.isGroup = false;
            this.isFrequent = true;
            this.isBatched = false;
            this.notes = "";
            this.dataSave.push(objData)
            emitter.emit('sendEdit', objData)
            this.isHide = false;
        },

        /**
        * event : Validate dữ liệu
        * @author : Đào Trọng Khang ( 27/11/2022 )
        */
        validateName() {
            if (!this.nameInput) { this.ceName = false }
            else { this.ceName = true }
        },
        validateCode() {
            if (!this.codeInput) { this.ceCode = false }
            else { this.ceCode = true }
        },
        validateLevel() {
            if (!this.level) { this.ceLevel = false }
            else { this.ceLevel = true }
        },
        validateObject() {
            if (this.outObject == 0) { this.ceObject = false }
            else { this.ceObject = true }
        },
        validateType() {
            if (!this.outType) { this.ceType = false }
            else { this.ceType = true }
        },
        /**
        * event : Validate dữ liệu phần checkbox
        * @author : Đào Trọng Khang ( 2/12/2022 )
        */
        valueOutput() {
            let a, b, c, d = null;
            if (this.isSingle) { a = 1 } else { a = 0 }
            if (this.isGroup) { b = 2 } else { b = 0 }
            if (this.isFrequent) { c = 1 } else { c = 0 }
            if (this.isBatched) { d = 2 } else { d = 0 }
            this.outObject = a + b;
            this.outType = c + d;
        },
        /**
        * event : Binding dữ liệu phần checkbox khi click edit
        * @author : Đào Trọng Khang 
        * @Created : 12/12/2022
        */
        valueInput() {
            switch (this.outObject) {
                case 1:
                    this.isSingle = true;
                    this.isGroup = false;
                    break;
                case 2:
                    this.isSingle = false;
                    this.isGroup = true;
                    break;
                case 3:
                    this.isSingle = true;
                    this.isGroup = true;
                    break;
            }
            switch (this.outType) {
                case 1:
                    this.isFrequent = true;
                    this.isBatched = false;
                    break;
                case 2:
                    this.isFrequent = false;
                    this.isBatched = true;
                    break;
                case 3:
                    this.isFrequent = true;
                    this.isBatched = true;
                    break;
            }
        },
        inputLevel(input) {
            let i = 0;
            while (i < this.levelOption.length){
                if(input == this.levelOption[i]){
                    this.isSelectedLevel = i + 1 ;
                }
                i++;
            }
        }

    },
    watch: {
        /**
        * watch value để validate dữ liệu => ẩn hiện msg required
        * @author : Đào Trọng Khang 
        * @Created : 4/12/2022
        */
        nameInput(val) {
            if (val.length > 0) {
                this.ceName = true
            }
        },
        codeInput(val) {
            if (val.length > 0) {
                this.ceCode = true
            }
        },
        level(val) {
            if (val.length > 0) {
                this.ceLevel = true
            }
        },
        outObject(val) {
            if (val == 0) {
                this.ceObject = false
            }
            else { this.ceObject = true }
        },
        outType(val) {
            if (val == 0) {
                this.ceType = false
            }
            else { this.ceType = true }
        }
    },
    directives: {
        // enables v-focus in template
        focus, ClickOutside,
    }
}
</script>
<style scoped>
@import url(../styles/modal.css);
@import url(../styles/content.css);
@import url(../styles/checkbox.css);
@import url(../styles/radio.css);

.custom5 {
    margin-bottom: 16px;
    display: grid;
}
</style> 