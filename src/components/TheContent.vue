<template>
  <div class="content" style="flex:1">
    <div class="tittle-content">Danh hiệu thi đua</div>
    <div class="toolbar">
      <div class="toolbar-left">
        <input type="text" class="base-input" 
        placeholder="Nhập mã hoặc tên danh hiệu..." 
        v-model="searchText" />
        <div class="icon-clear" v-if="isShow"></div>
        <div class="icon-search"></div>
        <div class="filter">
          <button class="filter-btn" @click="(isShowFilter = !isShowFilter)">
            <div class="icon-filter"></div>
            Bộ lọc
          </button>
          <div class="position-filter" v-show="isShowFilter">
            <div class="dropdown-body">
              <span class="arrow"></span>
              <div class="box-header">
                <div class="box-tittle">Lọc danh hiệu</div>
                <div class="modal-close" @click="(isShowFilter = !isShowFilter)"></div>
              </div>
              <div class="box-content">
                <div class="form-group">
                  <label class="filter-label">Đối tượng khen thưởng</label>
                  <div class="c-combobox combobox-level" v-click-outside="hideObject">
                    <input class="page-limit input-level" type="text" :value="objectDefault">
                    <div class="icon-limit" @click="(dropObject = !dropObject)"></div>
                    <div class="dropdown-panel position-level--filter" v-show="dropObject">
                      <div class="dropdown-body scroll">
                        <ul class="dropdown-items">
                          <li class="combobox-item" v-for="(item, index) in arrObject" :key="index"
                            @click="chooseObject(index)" :class="{ 'chooseItem': objectSelected == index }"
                            style="text-align: left;">
                            <div class="combobox-item-con">
                              <div class="combobox-item--text">{{ item }} </div>
                              <div class="selected-container">
                                <div class="icon24 mi-checkbox-active" v-if="(objectSelected == index)">
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="form-group">
                  <label class="filter-label">Cấp khen thưởng</label>
                  <div class="c-combobox combobox-level" v-click-outside="hideLevel">
                    <input class="page-limit input-level" type="text" :value="levelDefault">
                    <div class="icon-limit" @click="(dropLevel = !dropLevel)"></div>
                    <div class="dropdown-panel position-level--filter" v-show="dropLevel">
                      <div class="dropdown-body scroll">
                        <ul class="dropdown-items">
                          <li class="combobox-item" v-for="(item, index) in arrLevel" :key="index"
                            @click="chooseLevel(index)" :class="{ 'chooseItem': levelSelected == index }"
                            style="text-align: left;">
                            <div class="combobox-item-con">
                              <div class="combobox-item--text">{{ item }} </div>
                              <div class="selected-container">
                                <div class="icon24 mi-checkbox-active" v-if="(levelSelected == index)">
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="form-group">
                  <label class="filter-label">Loại phong trào</label>
                  <div class="c-combobox combobox-level" v-click-outside="hideType">
                    <input class="page-limit input-level" type="text" :value="typeDefault">
                    <div class="icon-limit" @click="(dropType = !dropType)"></div>
                    <div class="dropdown-panel position-level--filter" v-show="dropType">
                      <div class="dropdown-body scroll">
                        <ul class="dropdown-items">
                          <li class="combobox-item" v-for="(item, index) in arrType" :key="index"
                            @click="chooseType(index)" :class="{ 'chooseItem': typeSelected == index }"
                            style="text-align: left;">
                            <div class="combobox-item-con">
                              <div class="combobox-item--text">{{ item }} </div>
                              <div class="selected-container">
                                <div class="icon24 mi-checkbox-active" v-if="(typeSelected == index)">
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="form-group">
                  <label class="filter-label">Trạng thái</label>
                  <div class="c-combobox combobox-level" v-click-outside="hideStatus">
                    <input class="page-limit input-level" type="text" :value="statusDefault">
                    <div class="icon-limit" @click="(dropStatus = !dropStatus)"></div>
                    <div class="dropdown-panel position-level--filter" v-show="dropStatus">
                      <div class="dropdown-body scroll">
                        <ul class="dropdown-items">
                          <li class="combobox-item" v-for="(item, index) in arrStatus" :key="index"
                            @click="chooseStatus(index)" :class="{ 'chooseItem': statusSelected == index }"
                            style="text-align: left;">
                            <div class="combobox-item-con">
                              <div class="combobox-item--text">{{ item }} </div>
                              <div class="selected-container">
                                <div class="icon24 mi-checkbox-active" v-if="(statusSelected == index)">
                                </div>
                              </div>
                            </div>
                          </li>
                        </ul>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="modal-footer box-footer">
                <div class="flex-row">
                  <div class="flex"></div>
                  <div class="flex-buttons">
                    <button class="btn btn-cancel" @click="(isShowFilter = !isShowFilter)">Huỷ</button>
                    <button class="btn btn-save" @click="(isShowFilter = !isShowFilter)" title="Ctrl + S">Áp
                      dụng</button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <button class="btn-addnew" :class="{ 'hide': countSelected }" @click="isClickAdd()"
        style="font-size: 14px; font-weight: 400 ;">
        <div class="icon-addnew"></div>
        Thêm danh hiệu
      </button>
      <div class="toolbar-right" v-show="!(countSelected == 0)">
        <div class="selected">Đã chọn <b>{{ countSelected }}</b></div>
        <div class="clear-selected">Bỏ chọn</div>
        <button class="use">Sử dụng</button>
        <button class="stop-use">Ngừng sử dụng</button>
        <button class="delete-selected">Xoá</button>
      </div>
    </div>
    <div class="table-wrap">
      <table class="data-table">
        <thead>
          <tr>
            <th class="column-checkbox">
              <label class="c-checkbox">
                <input type="checkbox" @click="checkAll()" v-model="isCheckAll">
                <span class="checkmark"
                  ></span>
              </label>
            </th>
            <th title="Tên danh hiệu thi đua" class="ce-name">Tên danh hiệu thi đua</th>
            <th title="Mã danh hiệu" class="ce-code">Mã danh hiệu</th>
            <th title="Đối tượng khen thưởng" class="reward-object">Đối tượng khen thưởng</th>
            <th title="Cấp khen thưởng" class="reward-level">Cấp khen thưởng</th>
            <th title="Loại phong trào" class="type-movement">Loại phong trào</th>
            <th title="Trạng thái" class="status">Trạng thái</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in dataTable" :key="index" @mouseenter="(hoverRow = index)"
            @mouseleave="(hoverRow = null)">
            <td class="column-checkbox">
              <label class="c-checkbox">
                <input type="checkbox" :value='index' v-model='isChecked' @change='updateCheckAll()'>
                <span class="checkmark"></span>
              </label>
            </td>
            <td class="ce-name text-align">
              <span>{{ item.name }}</span></td>
            <td class="ce-code">{{ item.code }}</td>
            <td class="reward-object">{{ displayObject(item.object) }}</td>
            <td class="reward-level">{{ item.level }}</td>
            <td title="Loại phong trào" class="type-movement">{{ displayType(item.type) }}</td>
            <td title="Trạng thái" class="status">
              <div class="flex-data">
                <div class="icon-stt">
                  <div class="img-stt" :class="{ 'not-active': item.status}"></div>
                </div>
                <div class="text">{{displayStatus(item.status)}}</div>
              </div>
            </td>
            <div class="action-menu" v-show="(hoverRow == index)">
              <div class="item-edit" title="Sửa" @click="isClickEdit()">
                <div class="icon-edit"></div>
              </div>
              <div class="item-del" title="Thêm nữa">
                <div class="icon-del"></div>
              </div>
            </div>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="footer-page">
      <div class="footer-left size14">Tổng số: <b>{{ dataTable.length }}</b> bản ghi</div>
      <div class="footer-right size 14">
        <div class="size14">Số bản ghi/trang</div>
          <div class="c-combobox" v-click-outside="onClickOutside">
            <input :value="setValue" readonly="readonly" class="page-limit" type="text">
            <div class="icon-limit" @click="clickPageLimit()"></div>
            <div class="dropdown-panel position-panel" v-show="isShowLimit" id="meomeo">
              <div class="dropdown-body scroll">
                <ul class="dropdown-items">
                  <li class="combobox-item" :class="{ 'chooseItem': (isSelected == index + 1) }"
                    v-for="(item, index) in arrPaging" :key="index" @click="chooseLimit(index)" style="text-align: left;">
                    <div class="combobox-item-con">
                      <div class="combobox-item--text"> {{ item }} </div>
                      <div class="selected-container">
                        <div class="icon24 mi-checkbox-active" v-if="(isSelected == index + 1)">
                        </div>
                      </div>
                    </div>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        <div class="size14"><b>{{ dataTable.length }}</b> bản ghi</div>
        <div class="btn-prev"></div>
        <div class="btn-next"></div>
      </div>
    </div>
  </div>
