<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToDuyenIELTS - Kiểm tra 150 từ vựng</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .tab-button.active {
            background-color: #3b82f6;
            color: white;
            border-bottom-color: transparent;
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
                <h2 class="text-center text-lg font-semibold text-blue-200">ToDuyenIELTS</h2>
                <h1 class="text-3xl font-bold text-center mt-1">Bài kiểm tra 150 từ vựng</h1>
                <p class="text-center text-blue-200 mt-2">150 câu hỏi trong 20 phút</p>
            </div>

            <nav class="flex flex-wrap justify-center border-b border-gray-200 bg-gray-50">
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="name">1. Tên</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="quiz" disabled>2. Bài làm</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="result" disabled>3. Kết quả</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="answers" disabled>4. Đáp án</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100 transition-colors duration-300" data-tab="history">5. Lịch sử</button>
            </nav>

            <main class="p-6 sm:p-8">
                <div id="name" class="tab-content">
                    <h2 class="text-2xl font-semibold mb-4 text-center text-blue-800">Chào mừng bạn!</h2>
                    <p class="text-center text-gray-700 mb-6">Vui lòng nhập tên của bạn để bắt đầu bài kiểm tra.</p>
                    <div class="max-w-sm mx-auto">
                        <input type="text" id="username" placeholder="Nhập tên của bạn..." class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500 transition">
                        <button id="startBtn" class="w-full mt-4 bg-blue-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-600 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-opacity-50">Bắt đầu</button>
                    </div>
                </div>

                <div id="quiz" class="tab-content hide">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-2xl font-semibold text-blue-800">Câu hỏi</h2>
                        <div id="timer" class="text-xl font-bold bg-blue-100 text-blue-700 px-4 py-2 rounded-lg">20:00</div>
                    </div>
                    <div id="quiz-container" class="space-y-6">
                        </div>
                    <button id="submitBtn" class="w-full mt-8 bg-green-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-green-600 transition-transform transform hover:scale-105 focus:outline-none focus:ring-2 focus:ring-green-500 focus:ring-opacity-50">Nộp bài</button>
                </div>

                <div id="result" class="tab-content hide text-center">
                    <h2 class="text-2xl font-semibold mb-4 text-blue-800">Hoàn thành!</h2>
                    <div id="result-content" class="bg-gray-50 p-8 rounded-lg space-y-3 max-w-md mx-auto">
                        </div>
                    <div class="mt-6 flex flex-col sm:flex-row justify-center items-center gap-4">
                        <button id="retakeBtn" class="w-full sm:w-auto bg-blue-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-blue-600 transition-transform transform hover:scale-105">Làm lại</button>
                        <button id="reviewAnswersBtn" class="w-full sm:w-auto bg-purple-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-purple-600 transition-transform transform hover:scale-105">Xem đáp án</button>
                        <button id="exportBtn" class="w-full sm:w-auto bg-gray-700 text-white font-bold py-3 px-6 rounded-lg hover:bg-gray-800 transition-transform transform hover:scale-105">Lưu & Xuất kết quả</button>
                    </div>
                </div>

                <div id="answers" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center text-blue-800">Đáp án chi tiết</h2>
                    <div id="answers-container" class="space-y-4">
                        </div>
                </div>

                <div id="history" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center text-blue-800">Lịch sử làm bài</h2>
                    <div id="history-container" class="overflow-x-auto">
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
15,Token,(a),/ˈtəʊkən/,Tượng trưng
16,Well-deserved roles,(phrase),/ˌwel dɪˈzɜːvd rəʊlz/,Vai trò xứng đáng
17,The relevance of,(phrase),/ðə ˈreləvəns ɒv/,Sự liên quan của
18,Tangible,(a),/ˈtændʒəbl/,Hữu hình
19,Intangible,(a),/ɪnˈtændʒəbl/,Vô hình
20,Underlie,(v),/ˌʌndəˈlaɪ/,"Nằm dưới, làm nền tảng cho"
21,Stigma,(n),/ˈstɪɡmə/,Sự kỳ thị
22,Professionalism,(n),/prəˈfeʃənəlɪzəm/,Tính chuyên nghiệp
23,agrarian,(adj),/əˈɡreəriən/,(thuộc về) nông nghiệp
24,manufacturing techniques,(phrase),/ˌmænjuˈfæktʃərɪŋ tekˈniːks/,Kỹ thuật sản xuất/chế tạo
25,in mass quantities,(phrase),/ɪn mæs ˈkwɒntətiz/,Với số lượng lớn
26,pump,"(v, n)",/pʌmp/,Bơm; máy bơm
27,adapt,(v),/əˈdæpt/,"Thích nghi, điều chỉnh"
28,the forward and backward,(phrase),/ðə ˈfɔːwəd ænd ˈbækwəd/,Chuyển động tới lui
29,the gear mechanism,(phrase),/ðə ɡɪə ˈmekənɪzəm/,Cơ cấu/cơ chế bánh răng
30,rotary motion,(phrase),/ˈrəʊtəri ˈməʊʃn/,Chuyển động quay tròn
31,relatively,(adv),/ˈrelətɪvli/,Tương đối
32,locomotive,(n),/ˌləʊkəˈməʊtɪv/,Đầu máy (xe lửa)
33,spinner,(n),/ˈspɪnə(r)/,Thợ kéo sợi; máy kéo sợi
34,weaver,(n),/ˈwiːvə(r)/,Thợ dệt
35,thread,(n),/θred/,"Sợi chỉ, sợi tơ"
36,mechanise (mechanize),(v),/ˈmekənaɪz/,Cơ giới hóa
37,undergo,(v),/ˌʌndəˈɡəʊ/,"Trải qua, chịu đựng"
38,adopt,(v),/əˈdɒpt/,"Áp dụng, chấp nhận"
39,chief,(adj),/tʃiːf/,"Chính, chủ yếu, hàng đầu"
40,iron ore,(n),/ˈaɪən ɔː(r)/,Quặng sắt
41,charcoal,(n),/ˈtʃɑːkəʊl/,"Than củi, than gỗ"
42,metals,(n),/ˈmetlz/,Kim loại
43,enable,(v),/ɪˈneɪbl/,"Cho phép, làm cho có thể"
44,steel,(n),/stiːl/,Thép
45,in response to,(phrase),/ɪn rɪˈspɒns tu/,Để đáp lại
46,communication,(n),/kəˌmjuːnɪˈkeɪʃn/,"Sự giao tiếp, truyền thông"
47,communicate,(v),/kəˈmjuːnɪkeɪt/,"Giao tiếp, truyền đạt"
48,immense,(adj),/ɪˈmens/,"To lớn, mênh mông, bao la"
49,rural areas,(phrase),/ˈrʊərəl ˈeəriəz/,Vùng nông thôn
50,accelerate,(v),/əkˈseləreɪt/,"Tăng tốc, thúc đẩy"
51,dramatically,(adv),/drəˈmætɪkli/,"Một cách đáng kể, đột ngột"
52,inadequate,(adj),/ɪnˈædɪkwət/,"Không đủ, thiếu"
53,sanitation,(n),/ˌsænɪˈteɪʃn/,Hệ thống vệ sinh
54,the middle and upper classes,(phrase),-,Tầng lớp trung lưu và thượng lưu
55,struggle,"(v, n)",/ˈstrʌɡl/,Đấu tranh; cuộc đấu tranh
56,along with,(phrase),/əˈlɒŋ wɪð/,Cùng với
57,the pace of,(phrase),/ðə peɪs ɒv/,Nhịp độ của
58,fuel,(v),/ˈfjuːəl/,"Thúc đẩy, tiếp nhiên liệu"
59,opposition,(n),/ˌɒpəˈzɪʃn/,Sự phản đối
60,industrialisation,(n),/ɪnˌdʌstriəlaɪˈzeɪʃn/,Sự công nghiệp hóa
61,textile,"(n, adj)",/ˈtekstaɪl/,"Vải dệt, hàng dệt; (thuộc) ngành dệt"
62,object to,(v),/əbˈdʒekt tu/,Phản đối
63,mechanised looms,(phrase),/ˈmekənaɪzd luːmz/,Khung cửi cơ giới hóa
64,knitting frames,(phrase),/ˈnɪtɪŋ freɪmz/,Khung dệt kim
65,craft,(n),/krɑːft/,Nghề thủ công
66,livelihood,(n),/ˈlaɪvlihʊd/,Kế sinh nhai
67,rob,(v),/rɒb/,"Cướp, tước đoạt"
68,desperate,(adj),/ˈdespərət/,"Tuyệt vọng, liều lĩnh"
69,smash,(v),/smæʃ/,Đập tan
70,apprentice,(n),/əˈprentɪs/,Người học việc
71,rumour (rumor),(n),/ˈruːmə(r)/,Tin đồn
72,wreck,(v),/rek/,"Phá hủy, làm hỏng"
73,take place,(phrase),/teɪk pleɪs/,"Diễn ra, xảy ra"
74,spread across,(phrase),/spred əˈkrɒs/,Lan rộng khắp
75,attack,"(v, n)",/əˈtæk/,Tấn công; cuộc tấn công
76,exchange,"(n, v)",/ɪksˈtʃeɪndʒ/,Sự trao đổi; trao đổi (khi đi với gunfire nghĩa là cuộc đấu súng)
77,gunfire,(n),/ˈɡʌnfaɪə(r)/,"Tiếng súng, cuộc đấu súng"
78,guard,"(n, v)",/ɡɑːd/,"Lính gác, người bảo vệ; canh gác"
79,soldier,(n),/ˈsəʊldʒə(r)/,Người lính
80,punishable,(adj),/ˈpʌnɪʃəbl/,"Có thể bị trừng phạt, đáng bị phạt"
81,unrest,(n),/ʌnˈrest/,"Tình trạng bất ổn, náo động"
82,mill,(n),/mɪl/,"Nhà máy (dệt, xay xát), xưởng"
83,in the days that followed,(phrase),-,Trong những ngày tiếp theo
84,arrest,"(v, n)",/əˈrest/,Bắt giữ; vụ bắt giữ
85,resistance,(n),/rɪˈzɪstəns/,"Sự kháng cự, sự chống cự"
86,vanish,(v),/ˈvænɪʃ/,"Biến mất, tan biến"
87,Brick by brick,(phrase),/brɪk baɪ brɪk/,"Từng viên gạch một, từ từ và kiên định"
88,magical,(adj),/ˈmædʒɪkl/,"Kì diệu, có phép thuật"
89,fairy-tale,(n),/ˈfeəri teɪl/,Truyện cổ tích
90,turret,(n),/ˈtʌrɪt/,Tháp nhỏ (trên lâu đài)
91,fire-breathing,(adj),/ˈfaɪə briːðɪŋ/,Phun ra lửa
92,wicked,(adj),/ˈwɪkɪd/,"Xấu xa, độc ác"
93,witch,(n),/wɪtʃ/,Phù thủy
94,gallant,(adj),/ˈɡælənt/,"Dũng cảm, hào hiệp"
95,enchant,(v),/ɪnˈtʃɑːnt/,"Bỏ bùa, làm say mê"
96,be aware of,(phrase),/bi əˈweər ɒv/,"Nhận thức về, ý thức về"
97,fantasy,(n),/ˈfæntəsi/,"Sự tưởng tượng, ảo mộng"
98,repercussion,(n),/ˌriːpəˈkʌʃn/,"Hậu quả, ảnh hưởng (thường là tiêu cực)"
99,abandon,(v),/əˈbændən/,"Từ bỏ, ruồng bỏ"
100,pretence (pretense),(n),/prɪˈtens/,"Sự giả vờ, giả bộ"
101,tire,(v),/ˈtaɪə(r)/,"Làm cho mệt mỏi, trở nên mệt mỏi"
102,settle down,(phr v),/ˈsetl daʊn/,Ổn định cuộc sống
103,take turns with,(phrase),/teɪk tɜːnz wɪð/,Thay phiên nhau
104,faculty,(n),/ˈfæklti/,"Khả năng, năng lực (trí tuệ, thể chất)"
105,underpin,(v),/ˌʌndəˈpɪn/,"Làm nền tảng, củng cố"
106,problem-solving,(n),/ˈprɒbləm sɒlvɪŋ/,Việc giải quyết vấn đề
107,adaptable,(adj),/əˈdæptəbl/,Dễ thích nghi
108,millennia,(n),/mɪˈleniə/,Thiên niên kỷ
109,philosopher,(n),/fəˈlɒsəfə(r)/,Nhà triết học
110,extoll (extol),(v),/ɪkˈstəʊl/,"Tán dương, ca tụng"
111,virtue,(n),/ˈvɜːtʃuː/,"Đức tính tốt, đức hạnh"
112,play-based learning,(phrase),/pleɪ beɪst ˈlɜːnɪŋ/,Học tập thông qua trò chơi
113,increasingly,(adv),/ɪnˈkriːsɪŋli/,Ngày càng
114,scarce,(adj),/skeəs/,Khan hiếm
115,curtail,(v),/kəˈteɪl/,"Cắt giảm, hạn chế"
116,victim,(n),/ˈvɪktɪm/,Nạn nhân
117,competition,(n),/ˌkɒmpəˈtɪʃn/,"Sự cạnh tranh, cuộc thi"
118,concern,(n),/kənˈsɜːn/,"Mối quan tâm, sự lo lắng"
119,implication,(n),/ˌɪmplɪˈkeɪʃn/,"Hàm ý, ảnh hưởng"
120,child-initiated,(adj),/tʃaɪld ɪˈnɪʃieɪtɪd/,Do trẻ em khởi xướng
121,spontaneous,(adj),/spɒnˈteɪniəs/,"Tự phát, tự nhiên"
122,unpredictable,(adj),/ˌʌnprɪˈdɪktəbl/,Không thể đoán trước
123,intervene,(v),/ˌɪntəˈviːn/,Can thiệp
124,puzzle,(n),/ˈpʌzl/,"Câu đố, trò chơi xếp hình"
125,possibility,(n),/ˌpɒsəˈbɪləti/,Khả năng (có thể xảy ra)
126,awareness,(n),/əˈweənəs/,Sự nhận thức
127,undertake,(v),/ˌʌndəˈteɪk/,"Đảm nhận, thực hiện"
128,carry out,(phr v),/ˈkæri aʊt/,"Tiến hành, thực hiện"
129,pre-schooler,(n),/ˈpriː skuːlə(r)/,Trẻ mẫu giáo
130,unfamiliar,(adj),/ˌʌnfəˈmɪliə(r)/,Không quen thuộc
131,requiring scientific reasoning,(phrase),-,Đòi hỏi sự lập luận khoa học
132,facilitate,(v),/fəˈsɪlɪteɪt/,"Tạo điều kiện, làm cho dễ dàng hơn"
133,extremely,(adv),/ɪkˈstriːmli/,"Cực kỳ, vô cùng"
134,self-regulate,(v),/self ˈreɡjuleɪt/,Tự điều chỉnh
135,indicator,(n),/ˈɪndɪkeɪtə(r)/,"Chỉ số, dấu hiệu"
136,investigate,(v),/ɪnˈvestɪɡeɪt/,Điều tra
137,observe,(v),/əbˈzɜːv/,Quan sát
138,diagnosis,(n),/ˌdaɪəɡˈnəʊsɪs/,Sự chẩn đoán
139,neurodevelopmental disorder,(phrase),-,Rối loạn phát triển thần kinh
140,play-based approach,(phrase),-,Phương pháp tiếp cận dựa trên trò chơi
141,stimulus,(n),/ˈstɪmjələs/,Sự kích thích
142,playful,(adj),/ˈpleɪfl/,"Vui tươi, ham chơi"
143,comment,"(n, v)",/ˈkɒment/,Lời bình luận; bình luận
144,backwater,(n),/ˈbækwɔːtə(r)/,"Nơi tù túng, hẻo lánh, kém phát triển"
145,untroubled,(adj),/ʌnˈtrʌbld/,"Yên bình, không bị làm phiền"
146,debate,"(n, v)",/dɪˈbeɪt/,Cuộc tranh luận; tranh luận
147,trivial,(adj),/ˈtrɪviəl/,"Tầm thường, không quan trọng"
148,contrast,"(n, v)","/ˈkɒntrɑːst/, /kənˈtrɑːst/",Sự tương phản; làm tương phản
149,bike-sharing scheme,(phrase),/baɪk ˈʃeərɪŋ skiːm/,Kế hoạch/hệ thống chia sẻ xe đạp
150,come up with,(phr v),/kʌm ʌp wɪð/,"Nghĩ ra, nảy ra (ý tưởng)"
151,perceive,(v),/pəˈsiːv/,"Nhận thức, xem xét"
152,thread of,(phrase),/θred ɒv/,"Mạch (suy nghĩ), dòng (sự kiện)"
153,consumerism,(n),/kənˈsjuːmərɪzəm/,Chủ nghĩa tiêu dùng
154,paint,(v),/peɪnt/,"Sơn, vẽ"
155,distribute,(v),/dɪˈstrɪbjuːt/,Phân phát
156,leaflet,(n),/ˈliːflət/,Tờ rơi
157,heavily,(adv),/ˈhevɪli/,"Nặng nề, rất nhiều"
158,recall,(v),/rɪˈkɔːl/,"Nhớ lại, gọi về"
159,particularly,(adv),/pəˈtɪkjələli/,Đặc biệt là
160,publicise (publicize),(v),/ˈpʌblɪsaɪz/,"Công khai, quảng bá"
161,symbolic,(adj),/sɪmˈbɒlɪk/,Tượng trưng
162,seize the opportunity to,(phrase),-,Nắm bắt cơ hội để
163,elaborate,"(v, adj)","/ɪˈlæbəreɪt/, /ɪˈlæbərət/","Diễn giải chi tiết; tỉ mỉ, phức tạp"
164,municipality,(n),/mjuːˌnɪsɪˈpæləti/,"Chính quyền thành phố, đô thị"
165,calculations,(n),/ˌkælkjuˈleɪʃnz/,Sự tính toán
166,turned out,(phr v),/tɜːnd aʊt/,"Hóa ra, thành ra"
167,unanimously,(adv),/juˈnænɪməsli/,"Nhất trí, đồng lòng"
168,reject,(v),/rɪˈdʒekt/,"Bác bỏ, từ chối"
169,belong to,(phr v),/bɪˈlɒŋ tu/,Thuộc về
170,glorious,(adj),/ˈɡlɔːriəs/,"Huy hoàng, rực rỡ"
171,discourage,(v),/dɪsˈkʌrɪdʒ/,Làm nản lòng
172,ask for,(phr v),/ɑːsk fɔː(r)/,"Yêu cầu, xin"
173,deposit,"(n, v)",/dɪˈpɒzɪt/,Tiền đặt cọc; đặt cọc
174,drop,(v),/drɒp/,"Rơi, thả; từ bỏ (kế hoạch)"
175,conscious,(adj),/ˈkɒnʃəs/,"Có ý thức, nhận biết được"
176,prove,(v),/pruːv/,Chứng minh
177,launch,(v),/lɔːntʃ/,"Ra mắt, khởi động, tung ra"
178,no longer,(phrase),/nəʊ ˈlɒŋɡə(r)/,Không còn nữa
179,guilder,(n),/ˈɡɪldə(r)/,Đồng Guilder (tiền Hà Lan cũ)
180,conspicuous,(adj),/kənˈspɪkjuəs/,"Dễ thấy, nổi bật"
181,sturdy,(adj),/ˈstɜːdi/,"Cứng cáp, vững chắc"
182,rack,(n),/ræk/,"Giá, kệ (để đồ)"
183,the chip card,(phrase),/ðə tʃɪp kɑːd/,Thẻ chip
184,the bike rack,(phrase),/ðə baɪk ræk/,Giá để xe đạp
185,prone,(adj),/prəʊn/,"Dễ bị, có khuynh hướng bị (điều gì xấu)"
186,vandalism,(n),/ˈvændəlɪzəm/,Hành vi phá hoại của công
187,theft,(n),/θeft/,Sự trộm cắp
188,instantly,(adv),/ˈɪnstəntli/,Ngay lập tức
189,recognise (recognize),(v),/ˈrekəɡnaɪz/,Nhận ra
190,blow,(n),/bləʊ/,"Cú giáng, cú sốc"
191,abolish,(v),/əˈbɒlɪʃ/,"Bãi bỏ, hủy bỏ"
192,profitable,(adj),/ˈprɒfɪtəbl/,Có lợi nhuận
193,pivotal,(adj),/ˈpɪvətl/,"Then chốt, chủ chốt"
194,disappoint,(v),/ˌdɪsəˈpɔɪnt/,Làm thất vọng
195,corporation,(n),/ˌkɔːpəˈreɪʃn/,"Tập đoàn, công ty lớn"
196,boast,(v),/bəʊst/,"Khoe khoang, tự hào về"
197,inspire,(v),/ɪnˈspaɪə(r)/,Truyền cảm hứng
198,set up,(phr v),/set ʌp/,"Thành lập, thiết lập"
199,financially,(adv),/faɪˈnænʃəli/,Về mặt tài chính
200,file,(v),/faɪl/,"Nộp (đơn), đệ trình"
201,patent,"(n, v)",/ˈpætnt/,Bằng sáng chế; cấp bằng sáng chế
202,regard,"(v, n)",/rɪˈɡɑːd/,"Coi như, xem như; sự quan tâm"
203,underground,"(adj, n)",/ˈʌndəɡraʊnd/,Dưới lòng đất; ngầm
204,destination,(n),/ˌdestɪˈneɪʃn/,Điểm đến
205,optimistic,(adj),/ˌɒptɪˈmɪstɪk/,Lạc quan
206,mentality,(n),/menˈtæləti/,"Tâm lý, tư duy"
207,dominate,(v),/ˈdɒmɪneɪt/,"Thống trị, chiếm ưu thế"
208,propose,(v),/prəˈpəʊz/,Đề xuất
209,intend,(v),/ɪnˈtend/,Có ý định
210,initially,(adv),/ɪˈnɪʃəli/,Ban đầu
211,withdraw,(v),/wɪðˈdrɔː/,"Rút lui, rút khỏi"
212,attitude,(n),/ˈætɪtjuːd/,Thái độ
213,majority,(n),/məˈdʒɒrəti/,Đa số
214,resident,(n),/ˈrezɪdənt/,Cư dân
215,likelihood,(n),/ˈlaɪklihʊd/,Khả năng (sẽ xảy ra)
216,reputation,(n),/ˌrepjuˈteɪʃn/,Danh tiếng
217,hand out,(phr v),/hænd aʊt/,Phân phát
218,condemn,(v),/kənˈdem/,"Lên án, chỉ trích"
219,get off the ground,,,bắt đầu triển khai
220,seize this opportunity to ,,,năm bắt cơ hội
221,Divergent,adj,/daɪˈvɜː.dʒənt/,"Khác nhau, bất đồng, phân kỳ"
222,Cardiovascular,adj,/ˌkɑː.di.əʊˈvæs.kjə.lər/,(thuộc) Tim mạch
223,Osteoarthritis,n,/ˌɒs.ti.əʊ.ɑːˈθraɪ.tɪs/,"Thoái hóa khớp, viêm xương khớp"
224,Conducive,adj,/kənˈdʒuː.sɪv/,"Có lợi, thuận lợi, có ích (cho việc gì)"
225,Rendering,n,/ˈren.dər.ɪŋ/,"Sự kết xuất (hình ảnh), sự diễn tả"
226,Futile,adj,/ˈfjuː.taɪl/,"Vô ích, không hiệu quả, phù phiếm"
227,Imperil,v,/ɪmˈper.ɪl/,"Gây nguy hiểm, đẩy vào tình thế nguy hiểm"
228,Caprices,n (plural),/kəˈpriː.sɪz/,"(Những) sự thất thường, ý thích bất chợt"
229,Transformation,n,/ˌtræns.fəˈmeɪ.ʃən/,"Sự thay đổi, sự biến đổi (thường là lớn và tích cực)"
230,Modification,n,/ˌmɒd.ɪ.fɪˈkeɪ.ʃən/,"Sự sửa đổi, sự điều chỉnh"
231,Customisation,n,/ˌkʌs.tə.maɪˈzeɪ.ʃən/,Sự tùy chỉnh (làm theo yêu cầu riêng)
232,Specification,n,/ˌspes.ɪ.fɪˈkeɪ.ʃənz/,"Các thông số kỹ thuật, đặc điểm kỹ thuật"
233,Elite,n,/iˈliːt/,"Giới tinh hoa, nhóm người xuất sắc nhất"
234,Significance,n,/sɪɡˈnɪf.ɪ.kəns/,"Tầm quan trọng, ý nghĩa"
235,Tension,n,/ˈten.ʃən/,Độ căng (của dây vợt)
236,Synthetic,n,/sɪnˈθet.ɪks/,Các vật liệu tổng hợp
237,Additive,n,/ˈæd.ɪ.tɪvz/,Chất phụ gia
238,Preference,n,/ˈpref.ər.ən.sɪz/,"Sở thích cá nhân, sự ưa chuộng"
239,Gut,n,/ɡʌt/,Ruột (động vật)
240,Underestimate,v,/ˌʌn.dəˈres.tɪ.meɪt/,Đánh giá thấp
241,Tweak,v,/twiːk/,"Tinh chỉnh, điều chỉnh nhỏ"
242,Maximise,v,/ˈmæk.sɪ.maɪz/,Tối đa hóa
243,Generate,v,/ˈdʒen.ə.reɪt/,"Tạo ra, sản sinh ra"
244,Ban,v,/bæn/,Cấm
245,Experiment,v,/ɪkˈsper.ɪ.ment/,Thử nghiệm
246,Enhance,v,/ɪnˈhɑːns/,"Nâng cao, cải thiện"
247,Revolutionise,v,/ˌrev.əˈluː.ʃə.naɪz/,"Cách mạng hóa, thay đổi hoàn toàn"
248,Attribute to,phr. v.,/əˈtrɪb.juːt tuː/,"Quy cho, cho là do"
249,Anticipate,v,/ænˈtɪs.ɪ.peɪt/,"Lường trước, dự đoán"
250,Mould,v,/məʊld/,"Đúc, tạo khuôn"
251,Indicate,v,/ˈɪn.dɪ.keɪt/,"Chỉ ra, cho thấy"
252,Incredible,adj,/ɪnˈkred.ə.bəl/,"Khó tin, phi thường"
253,Remarkable,adj,/rɪˈmɑː.kə.bəl/,"Đáng chú ý, xuất sắc"
254,Subtle,adj,/ˈsʌt.əl/,"Tinh tế, khó nhận thấy"
255,Visible,adj,/ˈvɪz.ə.bəl/,"Có thể nhìn thấy, rõ ràng"
256,Publicised,adj,/ˈpʌb.lɪ.saɪzd/,Được công bố rộng rãi
257,Valuable,adj,/ˈvæl.jə.bəl/,"Có giá trị, quý giá"
258,Particular,adj,/pəˈtɪk.jə.lər/,"Kỹ tính, cầu kỳ, đặc biệt"
259,Thorough,adj,/ˈθʌr.ə/,"Kỹ lưỡng, cẩn thận"
260,Denser,adj,/ˈden.sər/,Dày đặc hơn
261,Primary,adj,/ˈpraɪ.mər.i/,"Chính, chủ yếu"
262,Durable,adj,/ˈdʒʊə.rə.bəl/,"Bền, có độ bền cao"
263,Climatic,adj,/klaɪˈmæt.ɪk/,Thuộc về khí hậu
264,The likes of,phrase,/ðə laɪks ɒv/,"Những người/thứ tương tự như, chẳng hạn như."
265,To name just a few,idiom,/tə neɪm dʒəst ə fjuː/,(Để) kể ra một vài ví dụ.
266,Pass more or less unnoticed,idiom,/pɑːs mɔːr ɔː les ˌʌnˈnəʊ.tɪst/,Gần như không được chú ý đến.
267,Readily available,adj phr,/ˈred.ɪ.li əˈveɪ.lə.bəl/,"Có sẵn, dễ dàng tìm thấy hoặc mua được."
268,The line between winning and losing becomes thinner,idiom,/... bɪˈtwiːn ˈwɪn.ɪŋ ænd ˈluː.zɪŋ bɪˈkʌmz ˈθɪn.ər/,Ranh giới giữa thắng và thua ngày càng mong manh.
269,Competitive advantage,n phr,/kəmˌpet.ə.tɪv ədˈvɑːn.tɪdʒ/,Lợi thế cạnh tranh.
270,Date back to,phr. v.,/deɪt bæk tuː/,"Có từ thời, bắt nguồn từ."
271,By far,idiom,/baɪ fɑː(r)/,"Hơn hẳn, cho đến nay."
272,A perfect fit for,phrase,/ə ˈpɜː.fekt fɪt fɔː(r)/,Một sự phù hợp hoàn hảo cho.
273,Battle it out,idiom,/ˈbæt.əl ɪt aʊt/,Tranh đấu quyết liệt.
274,Go beyond,phr. v.,/ɡəʊ bɪˈjɒnd/,"Vượt ra ngoài, không chỉ dừng lại ở."
275,Misfit,n,/ˈmɪs.fɪts/,"kẻ lập dị, không phù hợp với xã hội."
276,Daredevil,n,/ˈdeəˌdev.əlz/,"người liều lĩnh, táo bạo."
277,Swashbuckler,n,/ˈswɒʃˌbʌk.ləz/,"kẻ phiêu lưu, ưa mạo hiểm."
278,Pursuer,n,/pəˈsjuː.əz/, người truy đuổi.
279,Might,n,/maɪt/,"Sức mạnh, quyền lực to lớn."
280,Fleet,n,/fliːt/,Hạm đội.
281,Reign,n,/reɪn/,"Triều đại, thời gian trị vì."
282,Civilisation,n,/ˌsɪv.əl.aɪˈzeɪ.ʃən/,Nền văn minh.
283,Inhabitant,n,/ɪnˈhæb.ɪ.tənts/,Cư dân
284,Hardship,n,/ˈhɑːd.ʃɪps/,"Sự gian khổ, khó khăn."
285,Coves,n,/kəʊvz/,"Các vịnh nhỏ, vũng kín."
286,Retaliation,n,/rɪˌtæl.iˈeɪ.ʃən/,"Sự trả đũa, trả thù."
287,Opponent,n,/əˈpəʊ.nənts/,Đối thủ.
288,Correspondence,n,/ˌkɒr.əˈspɒn.dəns/,Thư từ liên lạc.
289,Disruption,n,/dɪsˈrʌp.ʃən/,"Sự gián đoạn, sự phá vỡ."
290,Commerce,n,/ˈkɒm.ɜːs/,"Thương mại, buôn bán."
291,Orator,n,/ˈɒr.ə.tər/,Nhà hùng biện.
292,Detour,n,/ˈdiː.tʊər/,Đường vòng.
293,Culprit,n,/ˈkʌl.prɪts/,Thủ phạm.
294,Dignitaries,n,/ˈdɪɡ.nɪ.tər.iz/,Các quan chức cấp cao.
295,Ransom,n,/ˈræn.səm/,Tiền chuộc.
296,Menace,n,/ˈmen.əs/,Mối đe dọa.
297,Prowl,v,/praʊl/,"Lảng vảng, rình mò."
298,Raid,v,/reɪd/,"Đột kích, cướp phá."
299,Eradicate,v,/ɪˈræd.ɪ.keɪt/,"Triệt hạ, xóa sổ hoàn toàn."
300,Predate,v,/ˌpriːˈdeɪt/,"Có trước, tồn tại trước."
301,Possess,v,/pəˈzes/,Sở hữu.
302,Surrender,v,/səˈren.dər/,Đầu hàng.
303,Resort to,phr. v.,/rɪˈzɔːt tuː/,Phải dùng đến (một biện pháp cuối cùng).
304,Boost,v,/buːst/,"Thúc đẩy, tăng cường."
305,Assure,v,/əˈʃɔː(r)/,"Cam đoan, trấn an."
306,Condone,v,/kənˈdəʊn/,"Bỏ qua, dung túng (cho hành vi sai trái)."
307,Praise,v,/preɪz/,"Ca ngợi, tán dương."
308,Glorify,v,/ˈɡlɔː.rɪ.faɪ/,"Tôn vinh, ca tụng."
309,Hamper,v,/ˈhæm.pər/,"Cản trở, gây khó khăn."
310,Profit from,phr. v.,/ˈprɒf.ɪt frɒm/,Hưởng lợi từ.
311,Embolden,v,/ɪmˈbəʊl.dən/,"Cổ vũ, làm cho bạo dạn hơn."
312,Kidnap,v,/ˈkɪd.næp/,Bắt cóc.
313,Outlive,v,/ˌaʊtˈlɪv/,"Sống lâu hơn; hoặc trở nên lỗi thời, hết giá trị."
314,Grant,v,/ɡrɑːnt/,"Ban cho, cấp cho."
315,Combat,v,/ˈkɒm.bæt/,"Chiến đấu, chống lại."
316,Assign,v,/əˈsaɪn/,"Phân công, chỉ định."
317,Cleanse,v,/klenz/,"Dọn sạch, thanh trừng."
318,Vital,adj,/ˈvaɪ.təl/,"Tối quan trọng, thiết yếu."
319,Fertile,adj,/ˈfɜː.taɪl/,"Màu mỡ, phì nhiêu."
320,Rugged,adj,/ˈrʌɡ.ɪd/,"Gồ ghề, hiểm trở."
321,Unsurpassed,adj,/ˌʌn.səˈpɑːst/,"Vô song, không gì sánh bằng."
322,Navigable,adj,/ˈnæv.ɪ.ɡə.bəl/,Có thể đi lại được bằng tàu thuyền.
323,Substantial,adj,/səbˈstæn.ʃəl/,"Đáng kể, lớn lao."
324,Liberal,adj,/ˈlɪb.ər.əl/,"Phóng khoáng, rộng rãi."
325,Prominent,adj,/ˈprɒm.ɪ.nənt/,"Nổi bật, lỗi lạc."
326,Concerted,adj,/kənˈsɜː.tɪd/,"Có phối hợp, đồng lòng."
327,Vast,adj,/vɑːst/,"Rộng lớn, mênh mông."
328,Spring to mind,idiom,/sprɪŋ tə maɪnd/,"Nảy ra trong đầu, hiện lên trong tâm trí."
329,In command of,phrase,/ɪn kəˈmɑːnd ɒv/,"Chỉ huy, điều khiển."
330,Spread fear across,phrase,/spred fɪər əˈkrɒs/,Gieo rắc nỗi sợ hãi khắp nơi.
331,Rely heavily on,phrase,/rɪˈlaɪ ˈhev.ɪ.li ɒn/,Phụ thuộc nặng nề vào.
332,Turn to (piracy),phr. v.,/tɜːn tuː/,Chuyển sang (làm cướp biển).
333,Strike undetected,phrase,/straɪk ˌʌn.dɪˈtek.tɪd/,Tấn công mà không bị phát hiện.
334,Caught in a trap,idiom,/kɔːt ɪn ə træp/,Bị mắc bẫy.
335,In return,phrase,/ɪn rɪˈtɜːn/,Để đáp lại.
336,Outlive one's usefulness,idiom,/... wʌnz ˈjuːs.fəl.nəs/,"Hết giá trị sử dụng, không còn hữu ích nữa."
337,At the hands of,idiom,/æt ðə hændz ɒv/,Dưới tay của (ai đó).
338,reap greater benefits,v.p,/riːp ˈɡreɪtər ˈbɛnɪfɪts/,gặt hái/thu được nhiều lợi ích hơn
339,uphold morals and values in a community,v.p,/ʌpˈhoʊld ˈmɔːrəlz ənd ˈvæljuːz ɪn ə kəˈmjuːnəti/,giữ gìn/đề cao đạo đức và các giá trị trong cộng đồng
340,contribute free labor to...,v.p,/kənˈtrɪbjuːt friː ˈleɪbər tuː.../,đóng góp lao động miễn phí cho...
341,seek employment,v.p,/siːk ɪmˈplɔɪmənt/,tìm kiếm việc làm
342,puts greater pressure on...,v.p,/pʊts ˈɡreɪtər ˈprɛʃər ɒn.../,gây áp lực lớn hơn lên...
343,demographic shift,n.p,/ˌdɛməˈɡræfɪk ʃɪft/,sự chuyển dịch nhân khẩu học
344,dependency ratio,n.p,/dɪˈpɛndənsi ˈreɪʃiˌoʊ/,tỷ lệ phụ thuộc
345,strain on public finances,n.p,/streɪn ɒn ˈpʌblɪk ˈfaɪnænsɪz/,gánh nặng cho tài chính công
346,pension burden,n.p,/ˈpɛnʃən ˈbɜːrdn/,gánh nặng lương hưu
347,shrinking workforce,n.p,/ˈʃrɪŋkɪŋ ˈwɜːrkfɔːrs/,lực lượng lao động bị thu hẹp
348,intergenerational equity,n.p,/ˌɪntərˌdʒɛnəˈreɪʃənəl ˈɛkwəti/,công bằng giữa các thế hệ
349,socioeconomic implications,n.p,/ˌsoʊsioʊˌɛkəˈnɒmɪk ˌɪmplɪˈkeɪʃənz/,hệ lụy kinh tế-xã hội
350,accumulated wealth,n.p,/əˈkjuːmjəˌleɪtɪd wɛlθ/,tài sản tích lũy
351,disposable income,n.p,/dɪˈspoʊzəbl ˈɪnkʌm/,thu nhập khả dụng
352,experienced workforce,n.p,/ɪkˈspɪəriənst ˈwɜːrkfɔːrs/,lực lượng lao động giàu kinh nghiệm
353,proactive policies,n.p,/proʊˈæktɪv ˈpɒləsiz/,chính sách chủ động
354,a double-edged sword,idiom,/ə ˈdʌbəl-ɛdʒd sɔːrd/,con dao hai lưỡi
355,to harness the potential of,v.p,/tə ˈhɑːrnəs ðə pəˈtɛnʃəl ʌv.../,khai thác tiềm năng của...
356,a burgeoning market,n.p,/ə ˈbɜːrdʒənɪŋ ˈmɑːrkɪt/,một thị trường đang phát triển nhanh
357,the grey pound,n.p,/ðə ɡreɪ paʊnd/,sức mua của người cao tuổi
358,caregiving burden,n.p,/ˈkɛərˌɡɪvɪŋ ˈbɜːrdn/,gánh nặng chăm sóc
359,to mitigate the negative effects,v.p,/tə ˈmɪtɪˌɡeɪt ðə ˈnɛɡətɪv ɪˈfɛkts/,giảm thiểu các tác động tiêu cực
360,lifelong learning,n.p,/ˈlaɪflɔːŋ ˈlɜːrnɪŋ/,học tập suốt đời
361,aroma,n.,/əˈroʊmə/,"mùi thơm, hương thơm"
362,beverage,n.,/ˈbɛvərɪdʒ/,đồ uống
363,cluster,n.,/ˈklʌstər/,"cụm, bó, đàn, bầy"
364,combine,v.,/kəmˈbaɪn/,"kết hợp, phối hợp"
365,condensed,adj.,/kənˈdɛnst/,"cô đặc, đăc lại"
366,contemporary,adj.,/kənˈtɛmpəˌrɛri/,"đương đại, đương thời"
367,cultivate,v.,/ˈkʌltɪˌveɪt/,"trồng trọt, trau dồi"
368,divine,adj.,/dɪˈvaɪn/,"thần thánh, thiêng liêng"
369,humid,adj.,/ˈhjuːmɪd/,"ẩm, ẩm ướt"
370,odor,n.,/ˈoʊdər/,"mùi, mùi hôi"
371,palate,n.,/ˈpælɪt/,"vòm miệng, khẩu vị"
372,paradise,n.,/ˈpærəˌdaɪs/,thiên đường
373,plantation,n.,/plænˈteɪʃən/,đồn điền
374,rapid,adj.,/ˈræpɪd/,"nhanh, nhanh chóng"
375,rate,n.,/reɪt/,"tốc độ, tỷ lệ"
376,soothing,adj.,/ˈsuːðɪŋ/,"dịu dàng, êm dịu"
377,texture,n.,/ˈtɛkstʃər/,"kết cấu, bề mặt"
378,toxic,adj.,/ˈtɒksɪk/,"độc, độc hại"
379,vary,v.,/ˈvɛəri/,"thay đổi, biến đổi"
380,bring about,v.p,/brɪŋ əˈbaʊt/,"gây ra, mang lại"
381,care about,v.p,/kɛər əˈbaʊt/,quan tâm đến
382,do up,v.p,/duː ʌp/,"cài, thắt, trang trí, sửa chữa"
383,get over,v.p,/ɡɛt ˈoʊvər/,"vượt qua, bình phục"
384,give away,v.p,/ɡɪv əˈweɪ/,"cho đi, tiết lộ bí mật"
385,hand in,v.p,/hænd ɪn/,"nộp, đệ trình"
386,hold on,v.p,/hoʊld ɒn/,"giữ máy, chờ một chút, bám chặt"
387,make out,v.p,/meɪk aʊt/,"nhìn ra, hiểu được, hôn nhau"
388,put in for,v.p,/pʊt ɪn fɔːr/,"đòi hỏi, yêu sách, xin"
389,run into,v.p,/rʌn ˈɪntuː/,tình cờ gặp
390,set off,v.p,/sɛt ɔːf/,"khởi hành, bắt đầu một chuyến đi, gây nổ"
391,stand out,v.p,/stænd aʊt/,nổi bật
392,take over,v.p,/teɪk ˈoʊvər/,"tiếp quản, đảm nhận"
393,turn down,v.p,/tɜːrn daʊn/,"từ chối, vặn nhỏ (âm thanh, nhiệt độ)"
394,wrap up,v.p,/ræp ʌp/,"gói lại, kết thúc, mặc ấm"
395,absorbing,adj.,/əbˈsɔːrbɪŋ/,"lôi cuốn, hấp dẫn"
396,fatal,adj.,/ˈfeɪtəl/,"gây chết người, chí mạng"
397,genuine,adj.,/ˈdʒɛnjuɪn/,"thật, chân thật, chính hãng"
398,graceful,adj.,/ˈɡreɪsfəl/,"duyên dáng, uyển chuyển"
399,horrible,adj.,/ˈhɔːrəbəl/,"kinh khủng, khủng khiếp"
400,idle,adj.,/ˈaɪdəl/,"nhàn rỗi, lười biếng"
401,innocent,adj.,/ˈɪnəsənt/,"vô tội, ngây thơ"
402,judicious,adj.,/dʒuˈdɪʃəs/,"sáng suốt, khôn ngoan"
403,mean,adj.,/miːn/,"keo kiệt, xấu tính"
404,ordinary,adj.,/ˈɔːrdnˌɛri/,"bình thường, thông thường"
405,painful,adj.,/ˈpeɪnfəl/,đau đớn
406,praiseworthy,adj.,/ˈpreɪzˌwɜːrði/,đáng khen ngợi
407,precise,adj.,/prɪˈsaɪs/,"chính xác, tỉ mỉ"
408,puzzled,adj.,/ˈpʌzəld/,"bối rối, khó xử"
409,admiral,n.,/ˈædmərəl/,đô đốc
410,admonish,v.,/ædˈmɒnɪʃ/,"khiển trách, la rầy"
411,arc,n.,/ɑːrk/,"hình cung, vòng cung"
412,audible,adj.,/ˈɔːdəbəl/,có thể nghe thấy
413,awesome,adj.,/ˈɔːsəm/,"tuyệt vời, đáng kinh ngạc"
414,beware,v.,/bɪˈwɛər/,"cẩn thận, coi chừng"
415,brag,v.,/bræɡ/,khoe khoang
416,character,n.,/ˈkærəktər/,"tính cách, nhân vật"
417,conscience,n.,/ˈkɒnʃəns/,lương tâm
418,disagree,v.,/ˌdɪsəˈɡriː/,không đồng ý
419,echo,v.,/ˈɛkoʊ/,"vang lại, dội lại"
420,escape,v.,/ɪˈskeɪp/,trốn thoát
421,eventual,adj.,/ɪˈvɛntʃuəl/,"cuối cùng, sau cùng"
422,fiery,adj.,/ˈfaɪəri/,"bốc lửa, nảy lửa"
423,flesh,n.,/flɛʃ/,"thịt, da thịt"
424,grapefruit,n.,/ˈɡreɪpˌfruːt/,quả bưởi
425,hay,n.,/heɪ/,cỏ khô
426,hint,n.,/hɪnt/,lời gợi ý
427,horrified,adj.,/ˈhɔːrəˌfaɪd/,"kinh hoàng, khiếp sợ"
428,idiot,n.,/ˈɪdiət/,kẻ ngốc
429,indirect,adj.,/ˌɪndəˈrɛkt/,gián tiếp
430,kerosene,n.,/ˈkɛrəˌsiːn/,dầu hỏa
431,loop,n.,/luːp/,"vòng lặp, cái khâu"
432,middle,n.,/ˈmɪdəl/,"ở giữa, trung tâm"
433,option,n.,/ˈɒpʃən/,sự lựa chọn
434,paddle,n.,/ˈpædəl/,mái chèo
435,pastime,n.,/ˈpæsˌtaɪm/,"trò tiêu khiển, thú vui"
436,perfect,adj.,/ˈpɜːrfɪkt/,hoàn hảo
437,pinpoint,v.,/ˈpɪnˌpɔɪnt/,xác định chính xác
438,sour,adj.,/ˈsaʊər/,chua
439,stake,n.,/steɪk/,"cái cọc, tiền cược"
440,steward,n.,/ˈstjuːərd/,"người phục vụ (trên tàu, máy bay)"
441,string,n.,/strɪŋ/,"dây, sợi dây"
442,switch,v.,/swɪtʃ/,"chuyển đổi, công tắc"
443,thorn,n.,/θɔːrn/,cái gai
444,torment,v.,/tɔːrˈmɛnt/,"dằn vặt, làm đau khổ"
445,abrupt,adj.,/əˈbrʌpt/,"đột ngột, bất ngờ"
446,agony,n.,/ˈæɡəni/,sự đau đớn tột cùng
447,assassin,n.,/əˈsæsɪn/,"kẻ ám sát, sát thủ"
448,beard,n.,/bɪərd/,râu
449,beast,n.,/biːst/,"quái vật, con thú"
450,chapel,n.,/ˈtʃæpəl/,nhà nguyện`;

            // State variables
            let allVocab = [];
            let quizData = [];
            let timerInterval;
            let currentUsername = '';
            let userAnswers = {};
            let latestResult = null; // Biến để lưu kết quả mới nhất

            // DOM Elements
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
            const retakeBtn = document.getElementById('retakeBtn');
            const exportBtn = document.getElementById('exportBtn'); // Nút xuất kết quả
            const timerElement = document.getElementById('timer');

            // --- FUNCTIONS ---

            const parseCSV = (csv) => {
                return csv.split('\n')
                    .map(line => line.split(','))
                    .filter(parts => parts.length >= 5)
                    .map(parts => ({
                        word: parts[1].trim(),
                        definition: parts.slice(4).join(',').trim().replace(/^"|"$/g, '')
                    }))
                    .filter(vocab => vocab.word && vocab.definition);
            };
            
            const generateRandomQuiz = (count) => {
                const shuffledVocab = [...allVocab].sort(() => 0.5 - Math.random());
                const selectedWords = shuffledVocab.slice(0, count);
                
                quizData = selectedWords.map(correctWord => {
                    const answer = correctWord.definition;
                    const wrongOptions = new Set();
                    
                    while (wrongOptions.size < 3) {
                        const randomWord = allVocab[Math.floor(Math.random() * allVocab.length)];
                        if (randomWord.definition !== answer) {
                            wrongOptions.add(randomWord.definition);
                        }
                    }

                    const options = [answer, ...wrongOptions].sort(() => 0.5 - Math.random());
                    
                    return {
                        word: correctWord.word,
                        question: `Đâu là nghĩa của từ: <strong>"${correctWord.word}"</strong>?`,
                        options,
                        answer
                    };
                });
            };

            const showTab = (tabId) => {
                tabContents.forEach(content => content.classList.add('hide'));
                document.getElementById(tabId)?.classList.remove('hide');

                tabs.forEach(tab => {
                    tab.classList.toggle('active', tab.dataset.tab === tabId && !tab.disabled);
                });
            };

            const loadQuiz = () => {
                quizContainer.innerHTML = quizData.map((q, index) => `
                    <div class="bg-gray-50 p-5 rounded-lg border border-gray-200">
                        <p class="font-semibold text-lg mb-4">${index + 1}. ${q.question}</p>
                        <div class="space-y-2">
                            ${q.options.map(option => `
                                <label class="flex items-center p-3 rounded-lg border border-gray-200 hover:bg-blue-100 cursor-pointer transition has-[:checked]:bg-blue-100 has-[:checked]:border-blue-400">
                                    <input type="radio" name="question${index}" value="${option}" class="mr-3 focus:ring-blue-500">
                                    <span>${option}</span>
                                </label>
                            `).join('')}
                        </div>
                    </div>
                `).join('');
            };

            const startTimer = () => {
                let timeLeft = 20 * 60; // 20 minutes
                
                const updateTimer = () => {
                    timeLeft--;
                    const minutes = Math.floor(timeLeft / 60);
                    const seconds = timeLeft % 60;
                    timerElement.textContent = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;

                    if (timeLeft <= 0) {
                        clearInterval(timerInterval);
                        submitQuiz();
                    }
                };

                updateTimer(); // run once immediately
                timerInterval = setInterval(updateTimer, 1000);
            };

            const submitQuiz = () => {
                clearInterval(timerInterval);
                submitBtn.disabled = true;
                let score = 0;
                userAnswers = {};

                quizData.forEach((q, index) => {
                    const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                    const selectedValue = selectedOption ? selectedOption.value : null;
                    userAnswers[index] = selectedValue;
                    if (selectedValue === q.answer) {
                        score++;
                    }
                });

                latestResult = { // Cập nhật kết quả mới nhất
                    name: currentUsername,
                    score,
                    total: quizData.length,
                    date: new Date().toLocaleString('vi-VN')
                };

                resultContent.innerHTML = `
                    <p class="text-lg"><span class="font-semibold">Tên:</span> ${latestResult.name}</p>
                    <p class="text-3xl font-bold my-4 ${latestResult.score / latestResult.total >= 0.5 ? 'text-green-600' : 'text-red-600'}">
                        ${latestResult.score} / ${latestResult.total}
                    </p>
                    <p class="text-gray-500">Ngày làm: ${latestResult.date}</p>
                `;
                
                saveResult(latestResult);
                document.querySelector('button[data-tab="result"]').disabled = false;
                document.querySelector('button[data-tab="answers"]').disabled = false;
                loadAnswers();
                loadHistory(); 
                showTab('result');
            };
            
            const saveResult = (result) => {
                try {
                    let history = JSON.parse(localStorage.getItem('vocabTestHistory')) || [];
                    history.unshift(result);
                    localStorage.setItem('vocabTestHistory', JSON.stringify(history));
                } catch (e) {
                    console.error("Không thể lưu vào localStorage:", e);
                }
            };
            
            const loadHistory = () => {
                 let history = [];
                 try {
                     history = JSON.parse(localStorage.getItem('vocabTestHistory')) || [];
                 } catch (e) {
                     console.error("Không thể đọc từ localStorage:", e);
                 }

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
                    </table>`;
            };

            const loadAnswers = () => {
                answersContainer.innerHTML = quizData.map((q, index) => {
                    const userAnswer = userAnswers[index];
                    const isCorrect = userAnswer === q.answer;
                    
                    let resultHtml;
                    if (userAnswer === null) {
                        resultHtml = `<p class="text-sm font-medium text-yellow-600"><strong>➖ Bạn chưa trả lời</strong></p>`;
                    } else if (isCorrect) {
                        resultHtml = `<p class="text-sm font-medium text-green-600"><strong>✔️ Bạn đã chọn đúng:</strong> ${userAnswer}</p>`;
                    } else {
                        resultHtml = `<p class="text-sm font-medium text-red-600"><strong>❌ Bạn đã chọn sai:</strong> ${userAnswer}</p>`;
                    }

                    return `
                        <div class="bg-gray-50 p-5 rounded-lg border border-gray-200">
                            <p class="font-semibold text-lg mb-2">${index + 1}. ${q.question}</p>
                            ${resultHtml}
                            <p class="text-sm font-medium text-blue-600 mt-2"><strong>Đáp án đúng:</strong> ${q.answer}</p>
                        </div>`;
                }).join('');
            };

            // HÀM MỚI ĐỂ XUẤT KẾT QUẢ
            const exportResults = () => {
                if (!latestResult) {
                    alert('Không có kết quả để xuất!');
                    return;
                }

                // 1. Tạo nội dung file text
                let content = `KẾT QUẢ BÀI KIỂM TRA TỪ VỰNG - TODUYENIELTS\n`;
                content += `=========================================\n\n`;
                content += `Họ và tên: ${latestResult.name}\n`;
                content += `Ngày làm bài: ${latestResult.date}\n`;
                content += `Điểm số: ${latestResult.score} / ${latestResult.total}\n\n`;
                content += `CHI TIẾT BÀI LÀM\n`;
                content += `-----------------------------------------\n\n`;

                quizData.forEach((q, index) => {
                    const userAnswer = userAnswers[index];
                    const isCorrect = userAnswer === q.answer;
                    const questionText = q.question.replace(/<strong>|<\/strong>/g, ""); // Xóa tag HTML

                    content += `Câu ${index + 1}: ${questionText}\n`;
                    content += `  - Bạn đã chọn: ${userAnswer || 'Chưa trả lời'}\n`;
                    content += `  - Đáp án đúng: ${q.answer}\n`;
                    content += `  - Kết quả: ${isCorrect ? 'Đúng' : 'Sai'}\n\n`;
                });

                // 2. Tạo và tải file
                const blob = new Blob([content], { type: 'text/plain;charset=utf-8' });
                const link = document.createElement('a');
                link.href = URL.createObjectURL(blob);
                const safeName = latestResult.name.replace(/[^a-z0-9]/gi, '_').toLowerCase();
                const dateString = new Date().toISOString().slice(0, 10);
                link.download = `ket-qua-${safeName}-${dateString}.txt`;
                
                document.body.appendChild(link);
                link.click();
                document.body.removeChild(link);
            };

            const resetQuiz = () => {
                clearInterval(timerInterval);
                userAnswers = {};
                currentUsername = '';
                quizData = [];
                latestResult = null; // Reset kết quả
                
                timerElement.textContent = "20:00";
                usernameInput.value = '';
                startBtn.disabled = false;
                submitBtn.disabled = false;
                
                ['quiz', 'result', 'answers'].forEach(tabName => {
                    document.querySelector(`button[data-tab="${tabName}"]`).disabled = true;
                });
                
                showTab('name');
            };

            // --- EVENT LISTENERS ---

            tabs.forEach(tab => {
                tab.addEventListener('click', () => !tab.disabled && showTab(tab.dataset.tab));
            });

            startBtn.addEventListener('click', () => {
                currentUsername = usernameInput.value.trim();
                if (currentUsername) {
                    startBtn.disabled = true;
                    document.querySelector('button[data-tab="quiz"]').disabled = false;
                    
                    generateRandomQuiz(150);
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
            retakeBtn.addEventListener('click', resetQuiz);
            exportBtn.addEventListener('click', exportResults); // Gắn sự kiện cho nút mới

            // --- INITIALIZATION ---
            allVocab = parseCSV(vocabularyCSV);
            loadHistory();
            showTab('name');
        });
    </script>
</body>
</html>
