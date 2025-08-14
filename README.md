<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ระบบจัดการนักเรียน</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Sarabun:wght@300;400;500;600;700&display=swap');
        body { font-family: 'Sarabun', sans-serif; }
        .fade-in { animation: fadeIn 0.5s ease-in; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(20px); } to { opacity: 1; transform: translateY(0); } }
    </style>
</head>
<body class="bg-gradient-to-br from-blue-50 to-indigo-100 min-h-screen">
    <!-- หน้าเลือกบทบาท -->
    <div id="roleSelection" class="min-h-screen flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-md fade-in">
            <div class="text-center mb-8">
                <div class="bg-blue-100 w-20 h-20 rounded-full flex items-center justify-center mx-auto mb-4">
                    <span class="text-3xl font-bold text-blue-600">S</span>
                </div>
                <h1 class="text-2xl font-bold text-gray-800 mb-2">รายวิชาวิทยาศาสตร์ ว23101</h1>
                <p class="text-gray-600">เลือกบทบาทของคุณ</p>
            </div>
            
            <div class="space-y-4">
                <button onclick="showStudentPage()" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-4 px-6 rounded-xl transition-colors duration-200 flex items-center justify-center space-x-3">
                    <span class="text-xl font-bold">S</span>
                    <span>นักเรียน</span>
                </button>
                
                <button onclick="showTeacherLogin()" class="w-full bg-green-500 hover:bg-green-600 text-white font-medium py-4 px-6 rounded-xl transition-colors duration-200 flex items-center justify-center space-x-3">
                    <span class="text-xl font-bold">T</span>
                    <span>คุณครู</span>
                </button>
            </div>
        </div>
    </div>

    <!-- หน้าล็อกอินครู -->
    <div id="teacherLogin" class="min-h-screen flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl shadow-xl p-8 w-full max-w-md fade-in">
            <div class="text-center mb-8">
                <div class="bg-green-100 w-20 h-20 rounded-full flex items-center justify-center mx-auto mb-4">
                    <span class="text-3xl font-bold text-green-600">T</span>
                </div>
                <h2 class="text-2xl font-bold text-gray-800 mb-2">รายวิชาวิทยาศาสตร์ ว23101</h2>
                <p class="text-gray-600">กรุณาใส่รหัสผ่าน</p>
            </div>
            
            <form onsubmit="teacherLogin(event)" class="space-y-6">
                <div>
                    <input type="password" id="teacherPassword" placeholder="รหัสผ่าน" class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                </div>
                
                <button type="submit" class="w-full bg-green-500 hover:bg-green-600 text-white font-medium py-3 px-6 rounded-xl transition-colors duration-200">
                    เข้าสู่ระบบ
                </button>
                
                <button type="button" onclick="showRoleSelection()" class="w-full text-gray-500 hover:text-gray-700 font-medium py-2 transition-colors duration-200">
                    ← กลับ
                </button>
            </form>
        </div>
    </div>

    <!-- หน้านักเรียน -->
    <div id="studentPage" class="min-h-screen hidden">
        <!-- Header -->
        <header class="bg-white shadow-sm border-b">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-4">
                    <div class="flex items-center space-x-3">
                        <span class="text-2xl font-bold text-blue-600">S</span>
                        <h1 class="text-xl font-bold text-gray-800">รายวิชาวิทยาศาสตร์ ว23101</h1>
                    </div>
                    <button onclick="showRoleSelection()" class="text-gray-500 hover:text-gray-700 px-3 py-2 rounded-lg transition-colors">
                        ออกจากระบบ
                    </button>
                </div>
            </div>
        </header>

        <!-- Navigation -->
        <nav class="bg-blue-500 text-white">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex space-x-8 overflow-x-auto">
                    <button onclick="showStudentSection('attendance')" class="student-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors active">
                        เช็คชื่อ
                    </button>
                    <button onclick="showStudentSection('checkwork')" class="student-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        ตรวจสอบงาน
                    </button>
                    <button onclick="showStudentSection('submit')" class="student-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        ส่งงาน
                    </button>
                    <button onclick="showStudentSection('news')" class="student-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        กระดานข่าว
                    </button>
                </div>
            </div>
        </nav>

        <!-- Content -->
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <!-- เช็คชื่อ -->
            <div id="attendance" class="student-section">
                <div class="bg-white rounded-2xl shadow-lg p-6 max-w-2xl mx-auto">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6 text-center">เช็คชื่อเข้าเรียน</h2>
                    
                    <form onsubmit="submitAttendance(event)" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อจริง</label>
                                <input type="text" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อเล่น</label>
                                <input type="text" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">เลขที่</label>
                                <input type="number" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชั้นเรียน</label>
                                <select required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                                    <option value="">เลือกชั้นเรียน</option>
                                    <option value="ม.3/1">ม.3/1</option>
                                    <option value="ม.3/2">ม.3/2</option>
                                </select>
                            </div>
                        </div>
                        
                        <button type="submit" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-3 px-6 rounded-xl transition-colors duration-200">
                            เช็คชื่อ
                        </button>
                    </form>
                </div>
            </div>

            <!-- ตรวจสอบงาน -->
            <div id="checkwork" class="student-section hidden">
                <div class="bg-white rounded-2xl shadow-lg p-6 max-w-2xl mx-auto">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6 text-center">ตรวจสอบงาน</h2>
                    
                    <div class="mb-6">
                        <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อของคุณ</label>
                        <input type="text" id="checkWorkName" placeholder="กรอกชื่อเพื่อตรวจสอบงาน" class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                        <button onclick="checkWork()" class="mt-3 bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-6 rounded-xl transition-colors duration-200">
                            ตรวจสอบ
                        </button>
                    </div>
                    
                    <div id="workStatus" class="space-y-6">
                        <!-- ตารางรวมงานทั้งหมด -->
                        <div class="bg-gray-50 rounded-xl p-6">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">ตารางรวมงานทั้งหมด</h3>
                            
                            <!-- ห้อง ม.3/1 -->
                            <div class="mb-6">
                                <h4 class="text-md font-semibold text-blue-600 mb-3 flex items-center">
                                    <span class="bg-blue-100 px-3 py-1 rounded-full text-sm mr-2">ม.3/1</span>
                                    ห้องหนึ่ง
                                </h4>
                                
                                <div class="overflow-x-auto">
                                    <table class="w-full bg-white rounded-lg shadow-sm">
                                        <thead class="bg-blue-50">
                                            <tr>
                                                <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">เลขที่</th>
                                                <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">ชื่อ-นามสกุล</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 1</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 2</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 3</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 4</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 5</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 6</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 7</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 8</th>
                                            </tr>
                                        </thead>
                                        <tbody class="divide-y divide-gray-200">
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">1</td>
                                                <td class="px-4 py-3 text-sm font-medium">นางสาว กมลชนก ใจดี</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">2</td>
                                                <td class="px-4 py-3 text-sm font-medium">นาย จิรายุ รักเรียน</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">3</td>
                                                <td class="px-4 py-3 text-sm font-medium">นางสาว ชนิดา ขยันเรียน</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">4</td>
                                                <td class="px-4 py-3 text-sm font-medium">นาย ธนากร สมบูรณ์</td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">5</td>
                                                <td class="px-4 py-3 text-sm font-medium">นางสาว นิภาพร เก่งมาก</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                            
                            <!-- ห้อง ม.3/2 -->
                            <div>
                                <h4 class="text-md font-semibold text-green-600 mb-3 flex items-center">
                                    <span class="bg-green-100 px-3 py-1 rounded-full text-sm mr-2">ม.3/2</span>
                                    ห้องสอง
                                </h4>
                                
                                <div class="overflow-x-auto">
                                    <table class="w-full bg-white rounded-lg shadow-sm">
                                        <thead class="bg-green-50">
                                            <tr>
                                                <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">เลขที่</th>
                                                <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">ชื่อ-นามสกุล</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 1</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 2</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 3</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 4</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 5</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 6</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 7</th>
                                                <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ 8</th>
                                            </tr>
                                        </thead>
                                        <tbody class="divide-y divide-gray-200">
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">1</td>
                                                <td class="px-4 py-3 text-sm font-medium">นาย กิตติพงษ์ มานะดี</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">2</td>
                                                <td class="px-4 py-3 text-sm font-medium">นางสาว จันทิมา สวยงาม</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">3</td>
                                                <td class="px-4 py-3 text-sm font-medium">นาย ชัยวัฒน์ เรียนดี</td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">4</td>
                                                <td class="px-4 py-3 text-sm font-medium">นางสาว ณัฐชา ฉลาดมาก</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                            <tr class="hover:bg-gray-50">
                                                <td class="px-4 py-3 text-sm">5</td>
                                                <td class="px-4 py-3 text-sm font-medium">นาย ปิยะ ใฝ่เรียน</td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-red-600 font-bold">ไม่ส่ง</span></td>
                                                <td class="px-4 py-3 text-center"><span class="text-green-600 font-bold">ส่ง</span></td>
                                            </tr>
                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- ส่งงาน -->
            <div id="submit" class="student-section hidden">
                <div class="bg-white rounded-2xl shadow-lg p-6 max-w-2xl mx-auto">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6 text-center">ส่งงาน</h2>
                    
                    <form onsubmit="submitWork(event)" class="space-y-6">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อนักเรียน</label>
                            <input type="text" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">เลือกงาน</label>
                            <select required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-transparent outline-none">
                                <option value="">เลือกงานที่ต้องการส่ง</option>
                                <option value="งานที่ 1">งานที่ 1: เรียงความ</option>
                                <option value="งานที่ 2">งานที่ 2: แบบฝึกหัด</option>
                                <option value="งานที่ 3">งานที่ 3: โครงงาน</option>
                            </select>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">อัปโหลดไฟล์งาน</label>
                            <div class="border-2 border-dashed border-gray-300 rounded-xl p-6 text-center hover:border-blue-400 transition-colors" id="fileDropZone">
                                <input type="file" class="hidden" id="workFile" accept=".pdf,.doc,.docx,.jpg,.png" onchange="handleWorkFileSelect(event)">
                                <label for="workFile" class="cursor-pointer">
                                    <div class="text-4xl mb-2">📁</div>
                                    <p class="text-gray-600">คลิกเพื่อเลือกไฟล์</p>
                                    <p class="text-sm text-gray-500 mt-1">รองรับ PDF, Word, รูปภาพ</p>
                                </label>
                                <div id="selectedFileName" class="mt-3 text-sm text-green-600 hidden"></div>
                            </div>
                        </div>
                        
                        <button type="submit" class="w-full bg-blue-500 hover:bg-blue-600 text-white font-medium py-3 px-6 rounded-xl transition-colors duration-200">
                            ส่งงาน
                        </button>
                    </form>
                </div>
            </div>

            <!-- กระดานข่าว -->
            <div id="news" class="student-section hidden">
                <div class="space-y-6">
                    <h2 class="text-2xl font-bold text-gray-800 text-center">กระดานข่าว</h2>
                    
                    <!-- ตัวอย่างข่าว -->
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-start space-x-4">
                            <div class="bg-blue-100 w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0">
                                <span class="text-xl font-bold text-blue-600">N</span>
                            </div>
                            <div class="flex-1">
                                <h3 class="font-bold text-lg text-gray-800 mb-2">ประกาศสำคัญ</h3>
                                <p class="text-gray-600 mb-3">การสอบกลางภาคจะจัดขึ้นในวันที่ 15-20 มีนาคม 2024 นักเรียนทุกคนต้องเตรียมตัวให้พร้อม</p>
                                <div class="text-sm text-gray-500">วันที่ 1 มีนาคม 2024</div>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-start space-x-4">
                            <div class="bg-green-100 w-12 h-12 rounded-full flex items-center justify-center flex-shrink-0">
                                <span class="text-xl font-bold text-green-600">E</span>
                            </div>
                            <div class="flex-1">
                                <h3 class="font-bold text-lg text-gray-800 mb-2">กิจกรรมวันกีฬา</h3>
                                <p class="text-gray-600 mb-3">ขอเชิญนักเรียนทุกคนร่วมกิจกรรมวันกีฬาประจำปี วันที่ 25 มีนาคม 2024</p>
                                <div class="bg-gray-100 rounded-lg p-3 mb-3">
                                    <img src="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='200' viewBox='0 0 300 200'%3E%3Crect width='300' height='200' fill='%23f0f9ff'/%3E%3Ctext x='150' y='100' text-anchor='middle' dy='.3em' font-family='Arial' font-size='16' fill='%236b7280'%3Eรูปกิจกรรมกีฬา%3C/text%3E%3C/svg%3E" alt="กิจกรรมกีฬา" class="w-full rounded-lg">
                                </div>
                                <div class="text-sm text-gray-500">วันที่ 28 กุมภาพันธ์ 2024</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- หน้าคุณครู -->
    <div id="teacherPage" class="min-h-screen hidden">
        <!-- Header -->
        <header class="bg-white shadow-sm border-b">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex justify-between items-center py-4">
                    <div class="flex items-center space-x-3">
                        <span class="text-2xl font-bold text-green-600">T</span>
                        <h1 class="text-xl font-bold text-gray-800">รายวิชาวิทยาศาสตร์ ว23101</h1>
                    </div>
                    <div class="flex items-center space-x-4">
                        <button onclick="showPasswordChange()" class="text-gray-500 hover:text-gray-700 px-3 py-2 rounded-lg transition-colors">
                            เปลี่ยนรหัสผ่าน
                        </button>
                        <button onclick="showRoleSelection()" class="text-gray-500 hover:text-gray-700 px-3 py-2 rounded-lg transition-colors">
                            ออกจากระบบ
                        </button>
                    </div>
                </div>
            </div>
        </header>

        <!-- Navigation -->
        <nav class="bg-green-500 text-white">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <div class="flex space-x-8 overflow-x-auto">
                    <button onclick="showTeacherSection('dashboard')" class="teacher-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors active">
                        แดชบอร์ด
                    </button>
                    <button onclick="showTeacherSection('manage-students')" class="teacher-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        จัดการรายชื่อ
                    </button>
                    <button onclick="showTeacherSection('manage-work')" class="teacher-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        จัดการงาน
                    </button>
                    <button onclick="showTeacherSection('manage-news')" class="teacher-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        จัดการข่าว
                    </button>
                    <button onclick="showTeacherSection('reports')" class="teacher-nav-btn py-4 px-6 whitespace-nowrap border-b-2 border-transparent hover:border-white transition-colors">
                        รายงาน
                    </button>
                </div>
            </div>
        </nav>

        <!-- Content -->
        <main class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
            <!-- แดชบอร์ด -->
            <div id="dashboard" class="teacher-section">
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">นักเรียนเช็คชื่อวันนี้</p>
                                <p class="text-2xl font-bold text-blue-600">28</p>
                            </div>
                            <div class="bg-blue-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-blue-600">S</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">งานที่ส่งแล้ว</p>
                                <p class="text-2xl font-bold text-green-600">15</p>
                            </div>
                            <div class="bg-green-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-green-600">W</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">งานที่ยังไม่ส่ง</p>
                                <p class="text-2xl font-bold text-red-600">13</p>
                            </div>
                            <div class="bg-red-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-red-600">P</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">ข่าวประกาศ</p>
                                <p class="text-2xl font-bold text-purple-600">5</p>
                            </div>
                            <div class="bg-purple-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-purple-600">N</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-2xl shadow-lg p-6">
                    <h3 class="text-lg font-bold text-gray-800 mb-4">กิจกรรมล่าสุด</h3>
                    <div class="space-y-3">
                        <div class="flex items-center space-x-3 p-3 bg-gray-50 rounded-lg">
                            <span class="text-green-500 font-bold">ส่ง</span>
                            <span class="text-sm">นักเรียน "สมชาย" ส่งงานที่ 1 เรียบร้อยแล้ว</span>
                            <span class="text-xs text-gray-500 ml-auto">5 นาทีที่แล้ว</span>
                        </div>
                        <div class="flex items-center space-x-3 p-3 bg-gray-50 rounded-lg">
                            <span class="text-blue-500 font-bold">เช็ค</span>
                            <span class="text-sm">นักเรียน "สมหญิง" เช็คชื่อเข้าเรียน</span>
                            <span class="text-xs text-gray-500 ml-auto">10 นาทีที่แล้ว</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- จัดการรายชื่อนักเรียน -->
            <div id="manage-students" class="teacher-section hidden">
                <div class="space-y-6">
                    <!-- สรุปข้อมูลรวม -->
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
                        <div class="bg-white rounded-2xl shadow-lg p-6">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm font-medium text-gray-600">นักเรียนทั้งหมด</p>
                                    <p class="text-2xl font-bold text-blue-600" id="totalStudents">10</p>
                                </div>
                                <div class="bg-blue-100 w-12 h-12 rounded-full flex items-center justify-center">
                                    <span class="text-xl">👥</span>
                                </div>
                            </div>
                        </div>
                        
                        <div class="bg-white rounded-2xl shadow-lg p-6">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm font-medium text-gray-600">ห้อง ม.3/1</p>
                                    <p class="text-2xl font-bold text-green-600">5</p>
                                </div>
                                <div class="bg-green-100 w-12 h-12 rounded-full flex items-center justify-center">
                                    <span class="text-xl">🏫</span>
                                </div>
                            </div>
                        </div>
                        
                        <div class="bg-white rounded-2xl shadow-lg p-6">
                            <div class="flex items-center justify-between">
                                <div>
                                    <p class="text-sm font-medium text-gray-600">ห้อง ม.3/2</p>
                                    <p class="text-2xl font-bold text-purple-600">5</p>
                                </div>
                                <div class="bg-purple-100 w-12 h-12 rounded-full flex items-center justify-center">
                                    <span class="text-xl">🏫</span>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- ตารางรายชื่อนักเรียน -->
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex justify-between items-center mb-6">
                            <h3 class="text-lg font-bold text-gray-800">รายชื่อนักเรียนทั้งหมด</h3>
                            <div class="flex space-x-3">
                                <button onclick="exportToExcel()" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200 flex items-center space-x-2">
                                    <span>Excel</span>
                                </button>
                                <button onclick="exportToWord()" class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200 flex items-center space-x-2">
                                    <span>Word</span>
                                </button>
                            </div>
                        </div>

                        <!-- ตัวกรองข้อมูล -->
                        <div class="mb-6 flex flex-wrap gap-4">
                            <div class="flex-1 min-w-64">
                                <input type="text" id="searchStudent" placeholder="ค้นหาชื่อนักเรียน..." class="w-full px-4 py-2 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none" onkeyup="filterStudents()">
                            </div>
                            <div>
                                <select id="classFilter" class="px-4 py-2 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none" onchange="filterStudents()">
                                    <option value="">ทุกห้อง</option>
                                    <option value="ม.3/1">ม.3/1</option>
                                    <option value="ม.3/2">ม.3/2</option>
                                </select>
                            </div>
                        </div>

                        <!-- ตารางข้อมูล -->
                        <div class="overflow-x-auto">
                            <table class="w-full" id="studentsTable">
                                <thead class="bg-gray-50">
                                    <tr>
                                        <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">เลขที่</th>
                                        <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">ชื่อ-นามสกุล</th>
                                        <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">ชื่อเล่น</th>
                                        <th class="px-4 py-3 text-left text-sm font-medium text-gray-700">ชั้นเรียน</th>
                                        <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">การเช็คชื่อ</th>
                                        <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">งานที่ส่ง</th>
                                        <th class="px-4 py-3 text-center text-sm font-medium text-gray-700">สถานะ</th>
                                    </tr>
                                </thead>
                                <tbody class="divide-y divide-gray-200" id="studentsTableBody">
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">1</td>
                                        <td class="px-4 py-3 text-sm font-medium">นางสาว กมลชนก ใจดี</td>
                                        <td class="px-4 py-3 text-sm">กมล</td>
                                        <td class="px-4 py-3 text-sm">ม.3/1</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">15/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full text-xs">5/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ปกติ</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">2</td>
                                        <td class="px-4 py-3 text-sm font-medium">นาย จิรายุ รักเรียน</td>
                                        <td class="px-4 py-3 text-sm">จิ๋ม</td>
                                        <td class="px-4 py-3 text-sm">ม.3/1</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">12/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">6/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">เฝ้าระวัง</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">3</td>
                                        <td class="px-4 py-3 text-sm font-medium">นางสาว ชนิดา ขยันเรียน</td>
                                        <td class="px-4 py-3 text-sm">ดา</td>
                                        <td class="px-4 py-3 text-sm">ม.3/1</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">18/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">7/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ดีเยี่ยม</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">4</td>
                                        <td class="px-4 py-3 text-sm font-medium">นาย ธนากร สมบูรณ์</td>
                                        <td class="px-4 py-3 text-sm">กร</td>
                                        <td class="px-4 py-3 text-sm">ม.3/1</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-red-100 text-red-800 px-2 py-1 rounded-full text-xs">8/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-red-100 text-red-800 px-2 py-1 rounded-full text-xs">3/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-red-100 text-red-800 px-2 py-1 rounded-full text-xs">ต้องปรับปรุง</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">5</td>
                                        <td class="px-4 py-3 text-sm font-medium">นางสาว นิภาพร เก่งมาก</td>
                                        <td class="px-4 py-3 text-sm">นิภา</td>
                                        <td class="px-4 py-3 text-sm">ม.3/1</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">20/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">8/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ดีเยี่ยม</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">1</td>
                                        <td class="px-4 py-3 text-sm font-medium">นาย กิตติพงษ์ มานะดี</td>
                                        <td class="px-4 py-3 text-sm">กิต</td>
                                        <td class="px-4 py-3 text-sm">ม.3/2</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">16/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full text-xs">6/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ปกติ</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">2</td>
                                        <td class="px-4 py-3 text-sm font-medium">นางสาว จันทิมา สวยงาม</td>
                                        <td class="px-4 py-3 text-sm">จัน</td>
                                        <td class="px-4 py-3 text-sm">ม.3/2</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">17/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">6/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ดี</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">3</td>
                                        <td class="px-4 py-3 text-sm font-medium">นาย ชัยวัฒน์ เรียนดี</td>
                                        <td class="px-4 py-3 text-sm">ชัย</td>
                                        <td class="px-4 py-3 text-sm">ม.3/2</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">13/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">5/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-xs">เฝ้าระวัง</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">4</td>
                                        <td class="px-4 py-3 text-sm font-medium">นางสาว ณัฐชา ฉลาดมาก</td>
                                        <td class="px-4 py-3 text-sm">ชา</td>
                                        <td class="px-4 py-3 text-sm">ม.3/2</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">19/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">7/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ดีเยี่ยม</span>
                                        </td>
                                    </tr>
                                    <tr class="hover:bg-gray-50">
                                        <td class="px-4 py-3 text-sm">5</td>
                                        <td class="px-4 py-3 text-sm font-medium">นาย ปิยะ ใฝ่เรียน</td>
                                        <td class="px-4 py-3 text-sm">ปิ๋ม</td>
                                        <td class="px-4 py-3 text-sm">ม.3/2</td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">14/20 วัน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-blue-100 text-blue-800 px-2 py-1 rounded-full text-xs">6/8 งาน</span>
                                        </td>
                                        <td class="px-4 py-3 text-center">
                                            <span class="bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs">ปกติ</span>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </div>

            <!-- จัดการงาน -->
            <div id="manage-work" class="teacher-section hidden">
                <!-- ส่วนอัปโหลดรายชื่อนักเรียน -->
                <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
                    <h3 class="text-lg font-bold text-gray-800 mb-4">📋 จัดการรายชื่อนักเรียน</h3>
                    
                    <!-- แท็บเลือกวิธีเพิ่มข้อมูล -->
                    <div class="border-b border-gray-200 mb-6">
                        <nav class="flex space-x-8">
                            <button onclick="showUploadMethod('manual')" class="upload-method-btn py-3 px-4 border-b-2 border-green-500 text-green-600 font-medium text-sm whitespace-nowrap active">
                                ➕ เพิ่มทีละคน
                            </button>
                            <button onclick="showUploadMethod('import')" class="upload-method-btn py-3 px-4 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                📁 นำเข้าจากไฟล์
                            </button>
                        </nav>
                    </div>

                    <!-- เพิ่มทีละคน -->
                    <div id="manualUpload" class="upload-method-content">
                        <form onsubmit="addSingleStudent(event)" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-4">
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">เลขที่</label>
                                <input type="number" name="studentNumber" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อจริง</label>
                                <input type="text" name="firstName" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">นามสกุล</label>
                                <input type="text" name="lastName" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อเล่น</label>
                                <input type="text" name="nickname" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">ชั้นเรียน</label>
                                <select name="classroom" required class="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                                    <option value="">เลือกชั้น</option>
                                    <option value="ม.3/1">ม.3/1</option>
                                    <option value="ม.3/2">ม.3/2</option>
                                </select>
                            </div>
                            
                            <div class="md:col-span-2 lg:col-span-5">
                                <button type="submit" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-6 rounded-lg transition-colors duration-200">
                                    ➕ เพิ่มนักเรียน
                                </button>
                            </div>
                        </form>
                    </div>

                    <!-- นำเข้าจากไฟล์ -->
                    <div id="importUpload" class="upload-method-content hidden">
                        <div class="space-y-6">
                            <!-- ดาวน์โหลดแม่แบบ -->
                            <div class="bg-blue-50 rounded-lg p-4">
                                <h4 class="font-medium text-blue-800 mb-3">📥 ดาวน์โหลดแม่แบบ</h4>
                                <p class="text-sm text-blue-700 mb-3">ดาวน์โหลดแม่แบบเพื่อกรอกข้อมูลนักเรียน</p>
                                <div class="flex space-x-3">
                                    <button onclick="downloadStudentTemplate('excel')" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-lg transition-colors duration-200 flex items-center space-x-2">
                                        <span>📊</span>
                                        <span>Excel</span>
                                    </button>
                                    <button onclick="downloadStudentTemplate('word')" class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-lg transition-colors duration-200 flex items-center space-x-2">
                                        <span>📄</span>
                                        <span>Word</span>
                                    </button>
                                </div>
                            </div>

                            <!-- อัปโหลดไฟล์ -->
                            <div>
                                <label class="block text-sm font-medium text-gray-700 mb-2">อัปโหลดไฟล์รายชื่อ</label>
                                <div class="border-2 border-dashed border-gray-300 rounded-lg p-6 text-center hover:border-green-400 transition-colors">
                                    <input type="file" class="hidden" id="studentListFile" accept=".xlsx,.xls,.docx,.csv" onchange="handleStudentFileImport(event)">
                                    <label for="studentListFile" class="cursor-pointer">
                                        <div class="text-4xl mb-3">📁</div>
                                        <p class="text-gray-600 font-medium">คลิกเพื่อเลือกไฟล์</p>
                                        <p class="text-sm text-gray-500 mt-1">รองรับ Excel (.xlsx, .xls), Word (.docx), CSV</p>
                                    </label>
                                    <div id="selectedStudentFileName" class="mt-3 text-sm text-green-600 hidden"></div>
                                </div>
                            </div>

                            <!-- ตัวอย่างข้อมูลที่นำเข้า -->
                            <div id="studentImportResult" class="hidden">
                                <h4 class="font-medium text-gray-800 mb-3">👀 ตัวอย่างข้อมูลที่จะนำเข้า</h4>
                                <div class="overflow-x-auto bg-gray-50 rounded-lg p-4">
                                    <table class="w-full text-sm">
                                        <thead>
                                            <tr class="border-b border-gray-300">
                                                <th class="px-3 py-2 text-left">เลขที่</th>
                                                <th class="px-3 py-2 text-left">ชื่อจริง</th>
                                                <th class="px-3 py-2 text-left">นามสกุล</th>
                                                <th class="px-3 py-2 text-left">ชื่อเล่น</th>
                                                <th class="px-3 py-2 text-left">ชั้นเรียน</th>
                                            </tr>
                                        </thead>
                                        <tbody id="studentPreviewTableBody">
                                            <!-- ข้อมูลจะถูกเพิ่มที่นี่ -->
                                        </tbody>
                                    </table>
                                </div>
                                
                                <div class="flex space-x-3 mt-4">
                                    <button onclick="confirmStudentImport()" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-6 rounded-lg transition-colors duration-200">
                                        ✅ ยืนยันการนำเข้า
                                    </button>
                                    <button onclick="cancelStudentImport()" class="bg-gray-300 hover:bg-gray-400 text-gray-700 font-medium py-2 px-6 rounded-lg transition-colors duration-200">
                                        ❌ ยกเลิก
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- สถิติรวม -->
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">นักเรียนเช็คชื่อวันนี้</p>
                                <p class="text-2xl font-bold text-blue-600">28</p>
                            </div>
                            <div class="bg-blue-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-blue-600">S</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">งานที่ส่งแล้ว</p>
                                <p class="text-2xl font-bold text-green-600">15</p>
                            </div>
                            <div class="bg-green-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-green-600">W</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">งานที่ยังไม่ส่ง</p>
                                <p class="text-2xl font-bold text-red-600">13</p>
                            </div>
                            <div class="bg-red-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-red-600">P</span>
                            </div>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <div class="flex items-center justify-between">
                            <div>
                                <p class="text-sm font-medium text-gray-600">ข่าวประกาศ</p>
                                <p class="text-2xl font-bold text-purple-600">5</p>
                            </div>
                            <div class="bg-purple-100 w-12 h-12 rounded-full flex items-center justify-center">
                                <span class="text-xl font-bold text-purple-600">N</span>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="bg-white rounded-2xl shadow-lg p-6">
                    <h3 class="text-lg font-bold text-gray-800 mb-4">กิจกรรมล่าสุด</h3>
                    <div class="space-y-3">
                        <div class="flex items-center space-x-3 p-3 bg-gray-50 rounded-lg">
                            <span class="text-green-500 font-bold">ส่ง</span>
                            <span class="text-sm">นักเรียน "สมชาย" ส่งงานที่ 1 เรียบร้อยแล้ว</span>
                            <span class="text-xs text-gray-500 ml-auto">5 นาทีที่แล้ว</span>
                        </div>
                        <div class="flex items-center space-x-3 p-3 bg-gray-50 rounded-lg">
                            <span class="text-blue-500 font-bold">เช็ค</span>
                            <span class="text-sm">นักเรียน "สมหญิng" เช็คชื่อเข้าเรียน</span>
                            <span class="text-xs text-gray-500 ml-auto">10 นาทีที่แล้ว</span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- จัดการงาน -->
            <div id="manage-work" class="teacher-section hidden">
                <!-- แท็บงาน -->
                <div class="bg-white rounded-2xl shadow-lg mb-6">
                    <div class="border-b border-gray-200">
                        <nav class="flex space-x-8 px-6" id="workTabs">
                            <button onclick="showWorkTab(1)" class="work-tab-btn py-4 px-2 border-b-2 border-green-500 text-green-600 font-medium text-sm whitespace-nowrap active">
                                งานที่ 1
                            </button>
                            <button onclick="showWorkTab(2)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 2
                            </button>
                            <button onclick="showWorkTab(3)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 3
                            </button>
                            <button onclick="showWorkTab(4)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 4
                            </button>
                            <button onclick="showWorkTab(5)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 5
                            </button>
                            <button onclick="showWorkTab(6)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 6
                            </button>
                            <button onclick="showWorkTab(7)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 7
                            </button>
                            <button onclick="showWorkTab(8)" class="work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap">
                                งานที่ 8
                            </button>
                            <button onclick="addNewWorkTab()" class="py-4 px-2 text-green-500 hover:text-green-700 font-medium text-sm whitespace-nowrap flex items-center space-x-1">
                                <span>+</span>
                                <span>เพิ่มแท็บ</span>
                            </button>
                        </nav>
                    </div>

                    <!-- เนื้อหาแท็บ -->
                    <div class="p-6">
                        <div id="workTab1" class="work-tab-content">
                            <div class="flex justify-between items-center mb-6">
                                <h3 class="text-lg font-bold text-gray-800">งานที่ 1: เรียงความ</h3>
                                <div class="flex space-x-3">
                                    <button onclick="editWorkDetails(1)" class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        แก้ไข
                                    </button>
                                    <button onclick="exportWorkExcel(1)" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        Excel
                                    </button>
                                    <button onclick="exportWorkWord(1)" class="bg-purple-500 hover:bg-purple-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        Word
                                    </button>
                                </div>
                            </div>
                            
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                                <div class="bg-gray-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">กำหนดส่ง</p>
                                    <p class="text-lg font-semibold text-gray-800">15 มีนาคม 2024</p>
                                </div>
                                <div class="bg-green-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">ส่งแล้ว</p>
                                    <p class="text-lg font-semibold text-green-600">15/28 คน</p>
                                </div>
                                <div class="bg-red-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">ยังไม่ส่ง</p>
                                    <p class="text-lg font-semibold text-red-600">13 คน</p>
                                </div>
                            </div>

                            <div class="bg-gray-50 rounded-xl p-4 mb-6">
                                <h4 class="font-medium text-gray-800 mb-2">รายละเอียดงาน</h4>
                                <p class="text-gray-600">เขียนเรียงความเรื่อง "ความสำคัญของการศึกษา" ความยาวไม่น้อยกว่า 300 คำ</p>
                            </div>

                            <!-- รายชื่อผู้ส่งงาน -->
                            <div class="space-y-4">
                                <h4 class="font-medium text-gray-800">รายชื่อผู้ส่งงาน</h4>
                                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                                    <div class="bg-green-50 border border-green-200 rounded-xl p-4">
                                        <h5 class="font-medium text-green-800 mb-3">ส่งแล้ว (15 คน)</h5>
                                        <div class="space-y-2 text-sm">
                                            <div class="flex justify-between">
                                                <span>กมลชนก ใจดี (ม.3/1)</span>
                                                <span class="text-green-600 font-bold">ส่ง</span>
                                            </div>
                                            <div class="flex justify-between">
                                                <span>จิรายุ รักเรียน (ม.3/1)</span>
                                                <span class="text-green-600 font-bold">ส่ง</span>
                                            </div>
                                            <div class="flex justify-between">
                                                <span>ชนิดา ขยันเรียน (ม.3/1)</span>
                                                <span class="text-green-600 font-bold">ส่ง</span>
                                            </div>
                                            <div class="text-gray-500">... และอีก 12 คน</div>
                                        </div>
                                    </div>
                                    
                                    <div class="bg-red-50 border border-red-200 rounded-xl p-4">
                                        <h5 class="font-medium text-red-800 mb-3">ยังไม่ส่ง (13 คน)</h5>
                                        <div class="space-y-2 text-sm">
                                            <div class="flex justify-between">
                                                <span>ธนากร สมบูรณ์ (ม.3/1)</span>
                                                <span class="text-red-600 font-bold">ไม่ส่ง</span>
                                            </div>
                                            <div class="flex justify-between">
                                                <span>กิตติพงษ์ มานะดี (ม.3/2)</span>
                                                <span class="text-red-600 font-bold">ไม่ส่ง</span>
                                            </div>
                                            <div class="flex justify-between">
                                                <span>ชัยวัฒน์ เรียนดี (ม.3/2)</span>
                                                <span class="text-red-600 font-bold">ไม่ส่ง</span>
                                            </div>
                                            <div class="text-gray-500">... และอีก 10 คน</div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div id="workTab2" class="work-tab-content hidden">
                            <div class="flex justify-between items-center mb-6">
                                <h3 class="text-lg font-bold text-gray-800">งานที่ 2: แบบฝึกหัด</h3>
                                <div class="flex space-x-3">
                                    <button onclick="editWorkDetails(2)" class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        แก้ไข
                                    </button>
                                    <button onclick="exportWorkExcel(2)" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        Excel
                                    </button>
                                    <button onclick="exportWorkWord(2)" class="bg-purple-500 hover:bg-purple-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                        Word
                                    </button>
                                </div>
                            </div>
                            
                            <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-6">
                                <div class="bg-gray-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">กำหนดส่ง</p>
                                    <p class="text-lg font-semibold text-gray-800">20 มีนาคม 2024</p>
                                </div>
                                <div class="bg-green-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">ส่งแล้ว</p>
                                    <p class="text-lg font-semibold text-green-600">8/28 คน</p>
                                </div>
                                <div class="bg-red-50 rounded-xl p-4">
                                    <p class="text-sm text-gray-600">ยังไม่ส่ง</p>
                                    <p class="text-lg font-semibold text-red-600">20 คน</p>
                                </div>
                            </div>

                            <div class="bg-gray-50 rounded-xl p-4 mb-6">
                                <h4 class="font-medium text-gray-800 mb-2">รายละเอียดงาน</h4>
                                <p class="text-gray-600">ทำแบบฝึกหัดหน้า 45-50 ในหนังสือเรียน</p>
                            </div>
                        </div>

                        <!-- แท็บอื่นๆ จะมีโครงสร้างคล้ายกัน -->
                        <div id="workTab3" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 3: โครงงาน</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 3...</p>
                        </div>

                        <div id="workTab4" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 4</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 4...</p>
                        </div>

                        <div id="workTab5" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 5</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 5...</p>
                        </div>

                        <div id="workTab6" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 6</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 6...</p>
                        </div>

                        <div id="workTab7" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 7</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 7...</p>
                        </div>

                        <div id="workTab8" class="work-tab-content hidden">
                            <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ 8</h3>
                            <p class="text-gray-600">เนื้อหาของงานที่ 8...</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- จัดการข่าว -->
            <div id="manage-news" class="teacher-section hidden">
                <div class="bg-white rounded-2xl shadow-lg p-6 mb-6">
                    <h3 class="text-lg font-bold text-gray-800 mb-4">เพิ่มข่าวประกาศ</h3>
                    
                    <form onsubmit="addNews(event)" class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">หัวข้อข่าว</label>
                            <input type="text" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">เนื้อหาข่าว</label>
                            <textarea rows="4" class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none"></textarea>
                        </div>
                        
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">แนบไฟล์ (ถ้ามี)</label>
                            <div class="border-2 border-dashed border-gray-300 rounded-xl p-4 text-center hover:border-green-400 transition-colors">
                                <input type="file" class="hidden" id="newsFile" accept=".pdf,.doc,.docx,.jpg,.png,.xlsx,.xls" onchange="handleNewsFileSelect(event)">
                                <label for="newsFile" class="cursor-pointer">
                                    <div class="text-2xl mb-2">📎</div>
                                    <p class="text-gray-600">คลิกเพื่อเลือกไฟล์</p>
                                </label>
                                <div id="selectedNewsFileName" class="mt-2 text-sm text-green-600 hidden"></div>
                            </div>
                        </div>
                        
                        <button type="submit" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-6 rounded-xl transition-colors duration-200">
                            📢 เผยแพร่ข่าว
                        </button>
                    </form>
                </div>
                
                <div class="bg-white rounded-2xl shadow-lg p-6">
                    <h3 class="text-lg font-bold text-gray-800 mb-4">ข่าวประกาศทั้งหมด</h3>
                    
                    <div class="space-y-3">
                        <div class="flex items-start justify-between p-4 border border-gray-200 rounded-xl">
                            <div class="flex-1">
                                <h4 class="font-medium text-gray-800">ประกาศสำคัญ</h4>
                                <p class="text-sm text-gray-600 mt-1">การสอบกลางภาคจะจัดขึ้นในวันที่ 15-20 มีนาคม 2024</p>
                                <p class="text-xs text-gray-500 mt-2">1 มีนาคม 2024</p>
                            </div>
                            <button class="text-red-500 hover:text-red-700 p-2">🗑️</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- รายงาน -->
            <div id="reports" class="teacher-section hidden">
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-6">
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <h3 class="text-lg font-bold text-gray-800 mb-4">รายงานการเช็คชื่อ</h3>
                        
                        <div class="space-y-3 mb-4">
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="text-sm">สมชาย ใจดี (เลขที่ 1)</span>
                                <span class="text-xs bg-green-100 text-green-800 px-2 py-1 rounded">มาเรียน</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="text-sm">สมหญิง รักเรียน (เลขที่ 2)</span>
                                <span class="text-xs bg-green-100 text-green-800 px-2 py-1 rounded">มาเรียน</span>
                            </div>
                            <div class="flex justify-between items-center p-3 bg-gray-50 rounded-lg">
                                <span class="text-sm">สมศักดิ์ ขยัน (เลขที่ 3)</span>
                                <span class="text-xs bg-red-100 text-red-800 px-2 py-1 rounded">ขาดเรียน</span>
                            </div>
                        </div>
                        
                        <div class="flex space-x-3">
                            <button onclick="downloadAttendanceExcel()" class="flex-1 bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                📊 Excel
                            </button>
                            <button onclick="downloadAttendanceWord()" class="flex-1 bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                📋 Word
                            </button>
                        </div>
                    </div>
                    
                    <div class="bg-white rounded-2xl shadow-lg p-6">
                        <h3 class="text-lg font-bold text-gray-800 mb-4">รายงานการส่งงาน</h3>
                        
                        <div class="space-y-3 mb-4">
                            <div class="p-3 bg-gray-50 rounded-lg">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="font-medium text-sm">งานที่ 1: เรียงความ</span>
                                    <span class="text-xs text-gray-500">15/28 คน</span>
                                </div>
                                <div class="w-full bg-gray-200 rounded-full h-2">
                                    <div class="bg-green-500 h-2 rounded-full" style="width: 54%"></div>
                                </div>
                            </div>
                            
                            <div class="p-3 bg-gray-50 rounded-lg">
                                <div class="flex justify-between items-center mb-2">
                                    <span class="font-medium text-sm">งานที่ 2: แบบฝึกหัด</span>
                                    <span class="text-xs text-gray-500">8/28 คน</span>
                                </div>
                                <div class="w-full bg-gray-200 rounded-full h-2">
                                    <div class="bg-yellow-500 h-2 rounded-full" style="width: 29%"></div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="flex space-x-3">
                            <button onclick="downloadWorkReportExcel()" class="flex-1 bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                📊 Excel
                            </button>
                            <button onclick="downloadWorkReportWord()" class="flex-1 bg-purple-500 hover:bg-purple-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                                📋 Word
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </main>
    </div>

    <!-- Modal เปลี่ยนรหัสผ่าน -->
    <div id="passwordModal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-2xl shadow-xl p-6 w-full max-w-md">
            <h3 class="text-lg font-bold text-gray-800 mb-4">เปลี่ยนรหัสผ่าน</h3>
            
            <form onsubmit="changePassword(event)" class="space-y-4">
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">รหัสผ่านเก่า</label>
                    <input type="password" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">รหัสผ่านใหม่</label>
                    <input type="password" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">ยืนยันรหัสผ่านใหม่</label>
                    <input type="password" required class="w-full px-4 py-3 border border-gray-300 rounded-xl focus:ring-2 focus:ring-green-500 focus:border-transparent outline-none">
                </div>
                
                <div class="flex space-x-3">
                    <button type="submit" class="flex-1 bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                        บันทึก
                    </button>
                    <button type="button" onclick="hidePasswordChange()" class="flex-1 bg-gray-300 hover:bg-gray-400 text-gray-700 font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                        ยกเลิก
                    </button>
                </div>
            </form>
        </div>
    </div>

    <script>
        // ข้อมูลจำลอง
        let teacherPassword = 'teacher123';
        let students = [];
        let works = [];
        let news = [];
        let attendance = [];

        // ฟังก์ชันแสดงหน้าต่างๆ
        function showRoleSelection() {
            hideAllPages();
            document.getElementById('roleSelection').classList.remove('hidden');
        }

        function showStudentPage() {
            hideAllPages();
            document.getElementById('studentPage').classList.remove('hidden');
            showStudentSection('attendance');
        }

        function showTeacherLogin() {
            hideAllPages();
            document.getElementById('teacherLogin').classList.remove('hidden');
        }

        function showTeacherPage() {
            hideAllPages();
            document.getElementById('teacherPage').classList.remove('hidden');
            showTeacherSection('dashboard');
        }

        function hideAllPages() {
            document.getElementById('roleSelection').classList.add('hidden');
            document.getElementById('teacherLogin').classList.add('hidden');
            document.getElementById('studentPage').classList.add('hidden');
            document.getElementById('teacherPage').classList.add('hidden');
        }

        // ฟังก์ชันจัดการเมนูนักเรียน
        function showStudentSection(section) {
            // ซ่อนทุกส่วน
            document.querySelectorAll('.student-section').forEach(el => el.classList.add('hidden'));
            // แสดงส่วนที่เลือก
            document.getElementById(section).classList.remove('hidden');
            
            // อัปเดตสถานะเมนู
            document.querySelectorAll('.student-nav-btn').forEach(btn => btn.classList.remove('active', 'border-white'));
            event.target.classList.add('active', 'border-white');
        }

        // ฟังก์ชันจัดการเมนูครู
        function showTeacherSection(section) {
            // ซ่อนทุกส่วน
            document.querySelectorAll('.teacher-section').forEach(el => el.classList.add('hidden'));
            // แสดงส่วนที่เลือก
            document.getElementById(section).classList.remove('hidden');
            
            // อัปเดตสถานะเมนู
            document.querySelectorAll('.teacher-nav-btn').forEach(btn => btn.classList.remove('active', 'border-white'));
            event.target.classList.add('active', 'border-white');
        }

        // ฟังก์ชันล็อกอินครู
        function teacherLogin(event) {
            event.preventDefault();
            const password = document.getElementById('teacherPassword').value;
            
            if (password === teacherPassword) {
                showTeacherPage();
                document.getElementById('teacherPassword').value = '';
            } else {
                alert('รหัสผ่านไม่ถูกต้อง');
            }
        }

        // ฟังก์ชันเช็คชื่อ
        function submitAttendance(event) {
            event.preventDefault();
            const formData = new FormData(event.target);
            
            alert('เช็คชื่อเรียบร้อยแล้ว!');
            event.target.reset();
        }

        // ฟังก์ชันตรวจสอบงาน
        function checkWork() {
            const name = document.getElementById('checkWorkName').value;
            if (name.trim()) {
                // แสดงสถานะงานตัวอย่าง
                alert(`แสดงสถานะงานของ ${name}`);
            }
        }

        // ฟังก์ชันส่งงาน
        function submitWork(event) {
            event.preventDefault();
            const fileInput = document.getElementById('workFile');
            const fileName = document.getElementById('selectedFileName');
            
            if (fileInput.files.length > 0) {
                alert(`ส่งงานเรียบร้อยแล้ว! ไฟล์: ${fileInput.files[0].name}`);
            } else {
                alert('ส่งงานเรียบร้อยแล้ว!');
            }
            
            event.target.reset();
            fileName.classList.add('hidden');
            fileName.textContent = '';
        }

        // ฟังก์ชันจัดการไฟล์งาน
        function handleWorkFileSelect(event) {
            const file = event.target.files[0];
            const fileNameDisplay = document.getElementById('selectedFileName');
            
            if (file) {
                fileNameDisplay.textContent = `✅ เลือกไฟล์: ${file.name}`;
                fileNameDisplay.classList.remove('hidden');
            } else {
                fileNameDisplay.classList.add('hidden');
                fileNameDisplay.textContent = '';
            }
        }

        // ฟังก์ชันจัดการไฟล์ข่าว
        function handleNewsFileSelect(event) {
            const file = event.target.files[0];
            const fileNameDisplay = document.getElementById('selectedNewsFileName');
            
            if (file) {
                fileNameDisplay.textContent = `✅ เลือกไฟล์: ${file.name}`;
                fileNameDisplay.classList.remove('hidden');
            } else {
                fileNameDisplay.classList.add('hidden');
                fileNameDisplay.textContent = '';
            }
        }

        // ฟังก์ชันเพิ่มงาน
        function addWork(event) {
            event.preventDefault();
            alert('เพิ่มงานใหม่เรียบร้อยแล้ว!');
            event.target.reset();
        }

        // ฟังก์ชันเพิ่มข่าว
        function addNews(event) {
            event.preventDefault();
            const fileInput = document.getElementById('newsFile');
            const fileName = document.getElementById('selectedNewsFileName');
            
            if (fileInput.files.length > 0) {
                alert(`เผยแพร่ข่าวเรียบร้อยแล้ว! พร้อมไฟล์แนบ: ${fileInput.files[0].name}`);
            } else {
                alert('เผยแพร่ข่าวเรียบร้อยแล้ว!');
            }
            
            event.target.reset();
            fileName.classList.add('hidden');
            fileName.textContent = '';
        }

        // ฟังก์ชันกรองข้อมูลนักเรียน
        function filterStudents() {
            const searchTerm = document.getElementById('searchStudent').value.toLowerCase();
            const classFilter = document.getElementById('classFilter').value;
            const tableBody = document.getElementById('studentsTableBody');
            const rows = tableBody.getElementsByTagName('tr');

            for (let i = 0; i < rows.length; i++) {
                const row = rows[i];
                const name = row.cells[1].textContent.toLowerCase();
                const className = row.cells[3].textContent;
                
                const matchesSearch = name.includes(searchTerm);
                const matchesClass = classFilter === '' || className === classFilter;
                
                if (matchesSearch && matchesClass) {
                    row.style.display = '';
                } else {
                    row.style.display = 'none';
                }
            }
        }

        // ฟังก์ชันส่งออกข้อมูลเป็น Excel
        function exportToExcel() {
            try {
                // สร้างข้อมูล CSV
                let csvContent = "เลขที่,ชื่อ-นามสกุล,ชื่อเล่น,ชั้นเรียน,การเช็คชื่อ,งานที่ส่ง,สถานะ\n";
                csvContent += "1,นางสาว กมลชนก ใจดี,กมล,ม.3/1,15/20 วัน,5/8 งาน,ปกติ\n";
                csvContent += "2,นาย จิรายุ รักเรียน,จิ๋ม,ม.3/1,12/20 วัน,6/8 งาน,เฝ้าระวัง\n";
                csvContent += "3,นางสาว ชนิดา ขยันเรียน,ดา,ม.3/1,18/20 วัน,7/8 งาน,ดีเยี่ยม\n";
                csvContent += "4,นาย ธนากร สมบูรณ์,กร,ม.3/1,8/20 วัน,3/8 งาน,ต้องปรับปรุง\n";
                csvContent += "5,นางสาว นิภาพร เก่งมาก,นิภา,ม.3/1,20/20 วัน,8/8 งาน,ดีเยี่ยม\n";
                csvContent += "1,นาย กิตติพงษ์ มานะดี,กิต,ม.3/2,16/20 วัน,6/8 งาน,ปกติ\n";
                csvContent += "2,นางสาว จันทิมา สวยงาม,จัน,ม.3/2,17/20 วัน,6/8 งาน,ดี\n";
                csvContent += "3,นาย ชัยวัฒน์ เรียนดี,ชัย,ม.3/2,13/20 วัน,5/8 งาน,เฝ้าระวัง\n";
                csvContent += "4,นางสาว ณัฐชา ฉลาดมาก,ชา,ม.3/2,19/20 วัน,7/8 งาน,ดีเยี่ยม\n";
                csvContent += "5,นาย ปิยะ ใฝ่เรียน,ปิ๋ม,ม.3/2,14/20 วัน,6/8 งาน,ปกติ\n";

                // สร้าง Blob และดาวน์โหลด
                const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
                const link = document.createElement("a");
                const url = URL.createObjectURL(blob);
                link.setAttribute("href", url);
                link.setAttribute("download", "รายชื่อนักเรียน_วิทยาศาสตร์_ว23101.csv");
                link.style.visibility = 'hidden';
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
                URL.revokeObjectURL(url);
                
                alert('✅ ดาวน์โหลดไฟล์ Excel เรียบร้อยแล้ว!');
            } catch (error) {
                alert('❌ เกิดข้อผิดพลาดในการดาวน์โหลด กรุณาลองใหม่อีกครั้ง');
                console.error('Export error:', error);
            }
        }

        // ฟังก์ชันส่งออกข้อมูลเป็น Word
        function exportToWord() {
            try {
                // สร้างเนื้อหา HTML สำหรับ Word
                let htmlContent = `
                    <html>
                    <head>
                        <meta charset="utf-8">
                        <title>รายชื่อนักเรียน</title>
                        <style>
                            body { font-family: 'TH Sarabun New', Arial, sans-serif; }
                            table { border-collapse: collapse; width: 100%; }
                            th, td { border: 1px solid black; padding: 8px; text-align: left; }
                            th { background-color: #f2f2f2; }
                            h1 { text-align: center; }
                        </style>
                    </head>
                    <body>
                        <h1>รายชื่อนักเรียน ม.3</h1>
                        <h2>รายวิชาวิทยาศาสตร์ ว23101</h2>
                        <p>วันที่พิมพ์: ${new Date().toLocaleDateString('th-TH')}</p>
                        
                        <h2>สรุปข้อมูลรวม</h2>
                        <ul>
                            <li>นักเรียนทั้งหมด: 10 คน</li>
                            <li>ห้อง ม.3/1: 5 คน</li>
                            <li>ห้อง ม.3/2: 5 คน</li>
                        </ul>
                        
                        <h2>รายละเอียดนักเรียน</h2>
                        <table>
                            <tr>
                                <th>เลขที่</th>
                                <th>ชื่อ-นามสกุล</th>
                                <th>ชื่อเล่น</th>
                                <th>ชั้นเรียน</th>
                                <th>การเช็คชื่อ</th>
                                <th>งานที่ส่ง</th>
                                <th>สถานะ</th>
                            </tr>
                            <tr><td>1</td><td>นางสาว กมลชนก ใจดี</td><td>กมล</td><td>ม.3/1</td><td>15/20 วัน</td><td>5/8 งาน</td><td>ปกติ</td></tr>
                            <tr><td>2</td><td>นาย จิรายุ รักเรียน</td><td>จิ๋ม</td><td>ม.3/1</td><td>12/20 วัน</td><td>6/8 งาน</td><td>เฝ้าระวัง</td></tr>
                            <tr><td>3</td><td>นางสาว ชนิดา ขยันเรียน</td><td>ดา</td><td>ม.3/1</td><td>18/20 วัน</td><td>7/8 งาน</td><td>ดีเยี่ยม</td></tr>
                            <tr><td>4</td><td>นาย ธนากร สมบูรณ์</td><td>กร</td><td>ม.3/1</td><td>8/20 วัน</td><td>3/8 งาน</td><td>ต้องปรับปรุง</td></tr>
                            <tr><td>5</td><td>นางสาว นิภาพร เก่งมาก</td><td>นิภา</td><td>ม.3/1</td><td>20/20 วัน</td><td>8/8 งาน</td><td>ดีเยี่ยม</td></tr>
                            <tr><td>1</td><td>นาย กิตติพงษ์ มานะดี</td><td>กิต</td><td>ม.3/2</td><td>16/20 วัน</td><td>6/8 งาน</td><td>ปกติ</td></tr>
                            <tr><td>2</td><td>นางสาว จันทิมา สวยงาม</td><td>จัน</td><td>ม.3/2</td><td>17/20 วัน</td><td>6/8 งาน</td><td>ดี</td></tr>
                            <tr><td>3</td><td>นาย ชัยวัฒน์ เรียนดี</td><td>ชัย</td><td>ม.3/2</td><td>13/20 วัน</td><td>5/8 งาน</td><td>เฝ้าระวัง</td></tr>
                            <tr><td>4</td><td>นางสาว ณัฐชา ฉลาดมาก</td><td>ชา</td><td>ม.3/2</td><td>19/20 วัน</td><td>7/8 งาน</td><td>ดีเยี่ยม</td></tr>
                            <tr><td>5</td><td>นาย ปิยะ ใฝ่เรียน</td><td>ปิ๋ม</td><td>ม.3/2</td><td>14/20 วัน</td><td>6/8 งาน</td><td>ปกติ</td></tr>
                        </table>
                    </body>
                    </html>
                `;

                // สร้างลิงก์ดาวน์โหลด
                const blob = new Blob([htmlContent], { type: 'application/msword;charset=utf-8' });
                const url = URL.createObjectURL(blob);
                const link = document.createElement("a");
                link.setAttribute("href", url);
                link.setAttribute("download", "รายชื่อนักเรียน_วิทยาศาสตร์_ว23101.doc");
                link.style.visibility = 'hidden';
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
                URL.revokeObjectURL(url);
                
                alert('✅ ดาวน์โหลดไฟล์ Word เรียบร้อยแล้ว!');
            } catch (error) {
                alert('❌ เกิดข้อผิดพลาดในการดาวน์โหลด กรุณาลองใหม่อีกครั้ง');
                console.error('Export error:', error);
            }
        }

        // ฟังก์ชันจัดการแท็บงาน
        function showWorkTab(tabNumber) {
            // ซ่อนแท็บทั้งหมด
            document.querySelectorAll('.work-tab-content').forEach(tab => tab.classList.add('hidden'));
            
            // แสดงแท็บที่เลือก
            document.getElementById('workTab' + tabNumber).classList.remove('hidden');
            
            // อัปเดตสถานะปุ่มแท็บ
            document.querySelectorAll('.work-tab-btn').forEach(btn => {
                btn.classList.remove('active', 'border-green-500', 'text-green-600');
                btn.classList.add('border-transparent', 'text-gray-500');
            });
            
            // เปิดใช้งานแท็บที่เลือก
            event.target.classList.add('active', 'border-green-500', 'text-green-600');
            event.target.classList.remove('border-transparent', 'text-gray-500');
        }

        // ฟังก์ชันเพิ่มแท็บงานใหม่
        function addNewWorkTab() {
            const tabsContainer = document.getElementById('workTabs');
            const currentTabs = document.querySelectorAll('.work-tab-btn').length;
            const newTabNumber = currentTabs + 1;
            
            // สร้างปุ่มแท็บใหม่
            const newTabButton = document.createElement('button');
            newTabButton.onclick = () => showWorkTab(newTabNumber);
            newTabButton.className = 'work-tab-btn py-4 px-2 border-b-2 border-transparent text-gray-500 hover:text-gray-700 font-medium text-sm whitespace-nowrap';
            newTabButton.textContent = `งานที่ ${newTabNumber}`;
            
            // แทรกปุ่มใหม่ก่อนปุ่ม "เพิ่มแท็บ"
            const addButton = tabsContainer.lastElementChild;
            tabsContainer.insertBefore(newTabButton, addButton);
            
            // สร้างเนื้อหาแท็บใหม่
            const tabContent = document.querySelector('.work-tab-content').parentElement;
            const newTabContent = document.createElement('div');
            newTabContent.id = `workTab${newTabNumber}`;
            newTabContent.className = 'work-tab-content hidden';
            newTabContent.innerHTML = `
                <h3 class="text-lg font-bold text-gray-800 mb-4">งานที่ ${newTabNumber}</h3>
                <p class="text-gray-600">เนื้อหาของงานที่ ${newTabNumber}...</p>
                <div class="mt-4">
                    <button onclick="editWorkDetails(${newTabNumber})" class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200 mr-3">
                        ✏️ แก้ไข
                    </button>
                    <button onclick="exportWorkReport(${newTabNumber})" class="bg-green-500 hover:bg-green-600 text-white font-medium py-2 px-4 rounded-xl transition-colors duration-200">
                        📊 ส่งออก
                    </button>
                </div>
            `;
            tabContent.appendChild(newTabContent);
            
            alert(`เพิ่มแท็บงานที่ ${newTabNumber} เรียบร้อยแล้ว!`);
        }

        // ฟังก์ชันแก้ไขรายละเอียดงาน
        function editWorkDetails(workNumber) {
            alert(`แก้ไขรายละเอียดงานที่ ${workNumber} (ฟีเจอร์นี้เป็นตัวอย่าง)`);
        }

        // ฟังก์ชันส่งออกรายงานงาน Excel
        function exportWorkExcel(workNumber) {
            let csvContent = "เลขที่,ชื่อ-นามสกุล,ชั้นเรียน,สถานะการส่ง,วันที่ส่ง,คะแนน\n";
            
            // ข้อมูลตัวอย่างสำหรับงานที่ 1
            if (workNumber === 1) {
                csvContent += "1,นางสาว กมลชนก ใจดี,ม.3/1,ส่งแล้ว,10/03/2024,85\n";
                csvContent += "2,นาย จิรายุ รักเรียน,ม.3/1,ส่งแล้ว,12/03/2024,78\n";
                csvContent += "3,นางสาว ชนิดา ขยันเรียน,ม.3/1,ส่งแล้ว,09/03/2024,92\n";
                csvContent += "4,นาย ธนากร สมบูรณ์,ม.3/1,ยังไม่ส่ง,-,-\n";
                csvContent += "5,นางสาว นิภาพร เก่งมาก,ม.3/1,ส่งแล้ว,08/03/2024,95\n";
                csvContent += "1,นาย กิตติพงษ์ มานะดี,ม.3/2,ส่งแล้ว,11/03/2024,80\n";
                csvContent += "2,นางสาว จันทิมา สวยงาม,ม.3/2,ส่งแล้ว,13/03/2024,88\n";
                csvContent += "3,นาย ชัยวัฒน์ เรียนดี,ม.3/2,ยังไม่ส่ง,-,-\n";
                csvContent += "4,นางสาว ณัฐชา ฉลาดมาก,ม.3/2,ส่งแล้ว,10/03/2024,90\n";
                csvContent += "5,นาย ปิยะ ใฝ่เรียน,ม.3/2,ส่งแล้ว,14/03/2024,82\n";
            } else if (workNumber === 2) {
                csvContent += "1,นางสาว กมลชนก ใจดี,ม.3/1,ส่งแล้ว,18/03/2024,75\n";
                csvContent += "2,นาย จิรายุ รักเรียน,ม.3/1,ยังไม่ส่ง,-,-\n";
                csvContent += "3,นางสาว ชนิดา ขยันเรียน,ม.3/1,ส่งแล้ว,17/03/2024,88\n";
                csvContent += "4,นาย ธนากร สมบูรณ์,ม.3/1,ส่งแล้ว,19/03/2024,70\n";
                csvContent += "5,นางสาว นิภาพร เก่งมาก,ม.3/1,ส่งแล้ว,16/03/2024,93\n";
                csvContent += "1,นาย กิตติพงษ์ มานะดี,ม.3/2,ยังไม่ส่ง,-,-\n";
                csvContent += "2,นางสาว จันทิมา สวยงาม,ม.3/2,ส่งแล้ว,18/03/2024,85\n";
                csvContent += "3,นาย ชัยวัฒน์ เรียนดี,ม.3/2,ส่งแล้ว,20/03/2024,77\n";
                csvContent += "4,นางสาว ณัฐชา ฉลาดมาก,ม.3/2,ยังไม่ส่ง,-,-\n";
                csvContent += "5,นาย ปิยะ ใฝ่เรียน,ม.3/2,ยังไม่ส่ง,-,-\n";
            }

            const encodedUri = encodeURI("data:text/csv;charset=utf-8," + csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", `รายงานงานที่${workNumber}_วิทยาศาสตร์_ว23101.csv`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            alert(`ดาวน์โหลดรายงานงานที่ ${workNumber} (Excel) เรียบร้อยแล้ว!`);
        }

        // ฟังก์ชันส่งออกรายงานงาน Word
        function exportWorkWord(workNumber) {
            let workTitle = workNumber === 1 ? "เรียงความ" : workNumber === 2 ? "แบบฝึกหัด" : `งานที่ ${workNumber}`;
            let submittedCount = workNumber === 1 ? 15 : workNumber === 2 ? 8 : 10;
            let totalCount = 28;
            let notSubmittedCount = totalCount - submittedCount;
            
            const htmlContent = `
                <html>
                <head>
                    <meta charset="utf-8">
                    <title>รายงานงานที่ ${workNumber} - รายวิชาวิทยาศาสตร์ ว23101</title>
                    <style>
                        body { font-family: 'TH Sarabun New', Arial, sans-serif; margin: 20px; }
                        table { border-collapse: collapse; width: 100%; margin-top: 20px; }
                        th, td { border: 1px solid black; padding: 8px; text-align: left; }
                        th { background-color: #f2f2f2; font-weight: bold; }
                        h1, h2 { text-align: center; }
                        .summary { background-color: #f9f9f9; padding: 15px; margin: 20px 0; border-radius: 5px; }
                        .submitted { color: green; font-weight: bold; }
                        .not-submitted { color: red; font-weight: bold; }
                        .header-info { text-align: right; margin-bottom: 20px; }
                    </style>
                </head>
                <body>
                    <div class="header-info">
                        <p>รายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่พิมพ์: ${new Date().toLocaleDateString('th-TH')}</p>
                    </div>
                    
                    <h1>รายงานการส่งงานที่ ${workNumber}: ${workTitle}</h1>
                    
                    <div class="summary">
                        <h2>สรุปผลการส่งงาน</h2>
                        <ul>
                            <li>นักเรียนทั้งหมด: ${totalCount} คน</li>
                            <li class="submitted">ส่งงานแล้ว: ${submittedCount} คน (${Math.round((submittedCount/totalCount)*100)}%)</li>
                            <li class="not-submitted">ยังไม่ส่งงาน: ${notSubmittedCount} คน (${Math.round((notSubmittedCount/totalCount)*100)}%)</li>
                            <li>กำหนดส่ง: ${workNumber === 1 ? '15 มีนาคม 2024' : workNumber === 2 ? '20 มีนาคม 2024' : '25 มีนาคม 2024'}</li>
                        </ul>
                    </div>
                    
                    <h2>รายละเอียดการส่งงาน</h2>
                    <table>
                        <tr>
                            <th>เลขที่</th>
                            <th>ชื่อ-นามสกุล</th>
                            <th>ชั้นเรียน</th>
                            <th>สถานะการส่ง</th>
                            <th>วันที่ส่ง</th>
                            <th>คะแนน</th>
                            <th>หมายเหตุ</th>
                        </tr>`;
            
            // เพิ่มข้อมูลนักเรียน
            if (workNumber === 1) {
                htmlContent += `
                        <tr><td>1</td><td>นางสาว กมลชนก ใจดี</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>10/03/2024</td><td>85</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>2</td><td>นาย จิรายุ รักเรียน</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>12/03/2024</td><td>78</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>3</td><td>นางสาว ชนิดา ขยันเรียน</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>09/03/2024</td><td>92</td><td>ส่งก่อนกำหนด</td></tr>
                        <tr><td>4</td><td>นาย ธนากร สมบูรณ์</td><td>ม.3/1</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                        <tr><td>5</td><td>นางสาว นิภาพร เก่งมาก</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>08/03/2024</td><td>95</td><td>ส่งก่อนกำหนด</td></tr>
                        <tr><td>1</td><td>นาย กิตติพงษ์ มานะดี</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>11/03/2024</td><td>80</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>2</td><td>นางสาว จันทิมา สวยงาม</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>13/03/2024</td><td>88</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>3</td><td>นาย ชัยวัฒน์ เรียนดี</td><td>ม.3/2</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                        <tr><td>4</td><td>นางสาว ณัฐชา ฉลาดมาก</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>10/03/2024</td><td>90</td><td>ส่งก่อนกำหนด</td></tr>
                        <tr><td>5</td><td>นาย ปิยะ ใฝ่เรียน</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>14/03/2024</td><td>82</td><td>ส่งตรงเวลา</td></tr>
                `;
            } else if (workNumber === 2) {
                htmlContent += `
                        <tr><td>1</td><td>นางสาว กมลชนก ใจดี</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>18/03/2024</td><td>75</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>2</td><td>นาย จิรายุ รักเรียน</td><td>ม.3/1</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                        <tr><td>3</td><td>นางสาว ชนิดา ขยันเรียน</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>17/03/2024</td><td>88</td><td>ส่งก่อนกำหนด</td></tr>
                        <tr><td>4</td><td>นาย ธนากร สมบูรณ์</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>19/03/2024</td><td>70</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>5</td><td>นางสาว นิภาพร เก่งมาก</td><td>ม.3/1</td><td class="submitted">ส่งแล้ว</td><td>16/03/2024</td><td>93</td><td>ส่งก่อนกำหนด</td></tr>
                        <tr><td>1</td><td>นาย กิตติพงษ์ มานะดี</td><td>ม.3/2</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                        <tr><td>2</td><td>นางสาว จันทิมา สวยงาม</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>18/03/2024</td><td>85</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>3</td><td>นาย ชัยวัฒน์ เรียนดี</td><td>ม.3/2</td><td class="submitted">ส่งแล้ว</td><td>20/03/2024</td><td>77</td><td>ส่งตรงเวลา</td></tr>
                        <tr><td>4</td><td>นางสาว ณัฐชา ฉลาดมาก</td><td>ม.3/2</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                        <tr><td>5</td><td>นาย ปิยะ ใฝ่เรียน</td><td>ม.3/2</td><td class="not-submitted">ยังไม่ส่ง</td><td>-</td><td>-</td><td>เกินกำหนด</td></tr>
                `;
            }
            
            htmlContent += `
                    </table>
                    
                    <div style="margin-top: 30px;">
                        <h3>สถิติการส่งงาน</h3>
                        <p>• คะแนนเฉลี่ย: ${workNumber === 1 ? '84.5' : workNumber === 2 ? '81.2' : '80.0'} คะแนน</p>
                        <p>• คะแนนสูงสุด: ${workNumber === 1 ? '95' : workNumber === 2 ? '93' : '90'} คะแนน</p>
                        <p>• คะแนนต่ำสุด: ${workNumber === 1 ? '78' : workNumber === 2 ? '70' : '75'} คะแนน</p>
                        <p>• อัตราการส่งงาน: ${Math.round((submittedCount/totalCount)*100)}%</p>
                    </div>
                    
                    <div style="margin-top: 40px; text-align: center;">
                        <p>รายงานนี้สร้างโดยระบบจัดการรายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่: ${new Date().toLocaleDateString('th-TH')} เวลา: ${new Date().toLocaleTimeString('th-TH')}</p>
                    </div>
                </body>
                </html>
            `;

            const blob = new Blob([htmlContent], { type: 'application/msword' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement("a");
            link.setAttribute("href", url);
            link.setAttribute("download", `รายงานงานที่${workNumber}_${workTitle}_วิทยาศาสตร์_ว23101.doc`);
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            
            alert(`ดาวน์โหลดรายงานงานที่ ${workNumber} (Word) เรียบร้อยแล้ว!`);
        }

        // ฟังก์ชันดาวน์โหลดรายงานการเช็คชื่อ Excel
        function downloadAttendanceExcel() {
            let csvContent = "เลขที่,ชื่อ-นามสกุล,ชั้นเรียน,สถานะ,วันที่เช็คชื่อ,เวลา\n";
            csvContent += "1,นางสาว กมลชนก ใจดี,ม.3/1,มาเรียน,01/03/2024,08:00\n";
            csvContent += "2,นาย จิรายุ รักเรียน,ม.3/1,มาเรียน,01/03/2024,08:05\n";
            csvContent += "3,นางสาว ชนิดา ขยันเรียน,ม.3/1,มาเรียน,01/03/2024,07:55\n";
            csvContent += "4,นาย ธนากร สมบูรณ์,ม.3/1,ขาดเรียน,01/03/2024,-\n";
            csvContent += "5,นางสาว นิภาพร เก่งมาก,ม.3/1,มาเรียน,01/03/2024,07:50\n";
            csvContent += "1,นาย กิตติพงษ์ มานะดี,ม.3/2,มาเรียน,01/03/2024,08:10\n";
            csvContent += "2,นางสาว จันทิมา สวยงาม,ม.3/2,มาเรียน,01/03/2024,08:02\n";
            csvContent += "3,นาย ชัยวัฒน์ เรียนดี,ม.3/2,สาย,01/03/2024,08:15\n";
            csvContent += "4,นางสาว ณัฐชา ฉลาดมาก,ม.3/2,มาเรียน,01/03/2024,07:58\n";
            csvContent += "5,นาย ปิยะ ใฝ่เรียน,ม.3/2,มาเรียน,01/03/2024,08:03\n";

            const encodedUri = encodeURI("data:text/csv;charset=utf-8," + csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "รายงานการเช็คชื่อ_วิทยาศาสตร์_ว23101.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            alert('ดาวน์โหลดรายงานการเช็คชื่อ (Excel) เรียบร้อยแล้ว!');
        }

        // ฟังก์ชันดาวน์โหลดรายงานการเช็คชื่อ Word
        function downloadAttendanceWord() {
            const htmlContent = `
                <html>
                <head>
                    <meta charset="utf-8">
                    <title>รายงานการเช็คชื่อ - รายวิชาวิทยาศาสตร์ ว23101</title>
                    <style>
                        body { font-family: 'TH Sarabun New', Arial, sans-serif; margin: 20px; }
                        table { border-collapse: collapse; width: 100%; margin-top: 20px; }
                        th, td { border: 1px solid black; padding: 8px; text-align: left; }
                        th { background-color: #f2f2f2; font-weight: bold; }
                        h1, h2 { text-align: center; }
                        .summary { background-color: #f9f9f9; padding: 15px; margin: 20px 0; border-radius: 5px; }
                        .present { color: green; font-weight: bold; }
                        .absent { color: red; font-weight: bold; }
                        .late { color: orange; font-weight: bold; }
                        .header-info { text-align: right; margin-bottom: 20px; }
                    </style>
                </head>
                <body>
                    <div class="header-info">
                        <p>รายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่พิมพ์: ${new Date().toLocaleDateString('th-TH')}</p>
                    </div>
                    
                    <h1>รายงานการเช็คชื่อประจำวัน</h1>
                    <h2>วันที่ 1 มีนาคม 2024</h2>
                    
                    <div class="summary">
                        <h2>สรุปการเข้าเรียน</h2>
                        <ul>
                            <li>นักเรียนทั้งหมด: 10 คน</li>
                            <li class="present">มาเรียน: 8 คน (80%)</li>
                            <li class="late">มาสาย: 1 คน (10%)</li>
                            <li class="absent">ขาดเรียน: 1 คน (10%)</li>
                        </ul>
                    </div>
                    
                    <h2>รายละเอียดการเช็คชื่อ</h2>
                    <table>
                        <tr>
                            <th>เลขที่</th>
                            <th>ชื่อ-นามสกุล</th>
                            <th>ชั้นเรียน</th>
                            <th>สถานะ</th>
                            <th>เวลาเช็คชื่อ</th>
                            <th>หมายเหตุ</th>
                        </tr>
                        <tr><td>1</td><td>นางสาว กมลชนก ใจดี</td><td>ม.3/1</td><td class="present">มาเรียน</td><td>08:00</td><td>ตรงเวลา</td></tr>
                        <tr><td>2</td><td>นาย จิรายุ รักเรียน</td><td>ม.3/1</td><td class="present">มาเรียน</td><td>08:05</td><td>ตรงเวลา</td></tr>
                        <tr><td>3</td><td>นางสาว ชนิดา ขยันเรียน</td><td>ม.3/1</td><td class="present">มาเรียน</td><td>07:55</td><td>มาก่อนเวลา</td></tr>
                        <tr><td>4</td><td>นาย ธนากร สมบูรณ์</td><td>ม.3/1</td><td class="absent">ขาดเรียน</td><td>-</td><td>ไม่มาเรียน</td></tr>
                        <tr><td>5</td><td>นางสาว นิภาพร เก่งมาก</td><td>ม.3/1</td><td class="present">มาเรียน</td><td>07:50</td><td>มาก่อนเวลา</td></tr>
                        <tr><td>1</td><td>นาย กิตติพงษ์ มานะดี</td><td>ม.3/2</td><td class="present">มาเรียน</td><td>08:10</td><td>ตรงเวลา</td></tr>
                        <tr><td>2</td><td>นางสาว จันทิมา สวยงาม</td><td>ม.3/2</td><td class="present">มาเรียน</td><td>08:02</td><td>ตรงเวลา</td></tr>
                        <tr><td>3</td><td>นาย ชัยวัฒน์ เรียนดี</td><td>ม.3/2</td><td class="late">มาสาย</td><td>08:15</td><td>สาย 15 นาที</td></tr>
                        <tr><td>4</td><td>นางสาว ณัฐชา ฉลาดมาก</td><td>ม.3/2</td><td class="present">มาเรียน</td><td>07:58</td><td>มาก่อนเวลา</td></tr>
                        <tr><td>5</td><td>นาย ปิยะ ใฝ่เรียน</td><td>ม.3/2</td><td class="present">มาเรียน</td><td>08:03</td><td>ตรงเวลา</td></tr>
                    </table>
                    
                    <div style="margin-top: 30px;">
                        <h3>สถิติการเข้าเรียน</h3>
                        <p>• อัตราการเข้าเรียน: 90% (9/10 คน)</p>
                        <p>• อัตราการมาสาย: 10% (1/10 คน)</p>
                        <p>• อัตราการขาดเรียน: 10% (1/10 คน)</p>
                        <p>• เวลาเฉลี่ยในการเช็คชื่อ: 08:02 น.</p>
                    </div>
                    
                    <div style="margin-top: 40px; text-align: center;">
                        <p>รายงานนี้สร้างโดยระบบจัดการรายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่: ${new Date().toLocaleDateString('th-TH')} เวลา: ${new Date().toLocaleTimeString('th-TH')}</p>
                    </div>
                </body>
                </html>
            `;

            const blob = new Blob([htmlContent], { type: 'application/msword' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement("a");
            link.setAttribute("href", url);
            link.setAttribute("download", "รายงานการเช็คชื่อ_วิทยาศาสตร์_ว23101.doc");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            
            alert('ดาวน์โหลดรายงานการเช็คชื่อ (Word) เรียบร้อยแล้ว!');
        }

        // ฟังก์ชันดาวน์โหลดรายงานการส่งงาน Excel
        function downloadWorkReportExcel() {
            let csvContent = "งาน,กำหนดส่ง,ส่งแล้ว,ยังไม่ส่ง,อัตราการส่ง,คะแนนเฉลี่ย\n";
            csvContent += "งานที่ 1: เรียงความ,15/03/2024,15,13,53.6%,84.5\n";
            csvContent += "งานที่ 2: แบบฝึกหัด,20/03/2024,8,20,28.6%,81.2\n";
            csvContent += "งานที่ 3: โครงงาน,25/03/2024,5,23,17.9%,87.0\n";
            csvContent += "งานที่ 4: รายงาน,30/03/2024,12,16,42.9%,82.3\n";
            csvContent += "งานที่ 5: การทดลอง,05/04/2024,18,10,64.3%,85.8\n";
            csvContent += "งานที่ 6: แบบทดสอบ,10/04/2024,22,6,78.6%,79.4\n";
            csvContent += "งานที่ 7: นำเสนอ,15/04/2024,14,14,50.0%,88.2\n";
            csvContent += "งานที่ 8: สรุป,20/04/2024,10,18,35.7%,83.6\n";

            const encodedUri = encodeURI("data:text/csv;charset=utf-8," + csvContent);
            const link = document.createElement("a");
            link.setAttribute("href", encodedUri);
            link.setAttribute("download", "รายงานการส่งงาน_วิทยาศาสตร์_ว23101.csv");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            
            alert('ดาวน์โหลดรายงานการส่งงาน (Excel) เรียบร้อยแล้ว!');
        }

        // ฟังก์ชันดาวน์โหลดรายงานการส่งงาน Word
        function downloadWorkReportWord() {
            const htmlContent = `
                <html>
                <head>
                    <meta charset="utf-8">
                    <title>รายงานการส่งงาน - รายวิชาวิทยาศาสตร์ ว23101</title>
                    <style>
                        body { font-family: 'TH Sarabun New', Arial, sans-serif; margin: 20px; }
                        table { border-collapse: collapse; width: 100%; margin-top: 20px; }
                        th, td { border: 1px solid black; padding: 8px; text-align: center; }
                        th { background-color: #f2f2f2; font-weight: bold; }
                        h1, h2 { text-align: center; }
                        .summary { background-color: #f9f9f9; padding: 15px; margin: 20px 0; border-radius: 5px; }
                        .good { color: green; font-weight: bold; }
                        .warning { color: orange; font-weight: bold; }
                        .poor { color: red; font-weight: bold; }
                        .header-info { text-align: right; margin-bottom: 20px; }
                        .progress-bar { width: 100%; height: 20px; background-color: #f0f0f0; border-radius: 10px; overflow: hidden; }
                        .progress-fill { height: 100%; background-color: #4CAF50; }
                    </style>
                </head>
                <body>
                    <div class="header-info">
                        <p>รายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่พิมพ์: ${new Date().toLocaleDateString('th-TH')}</p>
                    </div>
                    
                    <h1>รายงานการส่งงานรวม</h1>
                    <h2>ภาคเรียนที่ 2/2567</h2>
                    
                    <div class="summary">
                        <h2>สรุปภาพรวม</h2>
                        <ul>
                            <li>จำนวนงานทั้งหมด: 8 งาน</li>
                            <li>นักเรียนทั้งหมด: 28 คน</li>
                            <li>อัตราการส่งงานเฉลี่ย: 46.4%</li>
                            <li>คะแนนเฉลี่ยรวม: 84.0 คะแนน</li>
                        </ul>
                    </div>
                    
                    <h2>รายละเอียดการส่งงานแต่ละชิ้น</h2>
                    <table>
                        <tr>
                            <th>งาน</th>
                            <th>กำหนดส่ง</th>
                            <th>ส่งแล้ว</th>
                            <th>ยังไม่ส่ง</th>
                            <th>อัตราการส่ง</th>
                            <th>คะแนนเฉลี่ย</th>
                            <th>สถานะ</th>
                        </tr>
                        <tr><td>งานที่ 1: เรียงความ</td><td>15/03/2024</td><td>15</td><td>13</td><td>53.6%</td><td>84.5</td><td class="warning">ปานกลาง</td></tr>
                        <tr><td>งานที่ 2: แบบฝึกหัด</td><td>20/03/2024</td><td>8</td><td>20</td><td>28.6%</td><td>81.2</td><td class="poor">ต้องปรับปรุง</td></tr>
                        <tr><td>งานที่ 3: โครงงาน</td><td>25/03/2024</td><td>5</td><td>23</td><td>17.9%</td><td>87.0</td><td class="poor">ต้องปรับปรุง</td></tr>
                        <tr><td>งานที่ 4: รายงาน</td><td>30/03/2024</td><td>12</td><td>16</td><td>42.9%</td><td>82.3</td><td class="warning">ปานกลาง</td></tr>
                        <tr><td>งานที่ 5: การทดลอง</td><td>05/04/2024</td><td>18</td><td>10</td><td>64.3%</td><td>85.8</td><td class="good">ดี</td></tr>
                        <tr><td>งานที่ 6: แบบทดสอบ</td><td>10/04/2024</td><td>22</td><td>6</td><td>78.6%</td><td>79.4</td><td class="good">ดี</td></tr>
                        <tr><td>งานที่ 7: นำเสนอ</td><td>15/04/2024</td><td>14</td><td>14</td><td>50.0%</td><td>88.2</td><td class="warning">ปานกลาง</td></tr>
                        <tr><td>งานที่ 8: สรุป</td><td>20/04/2024</td><td>10</td><td>18</td><td>35.7%</td><td>83.6</td><td class="poor">ต้องปรับปรุง</td></tr>
                    </table>
                    
                    <div style="margin-top: 30px;">
                        <h3>การวิเคราะห์และข้อเสนอแนะ</h3>
                        <p><strong>จุดแข็ง:</strong></p>
                        <ul>
                            <li>งานที่ 6 (แบบทดสอบ) มีอัตราการส่งสูงสุด 78.6%</li>
                            <li>งานที่ 7 (นำเสนอ) มีคะแนนเฉลี่ยสูงสุด 88.2 คะแนน</li>
                            <li>คุณภาพงานโดยรวมอยู่ในระดับดี (คะแนนเฉลี่ย 84.0)</li>
                        </ul>
                        
                        <p><strong>จุดที่ต้องปรับปรุง:</strong></p>
                        <ul>
                            <li>งานที่ 3 (โครงงาน) มีอัตราการส่งต่ำสุด 17.9%</li>
                            <li>ควรติดตามนักเรียนที่ส่งงานไม่สม่ำเสมอ</li>
                            <li>ปรับปรุงการแจ้งเตือนกำหนดส่งงาน</li>
                        </ul>
                        
                        <p><strong>สถิติสำคัญ:</strong></p>
                        <ul>
                            <li>อัตราการส่งงานสูงสุด: 78.6% (งานที่ 6)</li>
                            <li>อัตราการส่งงานต่ำสุด: 17.9% (งานที่ 3)</li>
                            <li>คะแนนเฉลี่ยสูงสุด: 88.2 คะแนน (งานที่ 7)</li>
                            <li>คะแนนเฉลี่ยต่ำสุด: 79.4 คะแนน (งานที่ 6)</li>
                        </ul>
                    </div>
                    
                    <div style="margin-top: 40px; text-align: center;">
                        <p>รายงานนี้สร้างโดยระบบจัดการรายวิชาวิทยาศาสตร์ ว23101</p>
                        <p>วันที่: ${new Date().toLocaleDateString('th-TH')} เวลา: ${new Date().toLocaleTimeString('th-TH')}</p>
                    </div>
                </body>
                </html>
            `;

            const blob = new Blob([htmlContent], { type: 'application/msword' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement("a");
            link.setAttribute("href", url);
            link.setAttribute("download", "รายงานการส่งงาน_วิทยาศาสตร์_ว23101.doc");
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
            URL.revokeObjectURL(url);
            
            alert('ดาวน์โหลดรายงานการส่งงาน (Word) เรียบร้อยแล้ว!');
        }

        // ฟังก์ชันจัดการรหัสผ่าน
        function showPasswordChange() {
            document.getElementById('passwordModal').classList.remove('hidden');
        }

        function hidePasswordChange() {
            document.getElementById('passwordModal').classList.add('hidden');
        }

        function changePassword(event) {
            event.preventDefault();
            alert('เปลี่ยนรหัสผ่านเรียบร้อยแล้ว!');
            hidePasswordChange();
            event.target.reset();
        }

        // ตัวแปรสำหรับเก็บข้อมูลที่นำเข้า
        let importedData = [];
        let importedStudentData = [];

        // ฟังก์ชันจัดการแท็บวิธีเพิ่มข้อมูล
        function showAddMethod(method) {
            // ซ่อนเนื้อหาทั้งหมด
            document.querySelectorAll('.add-method-content').forEach(content => content.classList.add('hidden'));
            
            // แสดงเนื้อหาที่เลือก
            if (method === 'manual') {
                document.getElementById('manualAdd').classList.remove('hidden');
            } else if (method === 'import') {
                document.getElementById('importAdd').classList.remove('hidden');
            }
            
            // อัปเดตสถานะปุ่มแท็บ
            document.querySelectorAll('.add-method-btn').forEach(btn => {
                btn.classList.remove('active', 'border-blue-500', 'text-blue-600');
                btn.classList.add('border-transparent', 'text-gray-500');
            });
            
            // เปิดใช้งานแท็บที่เลือก
            event.target.classList.add('active', 'border-blue-500', 'text-blue-600');
            event.target.classList.remove('border-transparent', 'text-gray-500');
        }

        // ฟังก์ชันจัดการแท็บวิธีอัปโหลดนักเรียน
        function showUploadMethod(method) {
            // ซ่อนเนื้อหาทั้งหมด
            document.querySelectorAll('.upload-method-content').forEach(content => content.classList.add('hidden'));
            
            // แสดงเนื้อหาที่เลือก
            if (method === 'manual') {
                document.getElementById('manualUpload').classList.remove('hidden');
            } else if (method === 'import') {
                document.getElementById('importUpload').classList.remove('hidden');
            }
            
            // อัปเดตสถานะปุ่มแท็บ
            document.querySelectorAll('.upload-method-btn').forEach(btn => {
                btn.classList.remove('active', 'border-green-500', 'text-green-600');
                btn.classList.add('border-transparent', 'text-gray-500');
            });
            
            // เปิดใช้งานแท็บที่เลือก
            event.target.classList.add('active', 'border-green-500', 'text-green-600');
            event.target.classList.remove('border-transparent', 'text-gray-500');
        }

        // ฟังก์ชันเพิ่มนักเรียนทีละคน
        function addSingleStudent(event) {
            event.preventDefault();
            const formData = new FormData(event.target);
            
            // ในระบบจริงจะบันทึกลงฐานข้อมูล
            alert('เพิ่มนักเรียนเรียบร้อยแล้ว!');
            event.target.reset();
            
            // รีเฟรชตารางรายชื่อ (ในระบบจริง)
            // refreshStudentTable();
        }

        // ฟังก์ชันดาวน์โหลดแม่แบบ
        function downloadTemplate(type) {
            if (type === 'excel') {
                // สร้างไฟล์ CSV แม่แบบ
                const csvContent = "เลขที่,ชื่อจริง,นามสกุล,ชื่อเล่น,ชั้นเรียน\n1,สมชาย,ใจดี,ชาย,ม.3/1\n2,สมหญิง,รักเรียน,หญิง,ม.3/1\n3,สมศักดิ์,ขยัน,ศักดิ์,ม.3/2";
                
                const encodedUri = encodeURI("data:text/csv;charset=utf-8," + csvContent);
                const link = document.createElement("a");
                link.setAttribute("href", encodedUri);
                link.setAttribute("download", "แม่แบบรายชื่อนักเรียน.csv");
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
                
                alert('ดาวน์โหลดแม่แบบ Excel เรียบร้อยแล้ว!');
                
            } else if (type === 'word') {
                // สร้างไฟล์ Word แม่แบบ
                const htmlContent = `
                    <html>
                    <head>
                        <meta charset="utf-8">
                        <title>แม่แบบรายชื่อนักเรียน</title>
                        <style>
                            body { font-family: 'TH Sarabun New', Arial, sans-serif; }
                            table { border-collapse: collapse; width: 100%; }
                            th, td { border: 1px solid black; padding: 8px; text-align: left; }
                            th { background-color: #f2f2f2; }
                            h1 { text-align: center; }
                        </style>
                    </head>
                    <body>
                        <h1>แม่แบบรายชื่อนักเรียน</h1>
                        <p>กรุณากรอกข้อมูลในตารางด้านล่าง</p>
                        
                        <table>
                            <tr>
                                <th>เลขที่</th>
                                <th>ชื่อจริง</th>
                                <th>นามสกุล</th>
                                <th>ชื่อเล่น</th>
                                <th>ชั้นเรียน</th>
                            </tr>
                            <tr><td>1</td><td>สมชาย</td><td>ใจดี</td><td>ชาย</td><td>ม.3/1</td></tr>
                            <tr><td>2</td><td>สมหญิง</td><td>รักเรียน</td><td>หญิง</td><td>ม.3/1</td></tr>
                            <tr><td>3</td><td>สมศักดิ์</td><td>ขยัน</td><td>ศักดิ์</td><td>ม.3/2</td></tr>
                            <tr><td></td><td></td><td></td><td></td><td></td></tr>
                            <tr><td></td><td></td><td></td><td></td><td></td></tr>
                            <tr><td></td><td></td><td></td><td></td><td></td></tr>
                        </table>
                    </body>
                    </html>
                `;

                const blob = new Blob([htmlContent], { type: 'application/msword' });
                const url = URL.createObjectURL(blob);
                const link = document.createElement("a");
                link.setAttribute("href", url);
                link.setAttribute("download", "แม่แบบรายชื่อนักเรียน.doc");
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
                URL.revokeObjectURL(url);
                
                alert('ดาวน์โหลดแม่แบบ Word เรียบร้อยแล้ว!');
            }
        }

        // ฟังก์ชันดาวน์โหลดแม่แบบนักเรียน
        function downloadStudentTemplate(type) {
            try {
                if (type === 'excel') {
                    // สร้างไฟล์ CSV แม่แบบ
                    const csvContent = "เลขที่,ชื่อจริง,นามสกุล,ชื่อเล่น,ชั้นเรียน\n1,สมชาย,ใจดี,ชาย,ม.3/1\n2,สมหญิง,รักเรียน,หญิง,ม.3/1\n3,สมศักดิ์,ขยัน,ศักดิ์,ม.3/2\n4,สมใจ,เรียนดี,ใจ,ม.3/1\n5,สมปอง,มานะดี,ปอง,ม.3/2";
                    
                    const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
                    const link = document.createElement("a");
                    const url = URL.createObjectURL(blob);
                    link.setAttribute("href", url);
                    link.setAttribute("download", "แม่แบบรายชื่อนักเรียน_วิทยาศาสตร์_ว23101.csv");
                    link.style.visibility = 'hidden';
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);
                    URL.revokeObjectURL(url);
                    
                    alert('✅ ดาวน์โหลดแม่แบบ Excel เรียบร้อยแล้ว!');
                    
                } else if (type === 'word') {
                    // สร้างไฟล์ Word แม่แบบ
                    const htmlContent = `
                        <html>
                        <head>
                            <meta charset="utf-8">
                            <title>แม่แบบรายชื่อนักเรียน - รายวิชาวิทยาศาสตร์ ว23101</title>
                            <style>
                                body { font-family: 'TH Sarabun New', Arial, sans-serif; margin: 20px; }
                                table { border-collapse: collapse; width: 100%; margin-top: 20px; }
                                th, td { border: 1px solid black; padding: 8px; text-align: left; }
                                th { background-color: #f2f2f2; font-weight: bold; }
                                h1, h2 { text-align: center; }
                                .instructions { background-color: #f9f9f9; padding: 15px; margin: 20px 0; border-radius: 5px; }
                            </style>
                        </head>
                        <body>
                            <h1>แม่แบบรายชื่อนักเรียน</h1>
                            <h2>รายวิชาวิทยาศาสตร์ ว23101</h2>
                            
                            <div class="instructions">
                                <h3>คำแนะนำการใช้งาน:</h3>
                                <ol>
                                    <li>กรุณากรอกข้อมูลนักเรียนในตารางด้านล่าง</li>
                                    <li>ห้ามเปลี่ยนหัวข้อคอลัมน์</li>
                                    <li>กรอกข้อมูลให้ครบทุกช่อง</li>
                                    <li>ชั้นเรียนให้ใส่เป็น ม.3/1 หรือ ม.3/2 เท่านั้น</li>
                                    <li>เมื่อกรอกเสร็จแล้วให้บันทึกไฟล์และอัปโหลดในระบบ</li>
                                </ol>
                            </div>
                            
                            <table>
                                <tr>
                                    <th>เลขที่</th>
                                    <th>ชื่อจริง</th>
                                    <th>นามสกุล</th>
                                    <th>ชื่อเล่น</th>
                                    <th>ชั้นเรียน</th>
                                </tr>
                                <tr><td>1</td><td>สมชาย</td><td>ใจดี</td><td>ชาย</td><td>ม.3/1</td></tr>
                                <tr><td>2</td><td>สมหญิง</td><td>รักเรียน</td><td>หญิง</td><td>ม.3/1</td></tr>
                                <tr><td>3</td><td>สมศักดิ์</td><td>ขยัน</td><td>ศักดิ์</td><td>ม.3/2</td></tr>
                                <tr><td>4</td><td>สมใจ</td><td>เรียนดี</td><td>ใจ</td><td>ม.3/1</td></tr>
                                <tr><td>5</td><td>สมปอง</td><td>มานะดี</td><td>ปอง</td><td>ม.3/2</td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                                <tr><td></td><td></td><td></td><td></td><td></td></tr>
                            </table>
                            
                            <div style="margin-top: 30px; text-align: center;">
                                <p>แม่แบบนี้สร้างโดยระบบจัดการรายวิชาวิทยาศาสตร์ ว23101</p>
                                <p>วันที่: ${new Date().toLocaleDateString('th-TH')}</p>
                            </div>
                        </body>
                        </html>
                    `;

                    const blob = new Blob([htmlContent], { type: 'application/msword;charset=utf-8' });
                    const url = URL.createObjectURL(blob);
                    const link = document.createElement("a");
                    link.setAttribute("href", url);
                    link.setAttribute("download", "แม่แบบรายชื่อนักเรียน_วิทยาศาสตร์_ว23101.doc");
                    link.style.visibility = 'hidden';
                    document.body.appendChild(link);
                    link.click();
                    document.body.removeChild(link);
                    URL.revokeObjectURL(url);
                    
                    alert('✅ ดาวน์โหลดแม่แบบ Word เรียบร้อยแล้ว!');
                }
            } catch (error) {
                alert('❌ เกิดข้อผิดพลาดในการดาวน์โหลด กรุณาลองใหม่อีกครั้ง');
                console.error('Download error:', error);
            }
        }

        // ฟังก์ชันจัดการการนำเข้าไฟล์
        function handleFileImport(event) {
            const file = event.target.files[0];
            if (!file) return;

            const fileName = file.name.toLowerCase();
            const fileExtension = fileName.split('.').pop();

            // ตรวจสอบประเภทไฟล์
            if (!['xlsx', 'xls', 'docx', 'csv'].includes(fileExtension)) {
                alert('ประเภทไฟล์ไม่รองรับ กรุณาเลือกไฟล์ Excel, Word หรือ CSV');
                return;
            }

            // อ่านไฟล์
            const reader = new FileReader();
            
            if (fileExtension === 'csv') {
                reader.onload = function(e) {
                    const csv = e.target.result;
                    parseCSVData(csv);
                };
                reader.readAsText(file, 'UTF-8');
            } else {
                // สำหรับ Excel และ Word ในระบบจริงจะใช้ library เช่น SheetJS
                // ที่นี่จะจำลองข้อมูล
                setTimeout(() => {
                    simulateFileImport(fileExtension);
                }, 1000);
            }
        }

        // ฟังก์ชันจัดการการนำเข้าไฟล์นักเรียน
        function handleStudentFileImport(event) {
            const file = event.target.files[0];
            const fileNameDisplay = document.getElementById('selectedStudentFileName');
            
            if (!file) {
                fileNameDisplay.classList.add('hidden');
                return;
            }

            const fileName = file.name.toLowerCase();
            const fileExtension = fileName.split('.').pop();

            // ตรวจสอบประเภทไฟล์
            if (!['xlsx', 'xls', 'docx', 'csv'].includes(fileExtension)) {
                alert('❌ ประเภทไฟล์ไม่รองรับ กรุณาเลือกไฟล์ Excel (.xlsx, .xls), Word (.docx) หรือ CSV');
                event.target.value = '';
                fileNameDisplay.classList.add('hidden');
                return;
            }

            // แสดงชื่อไฟล์ที่เลือก
            fileNameDisplay.textContent = `✅ เลือกไฟล์: ${file.name}`;
            fileNameDisplay.classList.remove('hidden');

            // อ่านไฟล์
            const reader = new FileReader();
            
            if (fileExtension === 'csv') {
                reader.onload = function(e) {
                    const csv = e.target.result;
                    parseStudentCSVData(csv);
                };
                reader.readAsText(file, 'UTF-8');
            } else {
                // สำหรับ Excel และ Word ในระบบจริงจะใช้ library เช่น SheetJS
                // ที่นี่จะจำลองข้อมูล
                setTimeout(() => {
                    simulateStudentFileImport(fileExtension);
                }, 1000);
            }
        }

        // ฟังก์ชันแปลงข้อมูล CSV
        function parseCSVData(csvText) {
            const lines = csvText.split('\n');
            const data = [];
            
            // ข้ามหัวข้อ (บรรทัดแรก)
            for (let i = 1; i < lines.length; i++) {
                const line = lines[i].trim();
                if (line) {
                    const columns = line.split(',');
                    if (columns.length >= 5) {
                        data.push({
                            number: columns[0].trim(),
                            firstName: columns[1].trim(),
                            lastName: columns[2].trim(),
                            nickname: columns[3].trim(),
                            classroom: columns[4].trim()
                        });
                    }
                }
            }
            
            if (data.length > 0) {
                importedData = data;
                showImportPreview();
            } else {
                alert('ไม่พบข้อมูลในไฟล์ กรุณาตรวจสอบรูปแบบไฟล์');
            }
        }

        // ฟังก์ชันจำลองการนำเข้าไฟล์ (สำหรับ Excel และ Word)
        function simulateFileImport(fileType) {
            // ข้อมูลจำลอง
            importedData = [
                { number: '6', firstName: 'สมชาย', lastName: 'ใจดี', nickname: 'ชาย', classroom: 'ม.3/1' },
                { number: '7', firstName: 'สมหญิง', lastName: 'รักเรียน', nickname: 'หญิง', classroom: 'ม.3/1' },
                { number: '8', firstName: 'สมศักดิ์', lastName: 'ขยัน', nickname: 'ศักดิ์', classroom: 'ม.3/2' },
                { number: '9', firstName: 'สมใจ', lastName: 'เรียนดี', nickname: 'ใจ', classroom: 'ม.3/2' },
                { number: '10', firstName: 'สมปอง', lastName: 'มานะดี', nickname: 'ปอง', classroom: 'ม.3/1' }
            ];
            
            showImportPreview();
        }

        // ฟังก์ชันแปลงข้อมูล CSV นักเรียน
        function parseStudentCSVData(csvText) {
            const lines = csvText.split('\n');
            const data = [];
            
            // ข้ามหัวข้อ (บรรทัดแรก)
            for (let i = 1; i < lines.length; i++) {
                const line = lines[i].trim();
                if (line) {
                    const columns = line.split(',');
                    if (columns.length >= 5) {
                        data.push({
                            number: columns[0].trim(),
                            firstName: columns[1].trim(),
                            lastName: columns[2].trim(),
                            nickname: columns[3].trim(),
                            classroom: columns[4].trim()
                        });
                    }
                }
            }
            
            if (data.length > 0) {
                importedStudentData = data;
                showStudentImportPreview();
            } else {
                alert('❌ ไม่พบข้อมูลในไฟล์ กรุณาตรวจสอบรูปแบบไฟล์');
            }
        }

        // ฟังก์ชันจำลองการนำเข้าไฟล์นักเรียน (สำหรับ Excel และ Word)
        function simulateStudentFileImport(fileType) {
            // ข้อมูลจำลอง
            importedStudentData = [
                { number: '11', firstName: 'อรุณ', lastName: 'สว่างใส', nickname: 'อรุณ', classroom: 'ม.3/1' },
                { number: '12', firstName: 'สุดา', lastName: 'ใจงาม', nickname: 'ดา', classroom: 'ม.3/1' },
                { number: '13', firstName: 'วิชัย', lastName: 'ชนะใจ', nickname: 'วิชัย', classroom: 'ม.3/2' },
                { number: '14', firstName: 'มาลี', lastName: 'หอมหวาน', nickname: 'มาลี', classroom: 'ม.3/2' },
                { number: '15', firstName: 'สมบัติ', lastName: 'รวยใจ', nickname: 'บัติ', classroom: 'ม.3/1' },
                { number: '16', firstName: 'นิรมล', lastName: 'บริสุทธิ์', nickname: 'นิรมล', classroom: 'ม.3/2' }
            ];
            
            showStudentImportPreview();
        }

        // ฟังก์ชันแสดงตัวอย่างข้อมูลที่จะนำเข้า
        function showImportPreview() {
            const previewTableBody = document.getElementById('previewTableBody');
            previewTableBody.innerHTML = '';
            
            importedData.forEach(student => {
                const row = document.createElement('tr');
                row.innerHTML = `
                    <td class="px-3 py-2">${student.number}</td>
                    <td class="px-3 py-2">${student.firstName}</td>
                    <td class="px-3 py-2">${student.lastName}</td>
                    <td class="px-3 py-2">${student.nickname}</td>
                    <td class="px-3 py-2">${student.classroom}</td>
                `;
                previewTableBody.appendChild(row);
            });
            
            document.getElementById('importResult').classList.remove('hidden');
        }

        // ฟังก์ชันยืนยันการนำเข้า
        function confirmImport() {
            if (importedData.length === 0) {
                alert('ไม่มีข้อมูลที่จะนำเข้า');
                return;
            }
            
            // ในระบบจริงจะบันทึกข้อมูลลงฐานข้อมูล
            alert(`นำเข้าข้อมูลนักเรียน ${importedData.length} คน เรียบร้อยแล้ว!`);
            
            // รีเซ็ตฟอร์ม
            cancelImport();
            document.getElementById('importFile').value = '';
            
            // รีเฟรชตารางรายชื่อ (ในระบบจริง)
            // refreshStudentTable();
        }

        // ฟังก์ชันยกเลิกการนำเข้า
        function cancelImport() {
            importedData = [];
            document.getElementById('importResult').classList.add('hidden');
        }

        // ฟังก์ชันแสดงตัวอย่างข้อมูลนักเรียนที่จะนำเข้า
        function showStudentImportPreview() {
            const previewTableBody = document.getElementById('studentPreviewTableBody');
            previewTableBody.innerHTML = '';
            
            importedStudentData.forEach(student => {
                const row = document.createElement('tr');
                row.className = 'border-b border-gray-200';
                row.innerHTML = `
                    <td class="px-3 py-2">${student.number}</td>
                    <td class="px-3 py-2">${student.firstName}</td>
                    <td class="px-3 py-2">${student.lastName}</td>
                    <td class="px-3 py-2">${student.nickname}</td>
                    <td class="px-3 py-2">${student.classroom}</td>
                `;
                previewTableBody.appendChild(row);
            });
            
            document.getElementById('studentImportResult').classList.remove('hidden');
        }

        // ฟังก์ชันยืนยันการนำเข้านักเรียน
        function confirmStudentImport() {
            if (importedStudentData.length === 0) {
                alert('❌ ไม่มีข้อมูลที่จะนำเข้า');
                return;
            }
            
            // ในระบบจริงจะบันทึกข้อมูลลงฐานข้อมูล
            alert(`✅ นำเข้าข้อมูลนักเรียน ${importedStudentData.length} คน เรียบร้อยแล้ว!\n\nข้อมูลที่นำเข้า:\n${importedStudentData.map(s => `- ${s.firstName} ${s.lastName} (${s.nickname}) ชั้น ${s.classroom}`).join('\n')}`);
            
            // รีเซ็ตฟอร์ม
            cancelStudentImport();
            document.getElementById('studentListFile').value = '';
            document.getElementById('selectedStudentFileName').classList.add('hidden');
            
            // รีเฟรชตารางรายชื่อ (ในระบบจริง)
            // refreshStudentTable();
        }

        // ฟังก์ชันยกเลิกการนำเข้านักเรียน
        function cancelStudentImport() {
            importedStudentData = [];
            document.getElementById('studentImportResult').classList.add('hidden');
        }

        // เริ่มต้นแสดงหน้าเลือกบทบาท
        showRoleSelection();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'96ef9ad0344f7dc3',t:'MTc1NTE2NTYyMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>