</template>

<script>
import emitter from '../js/event-bus.js'
import { ClickOutside } from "vue-click-outside-of";
export default {
  directives :{ ClickOutside },
  data() {
    return {
      tittleForm: null,
      isClick: false,
      isShow: false,
      showOptions: false,
      isShowLimit: false,
      isShowFilter: false,
      dropObject: false,  //ẩn hiện dropdown đối tượng trong filter panel
      dropLevel: false,  //ẩn hiện dropdown cấp bậc trong filter panel
      dropType: false,  //ẩn hiện dropdown loại trong filter panel
      dropStatus: false,  //ẩn hiện dropdown trạng thái trong filter panel

      objectSelected: 0,
      objectDefault: "Tất cả",
      arrObject: ["Tất cả", "Gia đình","Cá nhân","Tập thể", "Cá nhân và tập thể"],

      levelSelected: 0,
      levelDefault: "Tất cả",
      arrLevel: ["Tất cả", "Cấp Nhà nước", "Cấp Tỉnh/tương đương", "Cấp Huyện/tương đương", "Cấp Xã/tương đương"],

      typeSelected: 0,
      typeDefault: "Tất cả",
      arrType: ["Tất cả", "Thường xuyên", "Theo đợt"],

      statusSelected: 0,
      statusDefault: "Tất cả",
      arrStatus: ["Tất cả", "Sử dụng", "Ngừng sử dụng"],

      isSelected: 3,
      setValue: 50, // gtri ban đầu của limit/page
      isCheckAll: false,
      isChecked: [],
      arrPaging: [10, 20, 50, 100],
      countSelected: 0,
      indexEdit : null, // phần tử đã ấn edit
      dataTable: [
        { // data mẫu
          name: "Nội dung sẽ ẩn khi tên danh hiệu quá dài aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa",
          code: "LĐTTCX",
          object: 3,
          level: "Cấp Tỉnh/tương đương",
          type: 3,
          status: 0,
          notes : " data demo độ dài quá lớn"

        },
      ],
      hoverRow: null, // dòng được hover trong bảng
      searchText: null,
    }
  },
  watch: {
    /**
    * event : nhập vào input-search
    * result : hiện icon X khi nhập input-search
    * @author : Đào Trọng Khang 
    * @Created : 4/12/2022
    */
    searchText(val){
      if(val.length > 0){
        this.isShow = true
      }
      else{this.isShow = false}
    }
  },
  created() {
    emitter.on('sendData', (val) => {
      this.dataTable.unshift(val)

    }
    )
    emitter.on('sendEdit', (val)=>{
      this.dataTable[this.indexEdit] = val
    })
  },
  methods: {
    displayObject(input){
      let result = null ;
      result = this.arrObject[input+1]
      return result
    },
    displayType(input){
      let result = null ;
      if((input == 1) || (input == 2) ){ result = this.arrType[input]}
      if(input == 3){ result = "Thường xuyên; Theo đợt"}
      return result
    },
    displayStatus(input){
      let result = null ;
      if(input == 0){ result = "Ngừng sử dụng"}
      if(input == 1){ result = "Sử dụng"}
      return result
    },
    /** Click ngoài div để ẩn modal combobox
     * onClickOutside ; hideObject ; hideLevel ; hideType ; hideStatus
    * @author : Đào Trọng Khang 
    * @Created : 4/12/2022
    */
    onClickOutside() {
      this.isShowLimit = false;
    },
    hideObject() {
      this.dropObject = false;
    },
    hideLevel() {
      this.dropLevel = false;
    },
    hideType() {
      this.dropType = false;
    },
    hideStatus() {
      this.dropStatus = false;
    },


    /**
    * event : Click btn Thêm danh hiệu
    * result : hiện popup-modal Thêm danh hiệu
    * @author : Đào Trọng Khang 
    * @Created : 29/11/2022
    */
    isClickAdd() {
      this.isClick = true
      this.tittleForm = "Thêm"
      emitter.emit('addOnClick', [this.isClick, this.tittleForm])
    },
    /**
    * event : Click btn Sửa danh hiệu
    * result : hiện popup-modal Thêm danh hiệu
    * @author : Đào Trọng Khang 
    * @Created : 29/11/2022
    */
    isClickEdit() {
      this.isClick = true
      this.tittleForm = "Sửa"
      this.indexEdit = this.hoverRow;
      emitter.emit('editOnClick', [this.isClick, this.tittleForm, this.dataTable[this.hoverRow]])
    },

    /**
    * event : Click btn limit-per-page
    * result : hiện dropdown-menu chọn limit-record/page
    * @author : Đào Trọng Khang ( 28/11/2022 )
    * @Created : 29/11/2022
    */
    clickPageLimit() {
      this.isShowLimit = !this.isShowLimit
    },

    /**
    * event : Click item trong dropdown-menu limit-record
    * result : highlight + hiện icon active + ẩn dropdown
    * @author : Đào Trọng Khang 
    * @Created : 29/11/2022
    */
    chooseLimit(number) {
      this.isSelected = number + 1;
      this.isShowLimit = false;
      this.setValue = this.arrPaging[number]
    },
    /**
    * (chooseObject,chooseLevel,chooseType,chooseStatus)
    * event : Click item trong dropdown-menu filter
    * result : highlight + hiện icon active + ẩn dropdown
    * @author : Đào Trọng Khang 
    * @Created : 30/11/2022 
    */
    chooseObject(input) {
      this.objectSelected = input;
      this.dropObject = false;
      this.objectDefault = this.arrObject[input]
    },
    chooseLevel(input) {
      this.levelSelected = input;
      this.dropLevel = false;
      this.levelDefault = this.arrLevel[input]
    },
    chooseType(input) {
      this.typeSelected = input;
      this.dropType = false;
      this.typeDefault = this.arrType[input]
    },
    chooseStatus(input) {
      this.statusSelected = input;
      this.dropStatus = false;
      this.statusDefault = this.arrStatus[input]
    },
    /**
    * event : Chọn tất cả record trong table
    * result : Hiện options + đếm số record được chọn 
    * @author : Đào Trọng Khang 
    * @Created : 29/11/2022
    */
    checkAll() {
      this.isCheckAll = !this.isCheckAll;
      this.isChecked = [];
      let i = 0;
      if (this.isCheckAll) {
        while (i < this.dataTable.length) {
          this.isChecked.push(i);
          i++;
        }
        this.countRecordSelected()
      }
      else { this.countRecordSelected() }
    },
    /**
    * event : kiểm tra số record được chọn = tổng số record ko 
    * result : giá trị biến isCheckAll
    * @author : Đào Trọng Khang
    * @Created : 29/11/2022
    */
    updateCheckAll() {
      if (this.isChecked.length == this.dataTable.length) {
        this.isCheckAll = true;
      } else {
        this.isCheckAll = false;
      }
      this.countRecordSelected()
    },
    /**
    * event :đếm số record được chọntrong table
    * result : giá trị biến countSelected
    * @author : Đào Trọng Khang 
    * @Created : 29/11/2022
    */
    countRecordSelected() {
      this.countSelected = 0;
      let i = 0
      // Read Checked checkboxes value
      while (i < this.isChecked.length) {
        this.countSelected++;
        i++;
      }
    },
  },
}


</script>

<style scoped>
@import url(../styles/content.css);
@import url(../styles/table.css);
@import url(../styles/checkbox.css);
@import url(../styles/combobox.css);
@import url(../styles/modal.css);

.hide {
  display: none !important;
}

.content {
  display: flex;
  flex-direction: column;
  position: relative;
  height: calc(100vh - 56px);
  width: calc(100vw - 220px);
  top: 0px;
  padding: 16px;
  background-color: #F4F5F8;
  transition: width 0.3s ease;
  flex-shrink: 0;
  margin: 0px 0px 0px 0px;
  box-shadow: #1b0c0121 2px 2px 2px 2px;
}
.text-align{
  position: relative;
}

.text-align:before {
  content: ' ';
  visibility: hidden;
}

.text-align span {
  position: absolute;
  left: 8px;
  right: 0;
  top:11px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
</style>