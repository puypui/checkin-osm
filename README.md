<!DOCTYPE html>
<html>
<head>
  <base target="_top">
  <title>ระบบเช็คชื่อ อสม.ออนไลน์</title>
  <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
  <script type="text/javascript" src="https://www.gstatic.com/charts/loader.js"></script>
  <style>
    /* CSS Styles สำหรับการออกแบบ UI */
    body {
      font-family: 'Sarabun', sans-serif; /* ใช้ Sarabun font สำหรับภาษาไทย */
      margin: 0;
      padding: 0;
      background-color: #f0f8f0; /* สีพื้นหลังเขียวอ่อน */
      color: #333;
    }
    .container {
      max-width: 960px;
      margin: 20px auto;
      background-color: #fff;
      padding: 30px;
      border-radius: 8px;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }
    header {
      text-align: center;
      margin-bottom: 30px;
      padding-bottom: 15px;
      border-bottom: 1px solid #e0e0e0;
    }
    h1 {
      font-size: 2.8em; /* ขนาดหัวข้อใหญ่ */
      color: #2e8b57; /* สีเขียวเข้ม */
      margin-bottom: 5px;
      font-weight: bold; /* ตัวหนา */
    }
    h2 {
      font-size: 1.2em; /* ขนาดชื่อโรงพยาบาลเล็กกว่าเล็กน้อย */
      color: #666;
      margin-top: 5px;
    }
    .nav-tabs {
      display: flex;
      justify-content: center;
      margin-bottom: 20px;
      border-bottom: 2px solid #e0e0e0;
      flex-wrap: wrap; /* ให้แท็บสามารถขึ้นบรรทัดใหม่ได้ถ้าหน้าจอเล็ก */
    }
    .nav-tabs button {
      background-color: #f0f0f0;
      border: none;
      padding: 12px 20px;
      cursor: pointer;
      font-size: 1em;
      border-radius: 8px 8px 0 0;
      transition: background-color 0.3s ease;
      color: #555;
      display: flex;
      align-items: center;
      gap: 8px;
      margin: 0 2px;
    }
    .nav-tabs button:hover {
      background-color: #e0e0e0;
    }
    .nav-tabs button.active {
      background-color: #2e8b57; /* สีเขียวสำหรับแท็บที่ active */
      color: #fff;
      border-bottom: 2px solid #2e8b57;
    }
    .tab-content {
      padding: 20px 0;
      display: none; /* ซ่อนแท็บทั้งหมดตามค่าเริ่มต้น */
    }
    .tab-content.active {
      display: block; /* แสดงแท็บที่ active */
    }
    .form-group {
      margin-bottom: 15px;
    }
    label {
      display: block;
      margin-bottom: 8px;
      font-weight: bold;
      color: #444;
    }
    select, input[type="date"], input[type="text"], textarea {
      width: 100%;
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 1em;
      box-sizing: border-box; /* รวม padding ในความกว้าง */
    }
    textarea {
      resize: vertical;
      min-height: 80px;
    }
    .attendance-list {
      margin-top: 20px;
      border-top: 1px solid #eee;
      padding-top: 20px;
    }
    .aor-sor-mor-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 10px 0;
      border-bottom: 1px dashed #eee;
      flex-wrap: wrap; /* ให้รายการสามารถขึ้นบรรทัดใหม่ได้ */
    }
    .aor-sor-mor-item:last-child {
      border-bottom: none;
    }
    .aor-sor-mor-info {
      flex-grow: 1;
      font-size: 1.1em;
      color: #333;
      min-width: 200px; /* กันไม่ให้ข้อความเล็กเกินไป */
    }
    .attendance-status {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
      margin-top: 5px;
    }
    .attendance-status label {
      display: flex;
      align-items: center;
      cursor: pointer;
      font-weight: normal;
      color: #555;
      margin-bottom: 0;
    }
    .attendance-status input[type="radio"] {
      margin-right: 5px;
      transform: scale(1.2); /* ทำให้ radio button ใหญ่ขึ้นเล็กน้อย */
      width: auto; /* ไม่ให้มันยืดเต็ม 100% */
    }
    button[type="submit"], .btn {
      background-color: #2e8b57;
      color: white;
      padding: 12px 25px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1.1em;
      transition: background-color 0.3s ease;
      display: flex;
      align-items: center;
      gap: 8px;
      margin-top: 20px;
    }
    button[type="submit"]:hover, .btn:hover {
      background-color: #3cb371; /* สีเขียวที่เข้มขึ้นเมื่อ hover */
    }
    .message {
      margin-top: 20px;
      padding: 12px;
      background-color: #d4edda;
      color: #155724;
      border: 1px solid #c3e6cb;
      border-radius: 5px;
      text-align: center;
      font-weight: bold;
      display: none; /* ซ่อนตามค่าเริ่มต้น */
    }
    .message.error {
      background-color: #f8d7da;
      color: #721c24;
      border-color: #f5c6cb;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 20px;
    }
    th, td {
      border: 1px solid #ddd;
      padding: 10px;
      text-align: left;
    }
    th {
      background-color: #e6ffe6; /* สีเขียวอ่อนสุด */
      color: #333;
      font-weight: bold;
    }
    tr:nth-child(even) {
      background-color: #f9f9f9;
    }
    .stats-card {
      background-color: #e6ffe6;
      border-left: 5px solid #2e8b57;
      padding: 15px;
      margin-bottom: 15px;
      border-radius: 5px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    .stats-card strong {
      font-size: 1.5em;
      color: #2e8b57;
    }
    .stats-card span {
      font-size: 1.1em;
      color: #555;
    }
    #chart_div {
      width: 100%;
      height: 400px;
      margin-top: 20px;
    }
    .export-button-container {
      text-align: right;
      margin-top: 20px;
    }
    .add-aorsormor-form, .edit-aorsormor-form {
      display: flex;
      flex-direction: column;
      gap: 15px;
      margin-top: 20px;
      border-top: 1px solid #eee;
      padding-top: 20px;
    }
    .add-aorsormor-form div, .edit-aorsormor-form div {
      display: flex;
      flex-direction: column;
    }
    .add-aorsormor-form label, .edit-aorsormor-form label {
      margin-bottom: 5px;
    }
    .add-aorsormor-form input, .edit-aorsormor-form input {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 1em;
    }
    .aorsormor-management-list {
        margin-top: 20px;
    }
    .aorsormor-management-item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px 0;
        border-bottom: 1px dashed #eee;
    }
    .aorsormor-management-item:last-child {
        border-bottom: none;
    }
    .aorsormor-management-actions button {
        background-color: #ffc107; /* สีเหลืองสำหรับแก้ไข */
        color: #333;
        padding: 8px 12px;
        border: none;
        border-radius: 4px;
        cursor: pointer;
        font-size: 0.9em;
        margin-left: 5px;
        display: inline-flex; /* จัดให้ไอคอนและข้อความอยู่บรรทัดเดียวกัน */
        align-items: center;
        gap: 5px;
    }
    .aorsormor-management-actions button.delete-btn {
        background-color: #dc3545; /* สีแดงสำหรับลบ */
        color: white;
    }
    .aorsormor-management-actions button:hover {
        opacity: 0.9;
    }
    /* Modal styles */
    .modal {
      display: none; /* ซ่อนตามค่าเริ่มต้น */
      position: fixed; /* อยู่กับที่บนหน้าจอ */
      z-index: 1; /* อยู่เหนือเนื้อหาอื่น */
      left: 0;
      top: 0;
      width: 100%; /* เต็มความกว้าง */
      height: 100%; /* เต็มความสูง */
      overflow: auto; /* มี scrollbar ถ้าเนื้อหาเกิน */
      background-color: rgba(0,0,0,0.4); /* พื้นหลังทึบแสง */
    }
    .modal-content {
      background-color: #fefefe;
      margin: 15% auto; /* จัดกึ่งกลางแนวตั้งและแนวนอน */
      padding: 20px;
      border: 1px solid #888;
      width: 80%; /* ความกว้างของ Modal */
      max-width: 500px; /* จำกัดความกว้างสูงสุด */
      border-radius: 8px;
      position: relative;
    }
    .close-button {
      color: #aaa;
      float: right;
      font-size: 28px;
      font-weight: bold;
    }
    .close-button:hover,
    .close-button:focus {
      color: black;
      text-decoration: none;
      cursor: pointer;
    }
    .records-filter-group {
      display: flex;
      gap: 10px;
      margin-bottom: 20px;
      align-items: center;
    }
    .records-filter-group label {
      margin-bottom: 0;
    }
  </style>
