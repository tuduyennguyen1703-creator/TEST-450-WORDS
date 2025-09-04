<TODUYENIELTS>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kiểm tra 200 từ vựng ToDuyenielts</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .tab-button.active {
            background-color: #3b82f6;
            color: white;
        }
        .hide {
            display: none;
        }
        button:disabled {
            opacity: 0.5;
            cursor: not-allowed;
        }
    </style>
</head>
<body class="bg-gray-100 text-gray-800 flex items-center justify-center min-h-screen">
    <div class="container mx-auto p-4 sm:p-6 lg:p-8 max-w-4xl">
        <div class="bg-white rounded-2xl shadow-xl overflow-hidden">
            <div class="p-6 bg-blue-600 text-white">
                <h1 class="text-3xl font-bold text-center">Bài kiểm tra 200 từ vựng</h1>
                <p class="text-center text-blue-200 mt-2">200 câu hỏi trong 20 phút</p>
            </div>

            <!-- Thanh điều hướng các cửa sổ -->
            <nav class="flex flex-wrap justify-center border-b border-gray-200 bg-gray-50">
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="name">1. Tên</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="quiz" disabled>2. Bài làm</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="result" disabled>3. Kết quả</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="answers" disabled>4. Đáp án</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="history">5. Lịch sử</button>
            </nav>

            <main class="p-6 sm:p-8">
                <!-- Cửa sổ 1: Nhập tên -->
                <div id="name" class="tab-content">
                    <h2 class="text-2xl font-semibold mb-4 text-center">Chào mừng bạn!</h2>
                    <p class="text-center text-gray-600 mb-6">Vui lòng nhập tên của bạn để bắt đầu bài kiểm tra.</p>
                    <div class="max-w-sm mx-auto">
                        <input type="text" id="username" placeholder="Nhập tên của bạn..." class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 transition">
                        <button id="startBtn" class="w-full mt-4 bg-blue-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-600 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50">Bắt đầu</button>
                    </div>
                </div>

                <!-- Cửa sổ 2: Bài làm -->
                <div id="quiz" class="tab-content hide">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-2xl font-semibold">Câu hỏi</h2>
                        <div id="timer" class="text-xl font-bold bg-blue-100 text-blue-700 px-4 py-2 rounded-lg">20:00</div>
                    </div>
                    <div id="quiz-container" class="space-y-6">
                        <!-- Các câu hỏi sẽ được chèn vào đây bởi JavaScript -->
                    </div>
                    <button id="submitBtn" class="w-full mt-8 bg-green-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-green-600 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-opacity-50">Nộp bài</button>
                </div>

                <!-- Cửa sổ 3: Kết quả -->
                <div id="result" class="tab-content hide text-center">
                    <h2 class="text-2xl font-semibold mb-4">Hoàn thành!</h2>
                    <div id="result-content" class="bg-gray-50 p-8 rounded-lg space-y-3 max-w-md mx-auto">
                        <!-- Nội dung kết quả sẽ được chèn vào đây -->
                    </div>
                     <button id="reviewAnswersBtn" class="mt-6 bg-purple-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-purple-600 transition-transform transform hover:scale-105">Xem đáp án</button>
                </div>

                <!-- Cửa sổ 4: Đáp án -->
                <div id="answers" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center">Đáp án chi tiết</h2>
                    <div id="answers-container" class="space-y-6">
                        <!-- Nội dung đáp án sẽ được chèn vào đây -->
                    </div>
                </div>

                <!-- Cửa sổ 5: Lịch sử -->
                <div id="history" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center">Lịch sử làm bài</h2>
                    <div id="history-container" class="overflow-x-auto">
                        <!-- Bảng lịch sử sẽ được chèn vào đây -->
                    </div>
                </div>
            </main>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const vocabularyCSV = `1,Tune,(v),/tjuːn/,"Theo dõi, điều chỉnh"
2,A 20-year wait,(phrase),-,Sự chờ đợi 20 năm
3,Renown,(n),/rɪˈnaʊn/,"Tiếng tăm, sự nổi danh"
4,Stall in,(v),/stɔːl ɪn/,"Dừng lại, chững lại"
5,Anonymous,(a),/əˈnɒnɪməs/,"Ẩn danh, vô danh"
6,Donor,(n),/ˈdəʊnə(r)/,"Người tài trợ, người tặng"
7,Be granted,(phrase),/bi ˈɡrɑːntɪd/,"Được cấp, được tài trợ"
8,Engagement,(n),/ɪnˈɡeɪdʒmənt/,"Sự tham gia, sự gắn kết; hôn ước"
9,Troupe,(n),/truːp/,"Đoàn (kịch, hát)"
10,Entitle,(v),/ɪnˈtaɪtl/,"Cho quyền, đặt tên cho"
11,Capacity of,(phrase),/kəˈpæsəti ɒv/,"Với tư cách là, khả năng của"
12,In executive roles,(phrase),/ɪn ɪɡˈzekjətɪv rəʊlz/,Trong vai trò quản lý/điều hành
13,Coworker,(n),/ˈkəʊwɜːkə(r)/,Đồng nghiệp
14,Discrepancy,(n),/dɪˈskrepənsi/,"Sự khác nhau, sự không nhất quán"
15,In the mean time,(phrase),/ɪn ðə miːn taɪm/,Trong khi chờ đợi
16,In the short term,(phrase),/ɪn ðə ʃɔːt tɜːm/,Trong thời gian ngắn
17,Auspicious,(a),/ɔːˈspɪʃəs/,"Có triển vọng, thuận lợi"
18,Initiative,(n),/ɪˈnɪʃətɪv/,"Sáng kiến, sự khởi đầu"
19,Launch,(v),/lɔːntʃ/,"Bắt đầu, khởi động"
20,Proceed,(v),/prəˈsiːd/,"Tiếp tục, tiến hành"
21,Tax,(n),/tæks/,Thuế
22,Revenue,(n),/ˈrevənjuː/,Doanh thu
23,Fine,(n),/faɪn/,Tiền phạt
24,Infrastructure,(n),/ˈɪnfrəstrʌktʃə(r)/,Cơ sở hạ tầng
25,Well-being,(n),/ˌwel ˈbiːɪŋ/,"Sức khỏe, hạnh phúc"
26,Attribute,(v),/əˈtrɪbjuːt/,"Quy cho, cho là do"
27,Telecommuting,(n),/ˈtelikəmjuːtɪŋ/,"Làm việc từ xa"
28,Poll,(n),/pəʊl/,Cuộc thăm dò ý kiến
29,Contradict,(v),/ˌkɒntrəˈdɪkt/,"Mâu thuẫn, trái với"
30,Contention,(n),/kənˈtenʃn/,"Sự tranh cãi, sự bất đồng"
31,Invaluable,(a),/ɪnˈvæljuəbl/,Vô giá
32,Outweigh,(v),/ˌaʊtˈweɪ/,"Vượt trội, có giá trị hơn"
33,Downside,(n),/ˈdaʊnsaɪd/,Mặt hạn chế
34,Resentment,(n),/rɪˈzentmənt/,"Sự oán giận, sự phẫn uất"
35,Commitment,(n),/kəˈmɪtmənt/,"Sự cam kết, sự tận tụy"
36,Conceal,(v),/kənˈsiːl/,"Che giấu, giấu diếm"
37,Predecessor,(n),/ˈpriːdɪsesə(r)/,Người tiền nhiệm
38,Standpoint,(n),/ˈstændpɔɪnt/,Quan điểm
39,Unprecedented,(a),/ʌnˈpresɪdentɪd/,Chưa từng có tiền lệ
40,Skepticism,(n),/ˈskeptɪsɪzəm/,"Thái độ hoài nghi"
41,Acclaim,(n),/əˈkleɪm/,"Sự hoan nghênh, sự ca ngợi"
42,Adversely,(adv),/ˈædvɜːsli/,Một cách bất lợi
43,Appealing,(a),/əˈpiːlɪŋ/,"Hấp dẫn, lôi cuốn"
44,Contemporary,(a),/kənˈtemprəri/,Đương đại
45,Disrupt,(v),/dɪsˈrʌpt/,"Làm gián đoạn, phá vỡ"
46,Haphazardly,(adv),/hæpˈhæzədli/,Một cách bừa bãi
47,Persistent,(a),/pəˈsɪstənt/,"Kiên trì, bền bỉ"
48,Valid,(a),/ˈvælɪd/,"Hợp lệ, có hiệu lực"
49,Withdraw,(v),/wɪðˈdrɔː/,"Rút lui, rút tiền"
50,Evident,(a),/ˈevɪdənt/,"Hiển nhiên, rõ ràng"
51,Come to a halt,(v),/kʌm tuː ə hɔːlt/,"Dừng lại, tạm ngưng"
52,Inadvertently,(adv),/ˌɪnədˈvɜːtəntli/,Một cách vô tình
53,To be set to,(v),/tuː biː set tuː/,"Sắp sửa, được dự định"
54,To be likely to,(v),/tuː biː ˈlaɪkli tuː/,Có khả năng
55,To be certain to,(v),/tuː biː ˈsɜːtn tuː/,Chắc chắn sẽ
56,To be sure to,(v),/tuː biː ʃʊə tuː/,Chắc chắn sẽ
57,To be bound to,(v),/tuː biː baʊnd tuː/,Chắc chắn sẽ
58,To be due to,(v),/tuː biː djuː tuː/,"Do, bởi"
59,To be supposed to,(v),/tuː biː səˈpəʊzd tuː/,"Được cho là, có nhiệm vụ"
60,To be meant to,(v),/tuː biː ment tuː/,Có ý định
61,To be obliged to,(v),/tuː biː əˈblaɪdʒd tuː/,"Bị buộc, có nghĩa vụ"
62,Advantageous,(a),/ˌædvənˈteɪdʒəs/,Thuận lợi
63,Ecology,(n),/iˈkɒlədʒi/,Sinh thái học
64,Elude,(v),/iˈluːd/,"Lẩn tránh, thoát khỏi"
65,Erode,(v),/ɪˈrəʊd/,"Xói mòn, ăn mòn"
66,Perpetuate,(v),/pəˈpetʃueɪt/,"Làm cho tồn tại mãi mãi"
67,Redundant,(a),/rɪˈdʌndənt/,"Thừa, dư"
68,Integrate,(v),/ˈɪntɪɡreɪt/,Hội nhập
69,Infer,(v),/ɪnˈfɜː(r)/,Suy ra
70,Confer,(v),/kənˈfɜː(r)/,"Bàn bạc, hội ý"
71,Cite,(v),/saɪt/,"Trích dẫn"
72,Imply,(v),/ɪmˈplaɪ/,Ám chỉ
73,Whereas,(conj),/weərˈæz/,Trong khi
74,Abide by,(v),/əˈbaɪd baɪ/,"Tuân theo, tôn trọng"
75,Cancel,(v),/ˈkænsəl/,Hủy bỏ
76,Determine,(v),/dɪˈtɜːmɪn/,Xác định
77,Engage,(v),/ɪnˈɡeɪdʒ/,"Tham gia, cam kết"
78,Establish,(v),/ɪˈstæblɪʃ/,Thành lập
79,Obligate,(v),/ˈɒblɪɡeɪt/,"Bắt buộc, ép buộc"
80,Provision,(n),/prəˈvɪʒn/,"Sự cung cấp, điều khoản"
81,Resolve,(v),/rɪˈzɒlv/,Giải quyết
82,Assurance,(n),/əˈʃʊərəns/,"Sự đảm bảo, sự chắc chắn"
83,Bargain,(n),/ˈbɑːɡən/,Sự mặc cả
84,Competition,(n),/ˌkɒmpəˈtɪʃn/,Sự cạnh tranh
85,Market,(n),/ˈmɑːkɪt/,Thị trường
86,Attract,(v),/əˈtrækt/,Thu hút
87,Compare,(v),/kəmˈpeə(r)/,So sánh
88,Consume,(v),/kənˈsjuːm/,Tiêu thụ
89,Convince,(v),/kənˈvɪns/,Thuyết phục
90,Fad,(n),/fæd/,"Mốt nhất thời, sự thích thú tạm thời"
91,Inspire,(v),/ɪnˈspaɪə(r)/,Truyền cảm hứng
92,Persuasion,(n),/pəˈsweɪʒn/,"Sự thuyết phục, sự tin tưởng"
93,Productive,(a),/prəˈdʌktɪv/,Năng suất
94,Satisfaction,(n),/ˌsætɪsˈfækʃn/,"Sự hài lòng, sự thỏa mãn"
95,Consequence,(n),/ˈkɒnsɪkwəns/,Hậu quả
96,Reputation,(n),/ˌrepjuˈteɪʃn/,"Danh tiếng, uy tín"
97,Require,(v),/rɪˈkwaɪə(r)/,Yêu cầu
98,Variety,(n),/vəˈraɪəti/,"Sự đa dạng, nhiều thứ"
99,Consider,(v),/kənˈsɪdə(r)/,Cân nhắc
100,Protect,(v),/prəˈtekt/,Bảo vệ
101,Gather,(v),/ˈɡæðə(r)/,Tập hợp
102,Offer,(v),/ˈɒfə(r)/,Đề nghị
103,Primarily,(adv),/ˈpraɪmərəli/,Chủ yếu
104,Strategy,(n),/ˈstrætədʒi/,Chiến lược
105,Substitution,(n),/ˌsʌbstɪˈtjuːʃn/,Sự thay thế
106,Demonstrate,(v),/ˈdemənstreɪt/,Chứng minh
107,Develop,(v),/dɪˈveləp/,Phát triển
108,Evaluate,(v),/ɪˈvæljueɪt/,Đánh giá
109,Predict,(v),/prɪˈdɪkt/,Dự đoán
110,Strong,(a),/strɒŋ/,Mạnh mẽ
111,Address,(n),/əˈdres/,Địa chỉ
112,Avoid,(v),/əˈvɔɪd/,Tránh
113,Effective,(a),/ɪˈfektɪv/,Hiệu quả
114,Present,(v),/prɪˈzent/,Trình bày
115,Solve,(v),/sɒlv/,Giải quyết
116,Appreciate,(v),/əˈpriːʃieɪt/,Đánh giá cao
117,Confident,(a),/ˈkɒnfɪdənt/,Tự tin
118,Frequently,(adv),/ˈfriːkwəntli/,Thường xuyên
119,Promise,(v),/ˈprɒmɪs/,Hứa
120,Accommodate,(v),/əˈkɒmədeɪt/,"Cung cấp, đáp ứng"
121,Arrangement,(n),/əˈreɪndʒmənt/,"Sự sắp xếp, sự dàn xếp"
122,Association,(n),/əˌsəʊʃiˈeɪʃn/,"Hiệp hội, sự liên kết"
123,Register,(v),/ˈredʒɪstə(r)/,Đăng ký
124,Select,(v),/sɪˈlekt/,Lựa chọn
125,Session,(n),/ˈseʃn/,Phiên họp
126,Take part in,(v),/teɪk pɑːt ɪn/,Tham gia
127,Access,(v),/ˈækses/,Truy cập
128,Allocate,(v),/ˈæləkeɪt/,Phân bổ
129,Compatible,(a),/kəmˈpætəbl/,Tương thích
130,Duplicate,(v),/ˈdjuːplɪkeɪt/,Sao chép
131,Failure,(n),/ˈfeɪljə(r)/,Thất bại
132,Figure out,(v),/ˈfɪɡə(r) aʊt/,Tìm ra
133,Ignore,(v),/ɪɡˈnɔː(r)/,Phớt lờ
134,Search,(v),/sɜːtʃ/,Tìm kiếm
135,Shut down,(v),/ʃʌt daʊn/,Tắt
136,Warning,(n),/ˈwɔːnɪŋ/,Cảnh báo
137,Affordable,(a),/əˈfɔːdəbl/,Giá cả phải chăng
138,Capacity,(n),/kəˈpæsəti/,"Sức chứa, năng lực"
139,Durable,(a),/ˈdjʊərəbl/,Bền
140,Initiate,(v),/ɪˈnɪʃieɪt/,Khởi xướng
141,Physically,(adv),/ˈfɪzɪkli/,Thể chất
142,Provider,(n),/prəˈvaɪdə(r)/,Nhà cung cấp
143,Recur,(v),/rɪˈkɜː(r)/,Tái diễn
144,Reduction,(n),/rɪˈdʌkʃn/,Sự giảm bớt
145,Stay on top of,(v),/steɪ ɒn tɒp ɒv/,Nắm bắt
146,Stock,(n),/stɒk/,Hàng tồn kho
147,Appreciation,(n),/əˌpriːʃiˈeɪʃn/,"Sự đánh giá cao, sự cảm kích"
148,Bring in,(v),/brɪŋ ɪn/,Thuê
149,Casually,(adv),/ˈkæʒuəli/,Tình cờ
150,Code,(n),/kəʊd/,Quy tắc
151,Expose,(v),/ɪkˈspəʊz/,Phơi bày
152,Glimpse,(n),/ɡlɪmps/,"Cái nhìn thoáng qua"
153,Out of,(a),/aʊt ɒv/,Hết
154,Outdated,(a),/ˌaʊtˈdeɪtɪd/,Lỗi thời
155,Practice,(n),/ˈpræktɪs/,Thực hành
156,Reinforce,(v),/ˌriːɪnˈfɔːs/,Củng cố
157,Verbally,(adv),/ˈvɜːbəli/,Bằng lời nói
158,Disk,(n),/dɪsk/,Đĩa
159,Facilitate,(v),/fəˈsɪlɪteɪt/,Tạo điều kiện
160,Network,(v),/ˈnetwɜːk/,Kết nối
161,Popularity,(n),/ˌpɒpjuˈlærəti/,"Sự nổi tiếng, sự phổ biến"
162,Process,(n),/ˈprəʊses/,Quá trình
163,Replace,(v),/rɪˈpleɪs/,Thay thế
164,Revolution,(n),/ˌrevəˈluːʃn/,Cuộc cách mạng
165,Sharp,(a),/ʃɑːp/,Sắc bén
166,Skill,(n),/skɪl/,Kỹ năng
167,Software,(n),/ˈsɒftweə(r)/,Phần mềm
168,Store,(v),/stɔː(r)/,Lưu trữ
169,Technically,(adv),/ˈteknɪkli/,Về mặt kỹ thuật
170,Assemble,(v),/əˈsembl/,Lắp ráp
171,Beforehand,(adv),/bɪˈfɔːhænd/,Trước
172,Complicated,(a),/ˈkɒmplɪkeɪtɪd/,Phức tạp
173,Courier,(n),/ˈkʊriə(r)/,Người đưa thư
174,Express,(a),/ɪkˈspres/,Nhanh
175,Fold,(v),/fəʊld/,Gấp
176,Layout,(n),/ˈleɪaʊt/,Bố cục
177,Mention,(v),/ˈmenʃn/,Đề cập
178,Petition,(n),/pəˈtɪʃn/,Đơn kiến nghị
179,Proof,(v),/pruːf/,Bằng chứng
180,Registered,(a),/ˈredʒɪstəd/,Đã đăng ký
181,Revise,(v),/rɪˈvaɪz/,Sửa đổi
182,Abundant,(a),/əˈbʌndənt/,Dồi dào
183,Accomplishment,(n),/əˈkʌmplɪʃmənt/,Thành tựu
184,Bring together,(v),/brɪŋ təˈɡeðə(r)/,Gắn kết
185,Candidate,(n),/ˈkændɪdət/,Ứng cử viên
186,Come up with,(v),/kʌm ʌp wɪð/,Nghĩ ra
187,Commensurate,(a),/kəˈmenʃərət/,Tương xứng
188,Match,(n),/mætʃ/,Sự phù hợp
189,Profile,(n),/ˈprəʊfaɪl/,Hồ sơ
190,Qualification,(n),/ˌkwɒlɪfɪˈkeɪʃn/,Bằng cấp
191,Recruit,(v),/rɪˈkruːt/,Tuyển dụng
192,Submit,(v),/səbˈmɪt/,Nộp
193,Time-consuming,(a),/ˈtaɪm kənsjuːmɪŋ/,Tốn thời gian
194,Ability,(n),/əˈbɪləti/,Khả năng
195,Apply,(v),/əˈplaɪ/,Nộp đơn
196,Background,(n),/ˈbækɡraʊnd/,Lý lịch
197,Be ready for,(v),/biː ˈredi fɔː(r)/,Sẵn sàng cho
198,Call in,(v),/kɔːl ɪn/,Gọi đến
199,Constantly,(adv),/ˈkɒnstəntli/,Liên tục
200,Expert,(n),/ˈekspɜːt/,Chuyên gia`;

            let allVocab = [];
            let quizData = []; // Will be populated dynamically

            function parseCSV(csv) {
                const lines = csv.split('\n');
                const vocab = [];
                for (const line of lines) {
                    const parts = line.split(',');
                    if (parts.length >= 5) {
                        const word = parts[1].trim();
                        // The definition might contain commas, so we join the rest.
                        const definition = parts.slice(4).join(',').trim().replace(/^"|"$/g, '');
                        if (word && definition) {
                            vocab.push({ word, definition });
                        }
                    }
                }
                return vocab;
            }

            function generateRandomQuiz(count = 10) {
                const shuffledVocab = [...allVocab].sort(() => 0.5 - Math.random());
                const selectedWords = shuffledVocab.slice(0, count);
                
                quizData = selectedWords.map(correctWord => {
                    const question = `Đâu là nghĩa của từ: <strong>"${correctWord.word}"</strong>?`;
                    const answer = correctWord.definition;
                    
                    let wrongOptions = [];
                    while(wrongOptions.length < 3) {
                        const randomWord = allVocab[Math.floor(Math.random() * allVocab.length)];
                        if (randomWord.definition !== answer && !wrongOptions.includes(randomWord.definition)) {
                            wrongOptions.push(randomWord.definition);
                        }
                    }

                    const options = [answer, ...wrongOptions].sort(() => 0.5 - Math.random());
                    
                    return {
                        word: correctWord.word,
                        question: question,
                        options: options,
                        answer: answer
                    };
                });
            }

            const tabs = document.querySelectorAll('.tab-button');
            const tabContents = document.querySelectorAll('.tab-content');
            const startBtn = document.getElementById('startBtn');
            const submitBtn = document.getElementById('submitBtn');
            const usernameInput = document.getElementById('username');
            const quizContainer = document.getElementById('quiz-container');
            const answersContainer = document.getElementById('answers-container');
            const historyContainer = document.getElementById('history-container');
            const resultContent = document.getElementById('result-content');
            const reviewAnswersBtn = document.getElementById('reviewAnswersBtn');
            
            let timerInterval;
            let currentUsername = '';
            let userAnswers = {};

            function showTab(tabId) {
                tabContents.forEach(content => content.classList.add('hide'));
                document.getElementById(tabId).classList.remove('hide');

                tabs.forEach(tab => {
                    if (tab.dataset.tab === tabId && !tab.disabled) {
                        tab.classList.add('active');
                    } else {
                        tab.classList.remove('active');
                    }
                });
            }

            tabs.forEach(tab => {
                tab.addEventListener('click', () => {
                    if (!tab.disabled) {
                        showTab(tab.dataset.tab);
                    }
                });
            });

            function loadQuiz() {
                quizContainer.innerHTML = '';
                quizData.forEach((q, index) => {
                    const questionElement = document.createElement('div');
                    questionElement.className = 'bg-gray-50 p-5 rounded-lg border border-gray-200';
                    questionElement.innerHTML = `
                        <p class="font-semibold text-lg mb-4">${index + 1}. ${q.question}</p>
                        <div class="space-y-2">
                            ${q.options.map((option, i) => `
                                <label class="flex items-center p-3 rounded-lg border border-gray-200 hover:bg-blue-100 cursor-pointer transition">
                                    <input type="radio" name="question${index}" value="${option}" class="mr-3">
                                    <span>${option}</span>
                                </label>
                            `).join('')}
                        </div>
                    `;
                    quizContainer.appendChild(questionElement);
                });
            }

            function startTimer() {
                let timeLeft = 20 * 60; // 20 minutes
                const timerElement = document.getElementById('timer');

                timerInterval = setInterval(() => {
                    timeLeft--;
                    const minutes = Math.floor(timeLeft / 60);
                    const seconds = timeLeft % 60;
                    timerElement.textContent = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

                    if (timeLeft <= 0) {
                        clearInterval(timerInterval);
                        submitQuiz();
                    }
                }, 1000);
            }

            function submitQuiz() {
                clearInterval(timerInterval);
                submitBtn.disabled = true;
                let score = 0;
                userAnswers = {};

                quizData.forEach((q, index) => {
                    const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                    const selectedValue = selectedOption ? selectedOption.value : null;
                    userAnswers[index] = selectedValue;
                    if (selectedValue && selectedValue === q.answer) {
                        score++;
                    }
                });

                const result = {
                    name: currentUsername,
                    score: score,
                    total: quizData.length,
                    date: new Date().toLocaleString('vi-VN')
                };

                resultContent.innerHTML = `
                    <p class="text-lg"><span class="font-semibold">Tên:</span> ${result.name}</p>
                    <p class="text-3xl font-bold my-4 ${score / result.total > 0.5 ? 'text-green-600' : 'text-red-600'}">
                        ${result.score} / ${result.total}
                    </p>
                    <p class="text-gray-500">Ngày làm: ${result.date}</p>
                `;
                
                saveResult(result);
                enableTabsAfterTest();
                loadAnswers();
                loadHistory();
                showTab('result');
            }

            function saveResult(result) {
                let history = JSON.parse(localStorage.getItem('vocabTestHistory')) || [];
                history.unshift(result);
                localStorage.setItem('vocabTestHistory', JSON.stringify(history));
            }

            function loadHistory() {
                let history = JSON.parse(localStorage.getItem('vocabTestHistory')) || [];
                if (history.length === 0) {
                    historyContainer.innerHTML = '<p class="text-center text-gray-500">Chưa có lịch sử làm bài.</p>';
                    return;
                }

                historyContainer.innerHTML = `
                    <table class="min-w-full bg-white border border-gray-200 rounded-lg">
                        <thead class="bg-gray-50">
                            <tr>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Tên</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Điểm số</th>
                                <th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Ngày</th>
                            </tr>
                        </thead>
                        <tbody class="divide-y divide-gray-200">
                            ${history.map(item => `
                                <tr>
                                    <td class="px-6 py-4 whitespace-nowrap">${item.name}</td>
                                    <td class="px-6 py-4 whitespace-nowrap font-semibold">${item.score} / ${item.total}</td>
                                    <td class="px-6 py-4 whitespace-nowrap">${item.date}</td>
                                </tr>
                            `).join('')}
                        </tbody>
                    </table>
                `;
            }

            function loadAnswers() {
                answersContainer.innerHTML = '';
                 quizData.forEach((q, index) => {
                    const userAnswer = userAnswers[index];
                    const isCorrect = userAnswer === q.answer;
                    
                    let resultHtml;
                    if (userAnswer === null) {
                        resultHtml = `<p class="text-sm font-medium text-yellow-600">Bạn chưa trả lời</p>`;
                    } else if (isCorrect) {
                        resultHtml = `<p class="text-sm font-medium text-green-600">Bạn đã chọn đúng: ${userAnswer}</p>`;
                    } else {
                        resultHtml = `<p class="text-sm font-medium text-red-600">Bạn đã chọn sai: ${userAnswer}</p>`;
                    }

                    const answerElement = document.createElement('div');
                    answerElement.className = 'bg-gray-50 p-5 rounded-lg border border-gray-200';
                    answerElement.innerHTML = `
                        <p class="font-semibold text-lg mb-2">${index + 1}. ${q.question}</p>
                        <p class="text-sm text-gray-700 mb-2"><strong>Từ vựng:</strong> ${q.word}</p>
                        ${resultHtml}
                        <p class="text-sm font-medium text-blue-600 mt-2">Đáp án đúng: ${q.answer}</p>
                    `;
                    answersContainer.appendChild(answerElement);
                });
            }

            function enableTabsAfterTest() {
                document.querySelector('button[data-tab="result"]').disabled = false;
                document.querySelector('button[data-tab="answers"]').disabled = false;
            }

            startBtn.addEventListener('click', () => {
                currentUsername = usernameInput.value.trim();
                if (currentUsername) {
                    startBtn.disabled = true;
                    document.querySelector('button[data-tab="quiz"]').disabled = false;
                    
                    generateRandomQuiz(200);
                    loadQuiz();
                    
                    showTab('quiz');
                    startTimer();
                } else {
                    alert('Vui lòng nhập tên của bạn!');
                }
            });

            submitBtn.addEventListener('click', () => {
                 if (confirm('Bạn có chắc chắn muốn nộp bài không?')) {
                    submitQuiz();
                }
            });
            
            reviewAnswersBtn.addEventListener('click', () => showTab('answers'));

            // Initial setup
            allVocab = parseCSV(vocabularyCSV);
            showTab('name');
            loadHistory();
        });
    </script>
</body>
</html>

