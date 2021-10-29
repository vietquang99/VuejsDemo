<template>
  <div
    ref="dialogForm"
    id="dlgEmployeeForm"
    class="m-dialog"
    :class="{ 'm-dialog-show': isShow }"
  >
    <div class="m-dialog-modal"></div>
    <div class="m-dialog-box">
      <div class="m-dialog-header">
        <div class="m-dialog-title">THÔNG TIN NHÂN VIÊN</div>
        <div class="m-dialog-close" @click="btnCloseOnClick"></div>
      </div>
      <div class="m-dialog-content">
        <div class="m-dialog-content-left">
          <button class="m-btn-change-avatar m-default-avatar-icon"></button>
          <label for=""
            >(Vui lòng chọn ảnh có định dạng <br />.jpg .png .gif .jpeg)</label
          >
        </div>
        <div class="m-dialog-content-right">
          <div class="m-right-label">A. THÔNG TIN CHUNG:</div>
          <div class="m-common-info">
            <div class="m-input-box-left">
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box"
                  >Mã nhân viên(<mark class="mark-red">*</mark>)</label
                >
                <input
                  id="txtEmployeeCode"
                  ref="txtEmployeeCode"
                  type="text"
                  fieldName="EmployeeCode"
                  tabindex="1"
                  required
                  v-model="employee.EmployeeCode"
                />
              </div>
              <div class="m-input-box-with-label">
                <label class="m-label-input-box">Ngày sinh</label>
                <input
                  id="DateOfBirth"
                  type="date"
                  fieldName="DateOfBirth"
                  tabindex="3"
                  format="ddmmyyyy"
                  v-model="employee.DateOfBirth"
                />
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box"
                  >Số CMTND/Căn cước (<mark class="mark-red">*</mark>)</label
                >
                <input
                  id="txtIdentityNumber"
                  type="text"
                  fieldName="IdentityNumber"
                  tabindex="5"
                  :class="{ errorIdentityNumber: errorIdentityNumber.status }"
                  v-bind:title="messenger"
                  v-model="employee.IdentityNumber"
                  required
                />
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box">Nơi cấp</label>
                <input
                  id="txtIdentityPlace"
                  type="text"
                  fieldName="IdentityPlace"
                  v-model="employee.IdentityPlace"
                  tabindex="7"
                />
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box"
                  >Email(<mark class="mark-red">*</mark>)</label
                >
                <input
                  id="txtEmail"
                  type="text"
                  fieldName="Email"
                  tabindex="8"
                  v-model="employee.Email"
                  v-bind:title="messenger"
                  :class="{ errorEmail: errorEmail.status }"
                  required
                />
              </div>
            </div>
            <div class="m-input-box-right">
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box"
                  >Họ và tên(<mark class="mark-red">*</mark>)</label
                >
                <input
                  id="txtFullName"
                  type="text"
                  fieldName="FullName"
                  :class="{ errorFullName: errorFullName.status }"
                  v-bind:title="messenger"
                  v-model="employee.FullName"
                  tabindex="2"
                  required
                />
              </div>
              <div style="height: 40px">
                <div class="m-combobox" id="cbbGender">
                  <div class="m-combobox-label">Giới tính</div>
                  <div class="select-list" value="">
                    <div class="select-item" value="1">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Nam</div>
                    </div>
                    <div class="select-item" value="0">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Nữ</div>
                    </div>
                    <div class="select-item" value="2">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Khác</div>
                    </div>
                  </div>
                  <div class="select">
                    <input
                      class="m-combobox-input"
                      type="text"
                      placeholder="Chọn/Nhập thông tin"
                      value=""
                      tabindex="4"
                      id="genderTxt"
                      fieldname="Gender"
                      format="Gender"
                    />
                    <div class="m-combobox-button">
                      <i class="fas fa-angle-down"></i>
                    </div>
                  </div>
                </div>
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box">Ngày cấp</label>
                <input
                  id="txtIdentityDate"
                  type="date"
                  fieldName="IdentityDate"
                  tabindex="6"
                  format="ddmmyyyy"
                  ref="date"
                  v-model="employee.IdentityDate"
                />
              </div>
              <div
                class="m-input-box-with-label"
                style="position: absolute; bottom: 0"
              >
                <label for="" class="m-label-input-box">Số điện thoại</label>
                <input
                  id="txtPhoneNumber"
                  type="text"
                  fieldName="PhoneNumber"
                  tabindex="9"
                  :class="{ errorPhoneNumber: errorPhoneNumber.status }"
                  v-bind:title="messenger"
                  v-model="employee.PhoneNumber"
                />
              </div>
            </div>
          </div>
          <div class="m-right-label">B. THÔNG TIN CÔNG VIỆC:</div>
          <div class="m-work-info">
            <div class="m-input-box-left">
              <div style="height: 40px">
                <div
                  class="m-combobox"
                  id="cbbPosition"
                  cbbname="PositionName"
                  cbbid="PositionId"
                >
                  <div class="m-combobox-label">Vị trí</div>
                  <div class="select-list" value=""></div>
                  <div class="select">
                    <input
                      class="m-combobox-input"
                      type="text"
                      placeholder="Chọn/Nhập thông tin"
                      value=""
                      tabindex="10"
                      id="txtPosition"
                      fieldname="PositionId"
                      format="position"
                    />
                    <div class="m-combobox-button">
                      <i class="fas fa-angle-down"></i>
                    </div>
                  </div>
                </div>
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box"
                  >Mã số thuế cá nhân</label
                >
                <input
                  id="txtTaxNumber"
                  type="text"
                  fieldName="PersonalTaxCode"
                  v-model="employee.PersonalTaxCode"
                  tabindex="12"
                />
              </div>
              <div class="m-input-box-with-label" style="margin-bottom: 24px">
                <label for="" class="m-label-input-box"
                  >Ngày gia nhập công ty</label
                >
                <input
                  id="txtJoinDate"
                  type="date"
                  fieldName="JoinDate"
                  tabindex="14"
                  format="ddmmyyyy"
                  v-model="employee.JoinDate"
                />
              </div>
            </div>
            <div class="m-input-box-right" style="margin-left: 3px">
              <div style="height: 40px">
                <div
                  class="m-combobox"
                  id="cbbDepartment"
                  cbbname="DepartmentName"
                  cbbid="DepartmentId"
                >
                  <div class="m-combobox-label">Phòng ban</div>
                  <div class="select-list" style="z-index: 100"></div>
                  <div class="select">
                    <input
                      class="m-combobox-input"
                      type="text"
                      placeholder="Chọn/Nhập thông tin"
                      value=""
                      tabindex="11"
                      id="txtDepartment"
                      fieldname="DepartmentId"
                      format="department"
                    />
                    <div class="m-combobox-button">
                      <i class="fas fa-angle-down"></i>
                    </div>
                  </div>
                </div>
              </div>
              <div class="m-input-box-with-label">
                <label for="" class="m-label-input-box">Mức lương cơ bản</label>
                <input
                  id="txtSalary"
                  type="text"
                  fieldName="Salary"
                  tabindex="13"
                  format="Salary"
                  style="text-align: right"
                  v-model="employee.Salary"
                />
              </div>

              <div style="height: 40px">
                <div class="m-combobox" id="cbbWorkStatus">
                  <div class="m-combobox-label">Tình trạng công việc</div>
                  <div class="select-list" value="">
                    <div class="select-item" value="0">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Đang thử việc</div>
                    </div>
                    <div class="select-item" value="1">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Đang làm việc</div>
                    </div>
                    <div class="select-item" value="2">
                      <i class="fas fa-check"></i>
                      <div class="select-item-text">Đã nghỉ việc</div>
                    </div>
                  </div>
                  <div class="select">
                    <input
                      class="m-combobox-input"
                      type="text"
                      placeholder="Chọn/Nhập thông tin"
                      value=""
                      tabindex="15"
                      id="txtWorkStatus"
                      fieldname="WorkStatus"
                      format="workStatus"
                    />
                    <div class="m-combobox-button">
                      <i class="fas fa-angle-down"></i>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="m-dialog-footer">
        <div class="m-dialog-button">
          <button class="m-cancel-btn" tabindex="17" @click="btnCloseOnClick">
            Hủy
          </button>
          <button
            id="btnSave"
            class="m-btn m-save-btn"
            tabindex="16"
            @click="btnSaveOnClick"
          >
            <i class="fal fa-save style" style="padding-right: 8px"></i>Lưu
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Enum from "../../scripts/enum";
import Resource from "../../scripts/resource";
export default {
  name: "EmployeeForm",
  props: {
    employeeId: {
      type: String,
      default: "",
    },
    formMode: Number,
  },
  data() {
    return {
      isShow: false,
      messenger: "",
      errorFullName: {
        status: false,
      },
      errorIdentityNumber: {
        status: false,
      },
      errorEmail: {
        status: false,
      },
      errorPhoneNumber: {
        status: false,
      },
      employee: {
        EmployeeCode: null,
        FullName: "",
        PhoneNumber: "",
        Email: "",
        Salary: null,
        DateOfBirth: null,
        IdentityNumber: "",
        IdentityPlace: null,
        PersonalTaxCode: null,
        IdentityDate: null,
        JoinDate: null,
      },
    };
  },

  methods: {
    /**Tạo sự kiện cho nút X đóng dialog */
    btnCloseOnClick() {
      this.isShow = false;
      // Gọi lại hàm showDialogDetail của component cha:
      this.$emit("showDialogForm", false, Enum.FormMode.Default);
    },
    /**Tạo sự kiện cho nút Lưu (Lưu khách hàng) */
    btnSaveOnClick() {
      let me = this;
      // Thực hiện validate dữ liệu:
      let isValid = me.validateData();
      if (isValid) {
        // Dữ liệu đã hợp lệ thì thực hiện cất dữ liệu:
        if (me.formMode == Enum.FormMode.Add) {
          axios
            .post("http://cukcuk.manhnv.net/api/v1/Employees", me.employee)
            .then(function () {
              alert("Thêm mới thành công!");
              me.loadData();
              me.isShow = false;
            })
            .catch(function (res) {
              console.log(res);
            });
        } else {
          console.log("Cất dữ liệu đã chỉnh sửa");
        }
      }
    },
    /** Validate dữ liệu */
    // Họ tên không được để trống //
    validateData() {
      let isValid = true;
      if (this.employee.FullName == "") {
        isValid = false;
        this.errorFullName = {
          status: true,
        };
        this.messenger = Resource.VN.Alert.Blank;
      } else {
        this.errorFullName = {
          status: false,
        };
      }
      if (this.employee.IdentityNumber == "") {
        isValid = false;
        this.errorIdentityNumber = {
          status: true,
        };
        this.messenger = Resource.VN.Alert.Blank;
      } else {
        this.errorIdentityNumber = {
          status: false,
        };
      }
      if (this.employee.Email == "") {
        isValid = false;
        this.errorEmail = {
          status: true,
        };
        this.messenger = Resource.VN.Alert.Blank;
      } else {
        this.errorEmail = {
          status: false,
        };
      }
      if (this.employee.PhoneNumber == "") {
        isValid = false;
        this.errorPhoneNumber = {
          status: true,
        };
        this.messenger = Resource.VN.Alert.Blank;
      } else {
        this.errorPhoneNumber = {
          status: false,
        };
      }
      return isValid;
    },
    /** Chuyển đổi date từ json sang dạng yyyy-mm-dd */
    dateToString(value) {
      if (!value) return "";
      else {
        value = new Date(value);
        let date = value.getDate();
        date = date < 10 ? `0${date}` : date;
        let month = value.getMonth() + 1;
        month = month < 10 ? `0${month}` : month;
        let year = value.getFullYear();
        value = year + "-" + month + "-" + date;
        return value;
      }
    },
    /** Load data */
    loadData() {
      var me = this;
      // Gọi api lấy dữ liệu
      axios
        .get("http://cukcuk.manhnv.net/api/v1/Employees")
        .then(function (res) {
          me.employees = res.data;
        })
        .catch(function (res) {
          console.log(res);
        });
    },
    /** Thực hiện lấy mã khách hàng mới */
    getNewEmployeeCode() {
      let me = this;
      axios
        .get("http://cukcuk.manhnv.net/api/v1/Employees/NewEmployeeCode")
        .then(function (res) {
          me.employee.EmployeeCode = res.data;
          // Focus vào ô nhập liệu đầu tiên:
          me.$refs.txtEmployeeCode.focus();
        })
        .catch(function () {
          console.log("Lỗi!");
        });
    },
  },
  watch: {
    formMode: function () {
      let me = this;
      switch (this.formMode) {
        case Enum.FormMode.Add:
          // TH thêm mới, thực hiện lấy mã khách hàng mới:
          me.getNewEmployeeCode();
          me.isShow = true;
          break;
        case Enum.FormMode.Edit:
          // TH sửa thực hiện lấy thông tin khách hàng mới:
          axios
            .get(`http://cukcuk.manhnv.net/api/v1/Employees/${me.employeeId}`)
            .then(function (res) {
              me.employee = res.data;
              me.employee.DateOfBirth = me.dateToString(res.data.DateOfBirth);
              me.employee.IdentityDate = me.dateToString(res.data.IdentityDate);
              me.employee.JoinDate = me.dateToString(res.data.JoinDate);
            })
            .catch(function () {
              console.log("api lỗi!");
            });
          me.isShow = true;
          break;
        default:
          break;
      }
    },
  },
};
</script>

<style scoped>
@import url("../../styles/component/dialog.css");
@import url("../../styles/component/validate.css");
</style>