</head>
<body>
  <div class="container">
    <header>
      <h1>ระบบเช็คชื่อ อสม.ออนไลน์</h1>
      <h2>โรงพยาบาลส่งเสริมสุขภาพตำบลบ้านบึงปลาทู</h2>
    </header>

    <div class="nav-tabs">
      <button class="tab-button active" data-tab="checkin"><i class="material-icons">how_to_reg</i> เช็คชื่อ</button>
      <button class="tab-button" data-tab="records"><i class="material-icons">list_alt</i> รายละเอียดการเช็คชื่อ</button>
      <button class="tab-button" data-tab="status"><i class="material-icons">event_note</i> สถานะการบันทึก</button>
      <button class="tab-button" data-tab="statistics"><i class="material-icons">bar_chart</i> สถิติ</button>
      <button class="tab-button" data-tab="manage-aorsormor"><i class="material-icons">group_add</i> จัดการ อสม.</button>
    </div>

    <div id="checkin" class="tab-content active">
      <form id="attendanceForm">
        <div class="form-group">
          <label for="date"><i class="material-icons">calendar_today</i> เลือกวันที่:</label>
          <input type="date" id="date" name="date" required>
        </div>

        <div class="form-group">
          <label for="village_checkin"><i class="material-icons">location_on</i> เลือกหมู่บ้าน:</label>
          <select id="village_checkin" name="village" required>
            <option value="">-- เลือกหมู่บ้าน --</option>
            <option value="ม.1">ม.1</option>
            <option value="ม.2">ม.2</option>
            <option value="ม.3">ม.3</option>
            <option value="ม.4">ม.4</option>
            <option value="ม.5">ม.5</option>
            <option value="ม.6">ม.6</option>
            <option value="ม.7">ม.7</option>
            <option value="ม.8">ม.8</option>
            <option value="ม.9">ม.9</option>
          </select>
        </div>

        <div class="form-group">
          <label for="mainActivity"><i class="material-icons">event</i> เลือกกิจกรรม:</label>
          <select id="mainActivity" name="mainActivity" required>
            <option value="">-- เลือกกิจกรรมหลัก --</option>
            <option value="ประชุมประจำเดือน">ประชุมประจำเดือน</option>
            <option value="ในตำบลบึงปลาทู">ในตำบลบึงปลาทู</option>
            <option value="นอกตำบลบึงปลาทู">นอกตำบลบึงปลาทู</option>
            <option value="ระดับจังหวัดอำเภอ">ระดับจังหวัดอำเภอ</option>
            <option value="ระดับจังหวัด">ระดับจังหวัด</option>
            <option value="นอกจังหวัด">นอกจังหวัด</option>
          </select>
        </div>

        <div class="form-group">
          <label for="subActivity"><i class="material-icons">description</i> กิจกรรมย่อย (ไม่เกิน 100 คำ):</label>
          <textarea id="subActivity" name="subActivity" maxlength="100"></textarea>
        </div>

        <h3><i class="material-icons">group</i> รายชื่อ อสม.</h3>
        <div id="aorSorMoList" class="attendance-list">
          <p>กรุณาเลือกหมู่บ้านเพื่อแสดงรายชื่อ อสม.</p>
        </div>

        <div class="message" id="saveMessage"></div>
        <button type="submit" class="btn"><i class="material-icons">save</i> บันทึก</button>
      </form>
    </div>

    <div id="records" class="tab-content">
      <h3><i class="material-icons">view_list</i> รายละเอียดการเช็คชื่อในแต่ละวัน</h3>
      <div class="records-filter-group">
        <label for="village_records"><i class="material-icons">location_on</i> กรองตามหมู่บ้าน:</label>
        <select id="village_records">
          <option value="">-- แสดงทั้งหมด --</option>
          <option value="ม.1">ม.1</option>
          <option value="ม.2">ม.2</option>
          <option value="ม.3">ม.3</option>
          <option value="ม.4">ม.4</option>
          <option value="ม.5">ม.5</option>
          <option value="ม.6">ม.6</option>
          <option value="ม.7">ม.7</option>
          <option value="ม.8">ม.8</option>
          <option value="ม.9">ม.9</option>
        </select>
      </div>
      <table id="attendanceRecordsTable">
        <thead>
          <tr>
            <th>วันที่</th>
            <th>หมู่บ้าน</th>
            <th>กิจกรรมหลัก</th>
            <th>กิจกรรมย่อย</th>
            <th>เลขที่ อสม.</th>
            <th>ชื่อ-สกุล อสม.</th>
            <th>สถานะ</th>
            <th>รายละเอียด</th>
          </tr>
        </thead>
        <tbody>
          </tbody>
      </table>
    </div>

    <div id="status" class="tab-content">
      <h3><i class="material-icons">check_circle_outline</i> สถานะการบันทึกทั้งหมด</h3>
      <table id="fullAttendanceStatusTable">
        <thead>
          <tr>
            <th>วันที่</th>
            <th>หมู่บ้าน</th>
            <th>กิจกรรมหลัก</th>
            <th>กิจกรรมย่อย</th>
            <th>จำนวนผู้มา</th>
            <th>จำนวนผู้ไม่มา</th>
            <th>จำนวนผู้ลา</th>
            <th>จำนวนผู้ไม่เข้าร่วม</th>
            <th>รวม</th>
          </tr>
        </thead>
        <tbody>
          </tbody>
      </table>
    </div>

    <div id="statistics" class="tab-content">
      <h3><i class="material-icons">insights</i> สถิติการเช็คชื่อ</h3>
      <div class="stats-card">
        <span><i class="material-icons">people_alt</i> จำนวน อสม. ทั้งหมด:</span>
        <strong id="totalAorSorMor">0</strong>
      </div>
      <div class="stats-card">
        <span><i class="material-icons">event_available</i> จำนวนการบันทึกการเช็คชื่อทั้งหมด (กิจกรรมที่ไม่ซ้ำ):</span>
        <strong id="totalAttendanceRecords">0</strong>
      </div>
      <div id="chart_div"></div> <div class="export-button-container">
        <button id="exportExcelBtn" class="btn"><i class="material-icons">download</i> ส่งออกข้อมูลเป็น Excel</button>
      </div>
    </div>

    <div id="manage-aorsormor" class="tab-content">
      <h3><i class="material-icons">person_add_alt_1</i> เพิ่มรายชื่อ อสม.</h3>
      <form id="addAorSorMorForm" class="add-aorsormor-form">
        <div>
          <label for="aorsormorId"><i class="material-icons">vpn_key</i> เลขที่:</label>
          <input type="text" id="aorsormorId" name="id" required>
        </div>
        <div>
          <label for="aorsormorName"><i class="material-icons">badge</i> ชื่อ-สกุล:</label>
          <input type="text" id="aorsormorName" name="name" required>
        </div>
        <div>
          <label for="aorsormorVillage"><i class="material-icons">home</i> หมู่:</label>
          <input type="text" id="aorsormorVillage" name="village" required>
        </div>
        <div class="message" id="addAorSorMorMessage"></div>
        <button type="submit" class="btn"><i class="material-icons">add_box</i> เพิ่ม อสม.</button>
      </form>

      <h3><i class="material-icons">list</i> รายชื่อ อสม. ทั้งหมด (แก้ไข/ลบ)</h3>
      <div id="aorsormorManagementList" class="aorsormor-management-list">
        <p>กำลังโหลดรายชื่อ อสม. ...</p>
      </div>
    </div>

  </div>

  <div id="editAorSorMorModal" class="modal">
    <div class="modal-content">
      <span class="close-button" id="closeEditModal">&times;</span>
      <h3><i class="material-icons">edit</i> แก้ไขรายชื่อ อสม.</h3>
      <form id="editAorSorMorForm" class="edit-aorsormor-form">
        <input type="hidden" id="editAorSorMorOriginalId"> <div>
          <label for="editAorSorMorId"><i class="material-icons">vpn_key</i> เลขที่:</label>
          <input type="text" id="editAorSorMorId" name="id" required>
        </div>
        <div>
          <label for="editAorSorMorName"><i class="material-icons">badge</i> ชื่อ-สกุล:</label>
          <input type="text" id="editAorSorMorName" name="name" required>
        </div>
        <div>
          <label for="editAorSorMorVillage"><i class="material-icons">home</i> หมู่:</label>
          <input type="text" id="editAorSorMorVillage" name="village" required>
        </div>
        <div class="message" id="editAorSorMorMessage"></div>
        <button type="submit" class="btn"><i class="material-icons">save</i> บันทึกการแก้ไข</button>
      </form>
    </div>
  </div>

  <div id="aorSorMorDetailModal" class="modal">
    <div class="modal-content">
      <span class="close-button" id="closeDetailModal">&times;</span>
      <h3><i class="material-icons">person</i> รายละเอียดกิจกรรมของ อสม. <span id="detailAorSorMorName"></span></h3>
      <table id="aorSorMorDetailTable">
        <thead>
          <tr>
            <th>วันที่</th>
            <th>กิจกรรมหลัก</th>
            <th>กิจกรรมย่อย</th>
            <th>สถานะ</th>
          </tr>
        </thead>
        <tbody>
          </tbody>
      </table>
    </div>
  </div>

  <script>
    // JavaScript Code สำหรับจัดการการทำงานของ UI
    document.addEventListener('DOMContentLoaded', function() {
      const attendanceForm = document.getElementById('attendanceForm');
      const saveMessage = document.getElementById('saveMessage');
      const aorSorMoListDiv = document.getElementById('aorSorMoList');
      const villageSelectCheckin = document.getElementById('village_checkin'); // ตัวเลือกหมู่บ้านในแท็บเช็คชื่อ
      const villageSelectRecords = document.getElementById('village_records'); // ตัวเลือกหมู่บ้านในแท็บรายละเอียด
      const attendanceRecordsTableBody = document.querySelector('#attendanceRecordsTable tbody');
      const fullAttendanceStatusTableBody = document.querySelector('#fullAttendanceStatusTable tbody');
      const totalAorSorMorSpan = document.getElementById('totalAorSorMor');
      const totalAttendanceRecordsSpan = document.getElementById('totalAttendanceRecords');
      const addAorSorMorForm = document.getElementById('addAorSorMorForm');
      const addAorSorMorMessage = document.getElementById('addAorSorMorMessage');
      const aorsormorManagementListDiv = document.getElementById('aorsormorManagementList');
      const exportExcelBtn = document.getElementById('exportExcelBtn');

      const editAorSorMorModal = document.getElementById('editAorSorMorModal');
      const closeEditModalButton = document.getElementById('closeEditModal');
      const editAorSorMorForm = document.getElementById('editAorSorMorForm');
      const editAorSorMorMessage = document.getElementById('editAorSorMorMessage');

      const aorSorMorDetailModal = document.getElementById('aorSorMorDetailModal');
      const closeDetailModalButton = document.getElementById('closeDetailModal');
      const detailAorSorMorNameSpan = document.getElementById('detailAorSorMorName');
      const aorSorMorDetailTableBody = document.querySelector('#aorSorMorDetailTable tbody');

      const tabButtons = document.querySelectorAll('.tab-button');
      const tabContents = document.querySelectorAll('.tab-content');

      // ตั้งค่าวันที่เริ่มต้นในฟอร์มเช็คชื่อเป็นวันปัจจุบัน
      const today = new Date();
      const yyyy = today.getFullYear();
      const mm = String(today.getMonth() + 1).padStart(2, '0'); // เดือนเริ่มจาก 0
      const dd = String(today.getDate()).padStart(2, '0');
      document.getElementById('date').value = `${yyyy}-${mm}-${dd}`;

      // จัดการการเปลี่ยนแท็บเมนู
      tabButtons.forEach(button => {
        button.addEventListener('click', () => {
          const tabId = button.dataset.tab;

          // ซ่อนแท็บทั้งหมดและลบสถานะ active
          tabButtons.forEach(btn => btn.classList.remove('active'));
          tabContents.forEach(content => content.classList.remove('active'));

          // แสดงแท็บที่เลือกและเพิ่มสถานะ active
          button.classList.add('active');
          document.getElementById(tabId).classList.add('active');

          // โหลดข้อมูลเฉพาะเมื่อเปลี่ยนไปยังแท็บที่เกี่ยวข้อง
          if (tabId === 'records') {
            loadAttendanceRecords(villageSelectRecords.value); // โหลดตามค่าหมู่บ้านปัจจุบันใน dropdown
          } else if (tabId === 'status') {
            loadFullAttendanceStatus();
          } else if (tabId === 'statistics') {
            loadStatistics();
            google.charts.setOnLoadCallback(drawCharts); // โหลด Google Charts และวาดกราฟ
          } else if (tabId === 'checkin') {
             loadAorSorMoListForCheckin(villageSelectCheckin.value); // โหลดรายชื่อ อสม. สำหรับหน้าเช็คชื่อ
          } else if (tabId === 'manage-aorsormor') {
             loadAorSorMoManagementList(); // โหลดรายชื่อสำหรับหน้าจัดการ อสม.
          }
        });
      });

      // ฟังก์ชันสำหรับแสดงข้อความแจ้งเตือน (สำเร็จ/ข้อผิดพลาด)
      function showMessage(element, msg, type = 'success') {
        element.textContent = msg;
        element.classList.remove('success', 'error'); // ลบ class เก่า
        element.classList.add(type); // เพิ่ม class ตามประเภทข้อความ
        element.style.display = 'block';
        setTimeout(() => {
          element.style.display = 'none'; // ซ่อนข้อความหลังจาก 3 วินาที
        }, 3000);
      }

      // โหลดรายชื่อ อสม. สำหรับหน้าเช็คชื่อ ('checkin' tab) ตามหมู่บ้านที่เลือก
      function loadAorSorMoListForCheckin(villageFilter) {
        aorSorMoListDiv.innerHTML = '<p>กำลังโหลดรายชื่อ อสม. ...</p>';
        google.script.run.withSuccessHandler(function(list) {
          aorSorMoListDiv.innerHTML = '';
          if (list.length === 0) {
            aorSorMoListDiv.innerHTML = '<p>ไม่พบรายชื่อ อสม. ในหมู่บ้านนี้ หรือยังไม่มีรายชื่อ อสม. โปรดเพิ่มรายชื่อในแท็บ "จัดการ อสม."</p>';
            return;
          }
          list.forEach(aorSorMor => {
            const itemDiv = document.createElement('div');
            itemDiv.classList.add('aor-sor-mor-item');
            itemDiv.innerHTML = `
              <span class="aor-sor-mor-info">${aorSorMor.id}. ${aorSorMor.name} (หมู่ ${aorSorMor.village})</span>
              <div class="attendance-status">
                <label><input type="radio" name="status_${aorSorMor.id}" value="มา" checked> มา</label>
                <label><input type="radio" name="status_${aorSorMor.id}" value="ไม่มา"> ไม่มา</label>
                <label><input type="radio" name="status_${aorSorMor.id}" value="ลา"> ลา</label>
                <label><input type="radio" name="status_${aorSorMor.id}" value="ไม่เข้าร่วม"> ไม่เข้าร่วม</label>
              </div>
            `;
            aorSorMoListDiv.appendChild(itemDiv);
          });
        }).getAorSorMorListByVillage(villageFilter); // เรียกใช้ฟังก์ชันใหม่ที่กรองตามหมู่บ้าน
      }

      // Event listener เมื่อมีการเลือกหมู่บ้านในแท็บเช็คชื่อ
      villageSelectCheckin.addEventListener('change', function() {
        loadAorSorMoListForCheckin(this.value);
      });

      // จัดการการส่งฟอร์มเช็คชื่อ (เมื่อกดปุ่ม "บันทึก")
      attendanceForm.addEventListener('submit', function(e) {
        e.preventDefault();

        const date = document.getElementById('date').value;
        const village = villageSelectCheckin.value;
        const mainActivity = document.getElementById('mainActivity').value;
        const subActivity = document.getElementById('subActivity').value;

        if (!date || !village || !mainActivity) {
          showMessage(saveMessage, 'กรุณากรอกข้อมูลให้ครบถ้วน: วันที่, หมู่บ้าน, และกิจกรรมหลัก', 'error');
          return;
        }

        const attendance = [];
        const aorSorMorItems = aorSorMoListDiv.querySelectorAll('.aor-sor-mor-item');
        aorSorMorItems.forEach(item => {
          const infoSpan = item.querySelector('.aor-sor-mor-info');
          // ดึง ID และชื่อจากข้อความที่แสดง
          const idMatch = infoSpan.textContent.match(/^(\d+)\./);
          const id = idMatch ? idMatch[1] : '';
          const nameMatch = infoSpan.textContent.match(/\. (.*) \(หมู่/);
          const name = nameMatch ? nameMatch[1].trim() : '';
          const status = item.querySelector(`input[name="status_${id}"]:checked`).value;
          attendance.push({ id, name, status });
        });

        const data = {
          date: date,
          village: village,
          mainActivity: mainActivity,
          subActivity: subActivity,
          attendance: attendance
        };

        // เรียกใช้ฟังก์ชัน saveAttendance ใน Code.gs
        google.script.run.withSuccessHandler(function(response) {
          showMessage(saveMessage, response.message, response.success ? 'success' : 'error');
          // ไม่ต้องโหลดรายชื่อใหม่ทั้งหมด แต่ควรล้างค่ากิจกรรมย่อยและรีเซ็ต radio button หากต้องการ
          // document.getElementById('subActivity').value = '';
          // loadAorSorMoListForCheckin(villageSelectCheckin.value); // อาจทำให้ข้อมูลที่เลือกหายไปถ้าไม่ระมัดระวัง
        }).saveAttendance(data);
      });

      // โหลดรายละเอียดการเช็คชื่อสำหรับแท็บ "รายละเอียดการเช็คชื่อ" และกรองตามหมู่บ้าน
      function loadAttendanceRecords(villageFilter) {
        attendanceRecordsTableBody.innerHTML = '<tr><td colspan="8" style="text-align:center;">กำลังโหลดข้อมูล...</td></tr>';
        google.script.run.withSuccessHandler(function(records) {
          attendanceRecordsTableBody.innerHTML = '';
          if (records.length === 0) {
            attendanceRecordsTableBody.innerHTML = '<tr><td colspan="8" style="text-align:center;">ยังไม่มีการบันทึกการเช็คชื่อ</td></tr>';
            return;
          }

          // กรองข้อมูลตามหมู่บ้านที่เลือกในหน้า Records
          const filteredRecords = villageFilter ? records.filter(record => record.village === villageFilter) : records;

          if (filteredRecords.length === 0) {
            attendanceRecordsTableBody.innerHTML = '<tr><td colspan="8" style="text-align:center;">ไม่พบข้อมูลการเช็คชื่อในหมู่บ้านนี้</td></tr>';
            return;
          }

          filteredRecords.forEach(record => {
            const row = attendanceRecordsTableBody.insertRow();
            row.insertCell().textContent = record.date;
            row.insertCell().textContent = record.village;
            row.insertCell().textContent = record.mainActivity;
            row.insertCell().textContent = record.subActivity;
            row.insertCell().textContent = record.aorSorMorId;
            row.insertCell().textContent = record.aorSorMorName;
            row.insertCell().textContent = record.status;
            
            const detailCell = row.insertCell();
            const detailButton = document.createElement('button');
            detailButton.textContent = 'ดู';
            detailButton.classList.add('btn');
            detailButton.style.padding = '5px 10px';
            detailButton.style.marginTop = '0';
            detailButton.style.fontSize = '0.9em';
            detailButton.style.backgroundColor = '#17a2b8'; /* สีฟ้า */
            detailButton.addEventListener('click', () => showAorSorMorDetail(record.aorSorMorId, record.aorSorMorName));
            detailCell.appendChild(detailButton);
          });
        }).getAttendanceRecords();
      }

      // Event listener เมื่อมีการเลือกหมู่บ้านในแท็บรายละเอียดการเช็คชื่อ
      villageSelectRecords.addEventListener('change', function() {
        loadAttendanceRecords(this.value);
      });

      // ฟังก์ชันสำหรับแสดงรายละเอียดกิจกรรมของ อสม. แต่ละคน
      function showAorSorMorDetail(aorSorMorId, aorSorMorName) {
        detailAorSorMorNameSpan.textContent = aorSorMorName;
        aorSorMorDetailTableBody.innerHTML = '<tr><td colspan="4" style="text-align:center;">กำลังโหลดข้อมูล...</td></tr>';
        
        google.script.run.withSuccessHandler(function(records) {
          aorSorMorDetailTableBody.innerHTML = '';
          if (records.length === 0) {
            aorSorMorDetailTableBody.innerHTML = '<tr><td colspan="4" style="text-align:center;">ไม่พบข้อมูลกิจกรรมของ อสม. ท่านนี้</td></tr>';
            return;
          }
          records.forEach(record => {
            const row = aorSorMorDetailTableBody.insertRow();
            row.insertCell().textContent = record.date;
            row.insertCell().textContent = record.mainActivity;
            row.insertCell().textContent = record.subActivity;
            row.insertCell().textContent = record.status;
          });
          aorSorMorDetailModal.style.display = 'block'; // แสดง Modal
        }).getAttendanceRecordsByAorSorMor(aorSorMorId);
      }

      // โหลดสถานะการบันทึกทั้งหมดสำหรับแท็บ "สถานะการบันทึกทั้งหมด"
      function loadFullAttendanceStatus() {
          fullAttendanceStatusTableBody.innerHTML = '<tr><td colspan="9" style="text-align:center;">กำลังโหลดข้อมูล...</td></tr>';
          google.script.run.withSuccessHandler(function(records) {
              fullAttendanceStatusTableBody.innerHTML = '';
              if (records.length === 0) {
                  fullAttendanceStatusTableBody.innerHTML = '<tr><td colspan="9" style="text-align:center;">ยังไม่มีการบันทึกการเช็คชื่อ</td></tr>';
                  return;
              }

              // จัดกลุ่มข้อมูลตาม วันที่, หมู่บ้าน, กิจกรรมหลัก, กิจกรรมย่อย
              const groupedRecords = records.reduce((acc, record) => {
                  const key = `${record.date}|${record.village}|${record.mainActivity}|${record.subActivity}`;
                  if (!acc[key]) {
                      acc[key] = {
                          date: record.date,
                          village: record.village,
                          mainActivity: record.mainActivity,
                          subActivity: record.subActivity,
                          'มา': 0,
                          'ไม่มา': 0,
                          'ลา': 0,
                          'ไม่เข้าร่วม': 0,
                          total: 0
                      };
                  }
                  acc[key][record.status]++;
                  acc[key].total++;
                  return acc;
              }, {});

              // แสดงข้อมูลที่จัดกลุ่มแล้วในตาราง
              for (const key in groupedRecords) {
                  const data = groupedRecords[key];
                  const row = fullAttendanceStatusTableBody.insertRow();
                  row.insertCell().textContent = data.date;
                  row.insertCell().textContent = data.village;
                  row.insertCell().textContent = data.mainActivity;
                  row.insertCell().textContent = data.subActivity;
                  row.insertCell().textContent = data['มา'];
                  row.insertCell().textContent = data['ไม่มา'];
                  row.insertCell().textContent = data['ลา'];
                  row.insertCell().textContent = data['ไม่เข้าร่วม'];
                  row.insertCell().textContent = data.total;
              }
          }).getAttendanceRecords();
      }

      // โหลดสถิติสำหรับแท็บ "สถิติ"
      function loadStatistics() {
        google.script.run.withSuccessHandler(function(aorSorMorList) {
          totalAorSorMorSpan.textContent = aorSorMorList.length; // จำนวน อสม. ทั้งหมด
        }).getAorSorMorList();

        google.script.run.withSuccessHandler(function(records) {
          // นับจำนวนกิจกรรมที่ไม่ซ้ำกัน (เพื่อแสดงจำนวนการบันทึกทั้งหมด)
          const uniqueEvents = new Set();
          records.forEach(record => {
              const eventKey = `${record.date}-${record.village}-${record.mainActivity}-${record.subActivity}`;
              uniqueEvents.add(eventKey);
          });
          totalAttendanceRecordsSpan.textContent = uniqueEvents.size;
        }).getAttendanceRecords();
      }

      // ฟังก์ชันสำหรับวาดกราฟ (ใช้ Google Charts)
      google.charts.load('current', {'packages':['corechart']});
      function drawCharts() {
        google.script.run.withSuccessHandler(function(records) {
          if (records.length === 0) {
            document.getElementById('chart_div').innerHTML = '<p style="text-align:center;">ยังไม่มีข้อมูลสำหรับแสดงกราฟ</p>';
            return;
          }

          // ข้อมูลสำหรับกราฟวงกลมแสดงสถานะการเช็คชื่อโดยรวม
          const statusCounts = {'มา': 0, 'ไม่มา': 0, 'ลา': 0, 'ไม่เข้าร่วม': 0};
          records.forEach(record => {
            if (statusCounts.hasOwnProperty(record.status)) {
              statusCounts[record.status]++;
            }
          });

          const pieData = [['สถานะ', 'จำนวน']];
          for (const status in statusCounts) {
            if (statusCounts[status] > 0) { // แสดงเฉพาะสถานะที่มีข้อมูล
              pieData.push([status, statusCounts[status]]);
            }
          }

          const pieChartData = google.visualization.arrayToDataTable(pieData);
          const pieOptions = {
            title: 'สถิติสถานะการเช็คชื่อโดยรวม',
            is3D: true, // กราฟ 3 มิติ
            colors: ['#2e8b57', '#dc3545', '#ffc107', '#6c757d'], // สีเขียว, แดง, เหลือง, เทา
            legend: { position: 'bottom' }
          };
          const pieChart = new google.visualization.PieChart(document.getElementById('chart_div'));
          pieChart.draw(pieChartData, pieOptions);

        }).getAttendanceRecords();
      }

      // จัดการการส่งฟอร์มเพิ่ม อสม.
      addAorSorMorForm.addEventListener('submit', function(e) {
        e.preventDefault();

        const id = document.getElementById('aorsormorId').value;
        const name = document.getElementById('aorsormorName').value;
        const village = document.getElementById('aorsormorVillage').value;

        if (!id || !name || !village) {
          showMessage(addAorSorMoMessage, 'กรุณากรอกข้อมูล อสม. ให้ครบถ้วน', 'error');
          return;
        }

        const data = { id, name, village };
        google.script.run.withSuccessHandler(function(response) {
          showMessage(addAorSorMoMessage, response.message, response.success ? 'success' : 'error');
          if (response.success) {
            addAorSorMorForm.reset(); // ล้างฟอร์ม
            loadAorSorMoListForCheckin(villageSelectCheckin.value); // อัปเดตรายชื่อในแท็บเช็คชื่อ
            loadAorSorMoManagementList(); // อัปเดตรายชื่อในแท็บจัดการ
          }
        }).addAorSorMor(data);
      });

      // โหลดรายชื่อ อสม. สำหรับหน้าจัดการ (เพิ่ม/แก้ไข/ลบ)
      function loadAorSorMoManagementList() {
        aorsormorManagementListDiv.innerHTML = '<p>กำลังโหลดรายชื่อ อสม. ...</p>';
        google.script.run.withSuccessHandler(function(list) {
          aorsormorManagementListDiv.innerHTML = '';
          if (list.length === 0) {
            aorsormorManagementListDiv.innerHTML = '<p>ยังไม่มีรายชื่อ อสม.</p>';
            return;
          }
          list.forEach(aorSorMor => {
            const itemDiv = document.createElement('div');
            itemDiv.classList.add('aorsormor-management-item');
            itemDiv.innerHTML = `
              <span class="aor-sor-mor-info">${aorSorMor.id}. ${aorSorMor.name} (หมู่ ${aorSorMor.village})</span>
              <div class="aorsormor-management-actions">
                <button class="edit-btn" data-id="${aorSorMor.id}" data-name="${aorSorMor.name}" data-village="${aorSorMor.village}" data-rowindex="${aorSorMor.rowIndex}"><i class="material-icons">edit</i> แก้ไข</button>
                <button class="delete-btn" data-rowindex="${aorSorMor.rowIndex}"><i class="material-icons">delete</i> ลบ</button>
              </div>
            `;
            aorsormorManagementListDiv.appendChild(itemDiv);
          });

          // ผูก Event Listener สำหรับปุ่มแก้ไขและลบ
          aorsormorManagementListDiv.querySelectorAll('.edit-btn').forEach(button => {
            button.addEventListener('click', function() {
              // ดึงข้อมูลจาก data-attributes ไปใส่ใน Modal
              document.getElementById('editAorSorMorOriginalId').value = this.dataset.id;
              document.getElementById('editAorSorMorId').value = this.dataset.id;
              document.getElementById('editAorSorMorName').value = this.dataset.name;
              document.getElementById('editAorSorMorVillage').value = this.dataset.village;
              editAorSorMorModal.style.display = 'block'; // แสดง Modal
            });
          });

          aorsormorManagementListDiv.querySelectorAll('.delete-btn').forEach(button => {
            button.addEventListener('click', function() {
              if (confirm('คุณแน่ใจหรือไม่ว่าต้องการลบ อสม. นี้?')) {
                const rowIndexToDelete = parseInt(this.dataset.rowindex);
                google.script.run.withSuccessHandler(function(response) {
                  showMessage(addAorSorMoMessage, response.message, response.success ? 'success' : 'error');
                  if (response.success) {
                    loadAorSorMoManagementList(); // อัปเดตรายชื่อในแท็บจัดการ
                    loadAorSorMoListForCheckin(villageSelectCheckin.value); // อัปเดตรายชื่อในแท็บเช็คชื่อ
                  }
                }).deleteAorSorMor(rowIndexToDelete);
              }
            });
          });

        }).getAorSorMorList();
      }

      // ปิด Modal แก้ไข เมื่อคลิกปุ่มปิด
      closeEditModalButton.addEventListener('click', function() {
        editAorSorMorModal.style.display = 'none';
      });
      // ปิด Modal แก้ไข เมื่อคลิกนอก Modal
      window.addEventListener('click', function(event) {
        if (event.target == editAorSorMorModal) {
          editAorSorMorModal.style.display = 'none';
        }
      });

      // ปิด Modal รายละเอียดกิจกรรม เมื่อคลิกปุ่มปิด
      closeDetailModalButton.addEventListener('click', function() {
        aorSorMorDetailModal.style.display = 'none';
      });
      // ปิด Modal รายละเอียดกิจกรรม เมื่อคลิกนอก Modal
      window.addEventListener('click', function(event) {
        if (event.target == aorSorMorDetailModal) {
          aorSorMorDetailModal.style.display = 'none';
        }
      });

      // จัดการการส่งฟอร์มแก้ไข อสม.
      editAorSorMorForm.addEventListener('submit', function(e) {
        e.preventDefault();
        const originalId = document.getElementById('editAorSorMorOriginalId').value;
        const id = document.getElementById('editAorSorMorId').value;
        const name = document.getElementById('editAorSorMorName').value;
        const village = document.getElementById('editAorSorMorVillage').value;
        
        const data = { originalId, id, name, village };
        google.script.run.withSuccessHandler(function(response) {
          showMessage(editAorSorMoMessage, response.message, response.success ? 'success' : 'error');
          if (response.success) {
            editAorSorMorModal.style.display = 'none'; // ซ่อน Modal
            loadAorSorMoManagementList(); // อัปเดตรายชื่อในแท็บจัดการ
            loadAorSorMoListForCheckin(villageSelectCheckin.value); // อัปเดตรายชื่อในแท็บเช็คชื่อ
          }
        }).editAorSorMor(data);
      });

      // จัดการการส่งออกข้อมูลเป็น Excel (CSV)
      exportExcelBtn.addEventListener('click', function() {
        google.script.run.withSuccessHandler(function(csvString) {
          if (csvString) {
            const blob = new Blob([csvString], { type: 'text/csv;charset=utf-8;' });
            const link = document.createElement('a');
            const url = URL.createObjectURL(blob);
            link.setAttribute('href', url);
            link.setAttribute('download', 'attendance_records.csv'); // ชื่อไฟล์
            link.style.visibility = 'hidden'; // ซ่อนลิงก์
            document.body.appendChild(link);
            link.click(); // คลิกเพื่อดาวน์โหลด
            document.body.removeChild(link);
            showMessage(saveMessage, 'ส่งออกข้อมูลเรียบร้อย', 'success');
          } else {
            showMessage(saveMessage, 'ไม่มีข้อมูลให้ส่งออก', 'error');
          }
        }).exportAttendanceToCsv();
      });

      // โหลดรายชื่อ อสม. ครั้งแรกเมื่อหน้าเว็บโหลดเสร็จสมบูรณ์
      // ไม่ต้องเรียก loadAorSorMoListForCheckin ตรงๆ แต่ให้รอการเลือกหมู่บ้านในแท็บเช็คชื่อ
      // หรือหากต้องการให้โหลดทั้งหมดเมื่อไม่มีการเลือกหมู่บ้านในตอนเริ่มต้น
      // loadAorSorMoListForCheckin(""); // โหลด อสม. ทั้งหมดในตอนแรก
    });
  </script>
</body>
</html>
