<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToDuyenIELTS - Kiểm tra 150 từ vựng</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- Thư viện SheetJS (xlsx) để tạo và xuất file Excel -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
    
    <style>
        body { font-family: 'Inter', sans-serif; }
        .tab-button.active { background-color: #3b82f6; color: white; border-bottom-color: transparent; }
        .hide { display: none; }
        button:disabled { opacity: 0.5; cursor: not-allowed; }
    </style>
</head>
<body class="bg-gray-100 text-gray-800 flex items-center justify-center min-h-screen py-8">
    <div class="container mx-auto p-4 sm:p-6 lg:p-8 max-w-4xl">
        <div class="bg-white rounded-2xl shadow-xl overflow-hidden">
            <div class="p-6 bg-blue-600 text-white">
                <h2 class="text-center text-lg font-semibold text-blue-200">ToDuyenIELTS</h2>
                <h1 class="text-3xl font-bold text-center mt-1">Bài kiểm tra 150 từ vựng</h1>
                <p class="text-center text-blue-200 mt-2">150 câu hỏi trong 20 phút</p>
            </div>

            <nav class="flex flex-wrap justify-center border-b border-gray-200 bg-gray-50">
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100" data-tab="name">1. Tên</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100" data-tab="quiz" disabled>2. Bài làm</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100" data-tab="result" disabled>3. Kết quả</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100" data-tab="answers" disabled>4. Đáp án</button>
                <button class="tab-button py-4 px-6 text-sm sm:text-base font-medium text-gray-600 hover:bg-blue-100" data-tab="history">5. Lịch sử</button>
            </nav>

            <main class="p-6 sm:p-8">
                <div id="name" class="tab-content">
                    <h2 class="text-2xl font-semibold mb-4 text-center text-blue-800">Chào mừng bạn!</h2>
                    <p class="text-center text-gray-700 mb-6">Vui lòng nhập tên của bạn để bắt đầu bài kiểm tra.</p>
                    <div class="max-w-sm mx-auto">
                        <input type="text" id="username" placeholder="Nhập tên của bạn..." class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
                        <button id="startBtn" class="w-full mt-4 bg-blue-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-blue-600 transition-transform transform hover:scale-105">Bắt đầu</button>
                    </div>
                </div>

                <div id="quiz" class="tab-content hide">
                    <div class="flex justify-between items-center mb-6">
                        <h2 class="text-2xl font-semibold text-blue-800">Câu hỏi</h2>
                        <div id="timer" class="text-xl font-bold bg-blue-100 text-blue-700 px-4 py-2 rounded-lg">20:00</div>
                    </div>
                    <div id="quiz-container" class="space-y-6"></div>
                    <button id="submitBtn" class="w-full mt-8 bg-green-500 text-white font-bold py-3 px-4 rounded-lg hover:bg-green-600 transition-transform transform hover:scale-105">Nộp bài</button>
                </div>

                <div id="result" class="tab-content hide text-center">
                    <h2 class="text-2xl font-semibold mb-4 text-blue-800">Hoàn thành!</h2>
                    <div id="result-content" class="bg-gray-50 p-8 rounded-lg space-y-3 max-w-md mx-auto"></div>
                    <!-- CÁC NÚT CHỨC NĂNG VÀ XUẤT FILE -->
                    <div class="mt-8 flex flex-wrap justify-center items-center gap-4">
                        <button id="retakeBtn" class="w-full sm:w-auto bg-blue-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-blue-600 transition-transform transform hover:scale-105">Làm lại</button>
                        <button id="reviewAnswersBtn" class="w-full sm:w-auto bg-purple-500 text-white font-bold py-3 px-6 rounded-lg hover:bg-purple-600 transition-transform transform hover:scale-105">Xem đáp án</button>
                        <button id="exportXlsxBtn" class="w-full sm:w-auto bg-emerald-600 text-white font-bold py-3 px-6 rounded-lg hover:bg-emerald-700 transition-transform transform hover:scale-105">Xuất Excel</button>
                    </div>
                </div>

                <div id="answers" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center text-blue-800">Đáp án chi tiết</h2>
                    <div id="answers-container" class="space-y-4"></div>
                </div>

                <div id="history" class="tab-content hide">
                    <h2 class="text-2xl font-semibold mb-6 text-center text-blue-800">Lịch sử làm bài</h2>
                    <div id="history-container" class="overflow-x-auto"></div>
                </div>
            </main>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
             // DỮ LIỆU TỪ VỰNG (ĐÃ XÓA PHIÊN ÂM)
            const vocabularyCSV = `1,Tune,(v),,"Theo dõi, điều chỉnh"
2,A 20-year wait,(phrase),,Sự chờ đợi 20 năm
3,Renown,(n),,"Tiếng tăm, sự nổi danh"
4,Stall in,(v),,"Dừng lại, chững lại"
5,Anonymous,(a),,"Ẩn danh, vô danh"
6,Donor,(n),,"Người tài trợ, người tặng"
7,Be granted,(phrase),,"Được cấp, được tài trợ"
8,Engagement,(n),,"Sự tham gia, sự gắn kết; hôn ước"
9,Troupe,(n),,"Đoàn (kịch, hát)"
10,Entitle,(v),,"Cho quyền, đặt tên cho"
11,Capacity of,(phrase),,"Với tư cách là, khả năng của"
12,In executive roles,(phrase),,Trong vai trò quản lý/điều hành
13,Coworker,(n),,Đồng nghiệp
14,Discrepancy,(n),,"Sự khác nhau, sự không nhất quán"
15,Token,(a),,Tượng trưng
16,Well-deserved roles,(phrase),,Vai trò xứng đáng
17,The relevance of,(phrase),,Sự liên quan của
18,Tangible,(a),,Hữu hình
19,Intangible,(a),,Vô hình
20,Underlie,(v),,"Nằm dưới, làm nền tảng cho"
21,Stigma,(n),,Sự kỳ thị
22,Professionalism,(n),,Tính chuyên nghiệp
23,agrarian,(adj),,(thuộc về) nông nghiệp
24,manufacturing techniques,(phrase),,Kỹ thuật sản xuất/chế tạo
25,in mass quantities,(phrase),,Với số lượng lớn
26,pump,"(v, n)",,Bơm; máy bơm
27,adapt,(v),,"Thích nghi, điều chỉnh"
28,the forward and backward,(phrase),,Chuyển động tới lui
29,the gear mechanism,(phrase),,Cơ cấu/cơ chế bánh răng
30,rotary motion,(phrase),,Chuyển động quay tròn
31,relatively,(adv),,Tương đối
32,locomotive,(n),,Đầu máy (xe lửa)
33,spinner,(n),,Thợ kéo sợi; máy kéo sợi
34,weaver,(n),,Thợ dệt
35,thread,(n),,"Sợi chỉ, sợi tơ"
36,mechanise (mechanize),(v),,Cơ giới hóa
37,undergo,(v),,"Trải qua, chịu đựng"
38,adopt,(v),,"Áp dụng, chấp nhận"
39,chief,(adj),,"Chính, chủ yếu, hàng đầu"
40,iron ore,(n),,Quặng sắt
41,charcoal,(n),,"Than củi, than gỗ"
42,metals,(n),,Kim loại
43,enable,(v),,"Cho phép, làm cho có thể"
44,steel,(n),,Thép
45,in response to,(phrase),,Để đáp lại
46,communication,(n),,"Sự giao tiếp, truyền thông"
47,communicate,(v),,"Giao tiếp, truyền đạt"
48,immense,(adj),,"To lớn, mênh mông, bao la"
49,rural areas,(phrase),,Vùng nông thôn
50,accelerate,(v),,"Tăng tốc, thúc đẩy"
51,dramatically,(adv),,"Một cách đáng kể, đột ngột"
52,inadequate,(adj),,"Không đủ, thiếu"
53,sanitation,(n),,Hệ thống vệ sinh
54,the middle and upper classes,(phrase),,Tầng lớp trung lưu và thượng lưu
55,struggle,"(v, n)",,Đấu tranh; cuộc đấu tranh
56,along with,(phrase),,Cùng với
57,the pace of,(phrase),,Nhịp độ của
58,fuel,(v),,"Thúc đẩy, tiếp nhiên liệu"
59,opposition,(n),,Sự phản đối
60,industrialisation,(n),,Sự công nghiệp hóa
61,textile,"(n, adj)",,"Vải dệt, hàng dệt; (thuộc) ngành dệt"
62,object to,(v),,Phản đối
63,mechanised looms,(phrase),,Khung cửi cơ giới hóa
64,knitting frames,(phrase),,Khung dệt kim
65,craft,(n),,Nghề thủ công
66,livelihood,(n),,Kế sinh nhai
67,rob,(v),,"Cướp, tước đoạt"
68,desperate,(adj),,"Tuyệt vọng, liều lĩnh"
69,smash,(v),,Đập tan
70,apprentice,(n),,Người học việc
71,rumour (rumor),(n),,Tin đồn
72,wreck,(v),,"Phá hủy, làm hỏng"
73,take place,(phrase),,"Diễn ra, xảy ra"
74,spread across,(phrase),,Lan rộng khắp
75,attack,"(v, n)",,Tấn công; cuộc tấn công
76,exchange,"(n, v)",,Sự trao đổi; trao đổi (khi đi với gunfire nghĩa là cuộc đấu súng)
77,gunfire,(n),,"Tiếng súng, cuộc đấu súng"
78,guard,"(n, v)",,"Lính gác, người bảo vệ; canh gác"
79,soldier,(n),,Người lính
80,punishable,(adj),,"Có thể bị trừng phạt, đáng bị phạt"
81,unrest,(n),,"Tình trạng bất ổn, náo động"
82,mill,(n),,"Nhà máy (dệt, xay xát), xưởng"
83,in the days that followed,(phrase),,Trong những ngày tiếp theo
84,arrest,"(v, n)",,Bắt giữ; vụ bắt giữ
85,resistance,(n),,"Sự kháng cự, sự chống cự"
86,vanish,(v),,"Biến mất, tan biến"
87,Brick by brick,(phrase),,"Từng viên gạch một, từ từ và kiên định"
88,magical,(adj),,"Kì diệu, có phép thuật"
89,fairy-tale,(n),,Truyện cổ tích
90,turret,(n),,Tháp nhỏ (trên lâu đài)
91,fire-breathing,(adj),,Phun ra lửa
92,wicked,(adj),,"Xấu xa, độc ác"
93,witch,(n),,Phù thủy
94,gallant,(adj),,"Dũng cảm, hào hiệp"
95,enchant,(v),,"Bỏ bùa, làm say mê"
96,be aware of,(phrase),,"Nhận thức về, ý thức về"
97,fantasy,(n),,"Sự tưởng tượng, ảo mộng"
98,repercussion,(n),,"Hậu quả, ảnh hưởng (thường là tiêu cực)"
99,abandon,(v),,"Từ bỏ, ruồng bỏ"
100,pretence (pretense),(n),,"Sự giả vờ, giả bộ"
101,tire,(v),,"Làm cho mệt mỏi, trở nên mệt mỏi"
102,settle down,(phr v),,Ổn định cuộc sống
103,take turns with,(phrase),,Thay phiên nhau
104,faculty,(n),,"Khả năng, năng lực (trí tuệ, thể chất)"
105,underpin,(v),,"Làm nền tảng, củng cố"
106,problem-solving,(n),,Việc giải quyết vấn đề
107,adaptable,(adj),,Dễ thích nghi
108,millennia,(n),,Thiên niên kỷ
109,philosopher,(n),,Nhà triết học
110,extoll (extol),(v),,"Tán dương, ca tụng"
111,virtue,(n),,"Đức tính tốt, đức hạnh"
112,play-based learning,(phrase),,Học tập thông qua trò chơi
113,increasingly,(adv),,Ngày càng
114,scarce,(adj),,Khan hiếm
115,curtail,(v),,"Cắt giảm, hạn chế"
116,victim,(n),,Nạn nhân
117,competition,(n),,"Sự cạnh tranh, cuộc thi"
118,concern,(n),,"Mối quan tâm, sự lo lắng"
119,implication,(n),,"Hàm ý, ảnh hưởng"
120,child-initiated,(adj),,Do trẻ em khởi xướng
121,spontaneous,(adj),,"Tự phát, tự nhiên"
122,unpredictable,(adj),,Không thể đoán trước
123,intervene,(v),,Can thiệp
124,puzzle,(n),,"Câu đố, trò chơi xếp hình"
125,possibility,(n),,Khả năng (có thể xảy ra)
126,awareness,(n),,Sự nhận thức
127,undertake,(v),,"Đảm nhận, thực hiện"
128,carry out,(phr v),,"Tiến hành, thực hiện"
129,pre-schooler,(n),,Trẻ mẫu giáo
130,unfamiliar,(adj),,Không quen thuộc
131,requiring scientific reasoning,(phrase),,Đòi hỏi sự lập luận khoa học
132,facilitate,(v),,"Tạo điều kiện, làm cho dễ dàng hơn"
133,extremely,(adv),,"Cực kỳ, vô cùng"
134,self-regulate,(v),,Tự điều chỉnh
135,indicator,(n),,"Chỉ số, dấu hiệu"
136,investigate,(v),,Điều tra
137,observe,(v),,Quan sát
138,diagnosis,(n),,Sự chẩn đoán
139,neurodevelopmental disorder,(phrase),,Rối loạn phát triển thần kinh
140,play-based approach,(phrase),,Phương pháp tiếp cận dựa trên trò chơi
141,stimulus,(n),,Sự kích thích
142,playful,(adj),,"Vui tươi, ham chơi"
143,comment,"(n, v)",,Lời bình luận; bình luận
144,backwater,(n),,"Nơi tù túng, hẻo lánh, kém phát triển"
145,untroubled,(adj),,"Yên bình, không bị làm phiền"
146,debate,"(n, v)",,Cuộc tranh luận; tranh luận
147,trivial,(adj),,"Tầm thường, không quan trọng"
148,contrast,"(n, v)",,Sự tương phản; làm tương phản
149,bike-sharing scheme,(phrase),,Kế hoạch/hệ thống chia sẻ xe đạp
150,come up with,(phr v),,"Nghĩ ra, nảy ra (ý tưởng)"
151,perceive,(v),,"Nhận thức, xem xét"
152,thread of,(phrase),,"Mạch (suy nghĩ), dòng (sự kiện)"
153,consumerism,(n),,Chủ nghĩa tiêu dùng
154,paint,(v),,"Sơn, vẽ"
155,distribute,(v),,Phân phát
156,leaflet,(n),,Tờ rơi
157,heavily,(adv),,"Nặng nề, rất nhiều"
158,recall,(v),,"Nhớ lại, gọi về"
159,particularly,(adv),,Đặc biệt là
160,publicise (publicize),(v),,"Công khai, quảng bá"
161,symbolic,(adj),,Tượng trưng
162,seize the opportunity to,(phrase),,Nắm bắt cơ hội để
163,elaborate,"(v, adj)",,"Diễn giải chi tiết; tỉ mỉ, phức tạp"
164,municipality,(n),,"Chính quyền thành phố, đô thị"
165,calculations,(n),,Sự tính toán
166,turned out,(phr v),,"Hóa ra, thành ra"
167,unanimously,(adv),,"Nhất trí, đồng lòng"
168,reject,(v),,"Bác bỏ, từ chối"
169,belong to,(phr v),,Thuộc về
170,glorious,(adj),,"Huy hoàng, rực rỡ"
171,discourage,(v),,Làm nản lòng
172,ask for,(phr v),,"Yêu cầu, xin"
173,deposit,"(n, v)",,Tiền đặt cọc; đặt cọc
174,drop,(v),,"Rơi, thả; từ bỏ (kế hoạch)"
175,conscious,(adj),,"Có ý thức, nhận biết được"
176,prove,(v),,Chứng minh
177,launch,(v),,"Ra mắt, khởi động, tung ra"
178,no longer,(phrase),,Không còn nữa
179,guilder,(n),,Đồng Guilder (tiền Hà Lan cũ)
180,conspicuous,(adj),,"Dễ thấy, nổi bật"
181,sturdy,(adj),,"Cứng cáp, vững chắc"
182,rack,(n),,"Giá, kệ (để đồ)"
183,the chip card,(phrase),,Thẻ chip
184,the bike rack,(phrase),,Giá để xe đạp
185,prone,(adj),,"Dễ bị, có khuynh hướng bị (điều gì xấu)"
186,vandalism,(n),,Hành vi phá hoại của công
187,theft,(n),,Sự trộm cắp
188,instantly,(adv),,Ngay lập tức
189,recognise (recognize),(v),,Nhận ra
190,blow,(n),,"Cú giáng, cú sốc"
191,abolish,(v),,"Bãi bỏ, hủy bỏ"
192,profitable,(adj),,Có lợi nhuận
193,pivotal,(adj),,"Then chốt, chủ chốt"
194,disappoint,(v),,Làm thất vọng
195,corporation,(n),,"Tập đoàn, công ty lớn"
196,boast,(v),,"Khoe khoang, tự hào về"
197,inspire,(v),,Truyền cảm hứng
198,set up,(phr v),,"Thành lập, thiết lập"
199,financially,(adv),,Về mặt tài chính
200,file,(v),,"Nộp (đơn), đệ trình"
201,patent,"(n, v)",,Bằng sáng chế; cấp bằng sáng chế
202,regard,"(v, n)",,"Coi như, xem như; sự quan tâm"
203,underground,"(adj, n)",,Dưới lòng đất; ngầm
204,destination,(n),,Điểm đến
205,optimistic,(adj),,Lạc quan
206,mentality,(n),,"Tâm lý, tư duy"
207,dominate,(v),,"Thống trị, chiếm ưu thế"
208,propose,(v),,Đề xuất
209,intend,(v),,Có ý định
210,initially,(adv),,Ban đầu
211,withdraw,(v),,"Rút lui, rút khỏi"
212,attitude,(n),,Thái độ
213,majority,(n),,Đa số
214,resident,(n),,Cư dân
215,likelihood,(n),,Khả năng (sẽ xảy ra)
216,reputation,(n),,Danh tiếng
217,hand out,(phr v),,Phân phát
218,condemn,(v),,"Lên án, chỉ trích"
219,get off the ground,,,bắt đầu triển khai
220,seize this opportunity to ,,,năm bắt cơ hội
221,Divergent,adj,,"Khác nhau, bất đồng, phân kỳ"
222,Cardiovascular,adj,,(thuộc) Tim mạch
223,Osteoarthritis,n,,"Thoái hóa khớp, viêm xương khớp"
224,Conducive,adj,,"Có lợi, thuận lợi, có ích (cho việc gì)"
225,Rendering,n,,"Sự kết xuất (hình ảnh), sự diễn tả"
226,Futile,adj,,"Vô ích, không hiệu quả, phù phiếm"
227,Imperil,v,,"Gây nguy hiểm, đẩy vào tình thế nguy hiểm"
228,Caprices,n (plural),,"(Những) sự thất thường, ý thích bất chợt"
229,Transformation,n,,"Sự thay đổi, sự biến đổi (thường là lớn và tích cực)"
230,Modification,n,,"Sự sửa đổi, sự điều chỉnh"
231,Customisation,n,,Sự tùy chỉnh (làm theo yêu cầu riêng)
232,Specification,n,,"Các thông số kỹ thuật, đặc điểm kỹ thuật"
233,Elite,n,,"Giới tinh hoa, nhóm người xuất sắc nhất"
234,Significance,n,,"Tầm quan trọng, ý nghĩa"
235,Tension,n,,Độ căng (của dây vợt)
236,Synthetic,n,,Các vật liệu tổng hợp
237,Additive,n,,Chất phụ gia
238,Preference,n,,"Sở thích cá nhân, sự ưa chuộng"
239,Gut,n,,Ruột (động vật)
240,Underestimate,v,,Đánh giá thấp
241,Tweak,v,,"Tinh chỉnh, điều chỉnh nhỏ"
242,Maximise,v,,Tối đa hóa
243,Generate,v,,"Tạo ra, sản sinh ra"
244,Ban,v,,Cấm
245,Experiment,v,,Thử nghiệm
246,Enhance,v,,"Nâng cao, cải thiện"
247,Revolutionise,v,,"Cách mạng hóa, thay đổi hoàn toàn"
248,Attribute to,phr. v.,,"Quy cho, cho là do"
249,Anticipate,v,,"Lường trước, dự đoán"
250,Mould,v,,"Đúc, tạo khuôn"
251,Indicate,v,,"Chỉ ra, cho thấy"
252,Incredible,adj,,"Khó tin, phi thường"
253,Remarkable,adj,,"Đáng chú ý, xuất sắc"
254,Subtle,adj,,"Tinh tế, khó nhận thấy"
255,Visible,adj,,"Có thể nhìn thấy, rõ ràng"
256,Publicised,adj,,Được công bố rộng rãi
257,Valuable,adj,,"Có giá trị, quý giá"
258,Particular,adj,,"Kỹ tính, cầu kỳ, đặc biệt"
259,Thorough,adj,,"Kỹ lưỡng, cẩn thận"
260,Denser,adj,,Dày đặc hơn
261,Primary,adj,,"Chính, chủ yếu"
262,Durable,adj,,"Bền, có độ bền cao"
263,Climatic,adj,,Thuộc về khí hậu
264,The likes of,phrase,,"Những người/thứ tương tự như, chẳng hạn như."
265,To name just a few,idiom,,(Để) kể ra một vài ví dụ.
266,Pass more or less unnoticed,idiom,,Gần như không được chú ý đến.
267,Readily available,adj phr,,"Có sẵn, dễ dàng tìm thấy hoặc mua được."
268,The line between winning and losing becomes thinner,idiom,,Ranh giới giữa thắng và thua ngày càng mong manh.
269,Competitive advantage,n phr,,Lợi thế cạnh tranh.
270,Date back to,phr. v.,,"Có từ thời, bắt nguồn từ."
271,By far,idiom,,"Hơn hẳn, cho đến nay."
272,A perfect fit for,phrase,,Một sự phù hợp hoàn hảo cho.
273,Battle it out,idiom,,Tranh đấu quyết liệt.
274,Go beyond,phr. v.,,"Vượt ra ngoài, không chỉ dừng lại ở."
275,Misfit,n,,"kẻ lập dị, không phù hợp với xã hội."
276,Daredevil,n,,"người liều lĩnh, táo bạo."
277,Swashbuckler,n,,"kẻ phiêu lưu, ưa mạo hiểm."
278,Pursuer,n,, người truy đuổi.
279,Might,n,,"Sức mạnh, quyền lực to lớn."
280,Fleet,n,,Hạm đội.
281,Reign,n,,"Triều đại, thời gian trị vì."
282,Civilisation,n,,Nền văn minh.
283,Inhabitant,n,,Cư dân
284,Hardship,n,,"Sự gian khổ, khó khăn."
285,Coves,n,,"Các vịnh nhỏ, vũng kín."
286,Retaliation,n,,"Sự trả đũa, trả thù."
287,Opponent,n,,Đối thủ.
288,Correspondence,n,,Thư từ liên lạc.
289,Disruption,n,,"Sự gián đoạn, sự phá vỡ."
290,Commerce,n,,"Thương mại, buôn bán."
291,Orator,n,,Nhà hùng biện.
292,Detour,n,,Đường vòng.
293,Culprit,n,,Thủ phạm.
294,Dignitaries,n,,Các quan chức cấp cao.
295,Ransom,n,,Tiền chuộc.
296,Menace,n,,Mối đe dọa.
297,Prowl,v,,"Lảng vảng, rình mò."
298,Raid,v,,"Đột kích, cướp phá."
299,Eradicate,v,,"Triệt hạ, xóa sổ hoàn toàn."
300,Predate,v,,"Có trước, tồn tại trước."
301,Possess,v,,Sở hữu.
302,Surrender,v,,Đầu hàng.
303,Resort to,phr. v.,,Phải dùng đến (một biện pháp cuối cùng).
304,Boost,v,,"Thúc đẩy, tăng cường."
305,Assure,v,,"Cam đoan, trấn an."
306,Condone,v,,"Bỏ qua, dung túng (cho hành vi sai trái)."
307,Praise,v,,"Ca ngợi, tán dương."
308,Glorify,v,,"Tôn vinh, ca tụng."
309,Hamper,v,,"Cản trở, gây khó khăn."
310,Profit from,phr. v.,,Hưởng lợi từ.
311,Embolden,v,,"Cổ vũ, làm cho bạo dạn hơn."
312,Kidnap,v,,Bắt cóc.
313,Outlive,v,,"Sống lâu hơn; hoặc trở nên lỗi thời, hết giá trị."
314,Grant,v,,"Ban cho, cấp cho."
315,Combat,v,,"Chiến đấu, chống lại."
316,Assign,v,,"Phân công, chỉ định."
317,Cleanse,v,,"Dọn sạch, thanh trừng."
318,Vital,adj,,"Tối quan trọng, thiết yếu."
319,Fertile,adj,,"Màu mỡ, phì nhiêu."
320,Rugged,adj,,"Gồ ghề, hiểm trở."
321,Unsurpassed,adj,,"Vô song, không gì sánh bằng."
322,Navigable,adj,,Có thể đi lại được bằng tàu thuyền.
323,Substantial,adj,,"Đáng kể, lớn lao."
324,Liberal,adj,,"Phóng khoáng, rộng rãi."
325,Prominent,adj,,"Nổi bật, lỗi lạc."
326,Concerted,adj,,"Có phối hợp, đồng lòng."
327,Vast,adj,,"Rộng lớn, mênh mông."
328,Spring to mind,idiom,,"Nảy ra trong đầu, hiện lên trong tâm trí."
329,In command of,phrase,,"Chỉ huy, điều khiển."
330,Spread fear across,phrase,,Gieo rắc nỗi sợ hãi khắp nơi.
331,Rely heavily on,phrase,,Phụ thuộc nặng nề vào.
332,Turn to (piracy),phr. v.,,Chuyển sang (làm cướp biển).
333,Strike undetected,phrase,,Tấn công mà không bị phát hiện.
334,Caught in a trap,idiom,,Bị mắc bẫy.
335,In return,phrase,,Để đáp lại.
336,Outlive one's usefulness,idiom,,"Hết giá trị sử dụng, không còn hữu ích nữa."
337,At the hands of,idiom,,Dưới tay của (ai đó).
338,reap greater benefits,v.p,,gặt hái/thu được nhiều lợi ích hơn
339,uphold morals and values in a community,v.p,,giữ gìn/đề cao đạo đức và các giá trị trong cộng đồng
340,contribute free labor to...,v.p,,đóng góp lao động miễn phí cho...
341,seek employment,v.p,,tìm kiếm việc làm
342,puts greater pressure on...,v.p,,gây áp lực lớn hơn lên...
343,demographic shift,n.p,,sự chuyển dịch nhân khẩu học
344,dependency ratio,n.p,,tỷ lệ phụ thuộc
345,strain on public finances,n.p,,gánh nặng cho tài chính công
346,pension burden,n.p,,gánh nặng lương hưu
347,shrinking workforce,n.p,,lực lượng lao động bị thu hẹp
348,intergenerational equity,n.p,,công bằng giữa các thế hệ
349,socioeconomic implications,n.p,,hệ lụy kinh tế-xã hội
350,accumulated wealth,n.p,,tài sản tích lũy
351,disposable income,n.p,,thu nhập khả dụng
352,experienced workforce,n.p,,lực lượng lao động giàu kinh nghiệm
353,proactive policies,n.p,,chính sách chủ động
354,a double-edged sword,idiom,,con dao hai lưỡi
355,to harness the potential of,v.p,,khai thác tiềm năng của...
356,a burgeoning market,n.p,,một thị trường đang phát triển nhanh
357,the grey pound,n.p,,sức mua của người cao tuổi
358,caregiving burden,n.p,,gánh nặng chăm sóc
359,to mitigate the negative effects,v.p,,giảm thiểu các tác động tiêu cực
360,lifelong learning,n.p,,học tập suốt đời
361,aroma,n.,,"mùi thơm, hương thơm"
362,beverage,n.,,đồ uống
363,cluster,n.,,"cụm, bó, đàn, bầy"
364,combine,v.,,"kết hợp, phối hợp"
365,condensed,adj.,,"cô đặc, đăc lại"
366,contemporary,adj.,,"đương đại, đương thời"
367,cultivate,v.,,"trồng trọt, trau dồi"
368,divine,adj.,,"thần thánh, thiêng liêng"
369,humid,adj.,,"ẩm, ẩm ướt"
370,odor,n.,,"mùi, mùi hôi"
371,palate,n.,,"vòm miệng, khẩu vị"
372,paradise,n.,,thiên đường
373,plantation,n.,,đồn điền
374,rapid,adj.,,"nhanh, nhanh chóng"
375,rate,n.,,"tốc độ, tỷ lệ"
376,soothing,adj.,,"dịu dàng, êm dịu"
377,texture,n.,,"kết cấu, bề mặt"
378,toxic,adj.,,"độc, độc hại"
379,vary,v.,,"thay đổi, biến đổi"
380,bring about,v.p,,"gây ra, mang lại"
381,care about,v.p,,quan tâm đến
382,do up,v.p,,"cài, thắt, trang trí, sửa chữa"
383,get over,v.p,,"vượt qua, bình phục"
384,give away,v.p,,"cho đi, tiết lộ bí mật"
385,hand in,v.p,,"nộp, đệ trình"
386,hold on,v.p,,"giữ máy, chờ một chút, bám chặt"
387,make out,v.p,,"nhìn ra, hiểu được, hôn nhau"
388,put in for,v.p,,"đòi hỏi, yêu sách, xin"
389,run into,v.p,,tình cờ gặp
390,set off,v.p,,"khởi hành, bắt đầu một chuyến đi, gây nổ"
391,stand out,v.p,,nổi bật
392,take over,v.p,,"tiếp quản, đảm nhận"
393,turn down,v.p,,"từ chối, vặn nhỏ (âm thanh, nhiệt độ)"
394,wrap up,v.p,,"gói lại, kết thúc, mặc ấm"
395,absorbing,adj.,,"lôi cuốn, hấp dẫn"
396,fatal,adj.,,"gây chết người, chí mạng"
397,genuine,adj.,,"thật, chân thật, chính hãng"
398,graceful,adj.,,"duyên dáng, uyển chuyển"
399,horrible,adj.,,"kinh khủng, khủng khiếp"
400,idle,adj.,,"nhàn rỗi, lười biếng"
401,innocent,adj.,,"vô tội, ngây thơ"
402,judicious,adj.,,"sáng suốt, khôn ngoan"
403,mean,adj.,,"keo kiệt, xấu tính"
404,ordinary,adj.,,"bình thường, thông thường"
405,painful,adj.,,đau đớn
406,praiseworthy,adj.,,đáng khen ngợi
407,precise,adj.,,"chính xác, tỉ mỉ"
408,puzzled,adj.,,"bối rối, khó xử"
409,admiral,n.,,đô đốc
410,admonish,v.,,"khiển trách, la rầy"
411,arc,n.,,"hình cung, vòng cung"
412,audible,adj.,,có thể nghe thấy
413,awesome,adj.,,"tuyệt vời, đáng kinh ngạc"
414,beware,v.,,"cẩn thận, coi chừng"
415,brag,v.,,khoe khoang
416,character,n.,,"tính cách, nhân vật"
417,conscience,n.,,lương tâm
418,disagree,v.,,không đồng ý
419,echo,v.,,"vang lại, dội lại"
420,escape,v.,,trốn thoát
421,eventual,adj.,,"cuối cùng, sau cùng"
422,fiery,adj.,,"bốc lửa, nảy lửa"
423,flesh,n.,,"thịt, da thịt"
424,grapefruit,n.,,quả bưởi
425,hay,n.,,cỏ khô
426,hint,n.,,lời gợi ý
427,horrified,adj.,,"kinh hoàng, khiếp sợ"
428,idiot,n.,,kẻ ngốc
429,indirect,adj.,,gián tiếp
430,kerosene,n.,,dầu hỏa
431,loop,n.,,"vòng lặp, cái khâu"
432,middle,n.,,"ở giữa, trung tâm"
433,option,n.,,sự lựa chọn
434,paddle,n.,,mái chèo
435,pastime,n.,,"trò tiêu khiển, thú vui"
436,perfect,adj.,,hoàn hảo
437,pinpoint,v,,xác định chính xác
438,sour,adj.,,chua
439,stake,n.,,"cái cọc, tiền cược"
440,steward,n.,,"người phục vụ (trên tàu, máy bay)"
441,string,n.,,"dây, sợi dây"
442,switch,v.,,"chuyển đổi, công tắc"
443,thorn,n.,,cái gai
444,torment,v.,,"dằn vặt, làm đau khổ"
445,abrupt,adj.,,"đột ngột, bất ngờ"
446,agony,n.,,sự đau đớn tột cùng
447,assassin,n.,,"kẻ ám sát, sát thủ"
448,beard,n.,,râu
449,beast,n.,,"quái vật, con thú"
450,chapel,n.,,nhà nguyện`;

            // State variables
            let allVocab = [], quizData = [], timerInterval, currentUsername = '', userAnswers = {}, latestResult = null;

            // DOM Elements
            const dom = {
                tabs: document.querySelectorAll('.tab-button'),
                tabContents: document.querySelectorAll('.tab-content'),
                startBtn: document.getElementById('startBtn'),
                submitBtn: document.getElementById('submitBtn'),
                usernameInput: document.getElementById('username'),
                quizContainer: document.getElementById('quiz-container'),
                answersContainer: document.getElementById('answers-container'),
                historyContainer: document.getElementById('history-container'),
                resultContent: document.getElementById('result-content'),
                reviewAnswersBtn: document.getElementById('reviewAnswersBtn'),
                retakeBtn: document.getElementById('retakeBtn'),
                exportXlsxBtn: document.getElementById('exportXlsxBtn'),
                timerElement: document.getElementById('timer')
            };

            // --- UTILITY FUNCTIONS ---
            const parseCSV = (csv) => {
                return csv.split('\n').map(line => line.split(',')).filter(parts => parts.length >= 5).map(parts => ({
                    word: parts[1].trim(),
                    definition: parts.slice(4).join(',').trim().replace(/^"|"$/g, '')
                })).filter(vocab => vocab.word && vocab.definition);
            };
            
            const getFileName = () => {
                const safeName = latestResult.name.replace(/[^a-z0-9]/gi, '_').toLowerCase();
                const dateString = new Date().toISOString().slice(0, 10);
                return `ket-qua-${safeName}-${dateString}`;
            };
            
            // --- CORE LOGIC ---
            const startQuiz = () => {
                currentUsername = dom.usernameInput.value.trim();
                if (currentUsername) {
                    dom.startBtn.disabled = true;
                    document.querySelector('button[data-tab="quiz"]').disabled = false;
                    generateRandomQuiz(150);
                    loadQuiz();
                    showTab('quiz');
                    startTimer();
                } else {
                    alert('Vui lòng nhập tên của bạn!');
                }
            };
            
            const startTimer = () => {
                let timeLeft = 20 * 60;
                const updateTimer = () => {
                    timeLeft--;
                    const minutes = Math.floor(timeLeft / 60);
                    const seconds = timeLeft % 60;
                    dom.timerElement.textContent = `${minutes}:${seconds < 10 ? '0' : ''}${seconds}`;
                    if (timeLeft <= 0) {
                        clearInterval(timerInterval);
                        submitQuiz();
                    }
                };
                updateTimer();
                timerInterval = setInterval(updateTimer, 1000);
            };
            
            const generateRandomQuiz = (count) => {
                const shuffledVocab = [...allVocab].sort(() => 0.5 - Math.random());
                const selectedWords = shuffledVocab.slice(0, count);
                quizData = selectedWords.map(correctWord => {
                    const answer = correctWord.definition;
                    const wrongOptions = new Set();
                    while (wrongOptions.size < 3) {
                        const randomWord = allVocab[Math.floor(Math.random() * allVocab.length)];
                        if (randomWord.definition !== answer) wrongOptions.add(randomWord.definition);
                    }
                    const options = [answer, ...wrongOptions].sort(() => 0.5 - Math.random());
                    return { word: correctWord.word, question: `Đâu là nghĩa của từ: <strong>"${correctWord.word}"</strong>?`, options, answer };
                });
            };

            const submitQuiz = () => {
                clearInterval(timerInterval);
                dom.submitBtn.disabled = true;
                let score = 0;
                userAnswers = {};
                quizData.forEach((q, index) => {
                    const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
                    const selectedValue = selectedOption ? selectedOption.value : null;
                    userAnswers[index] = selectedValue;
                    if (selectedValue === q.answer) score++;
                });
                latestResult = { name: currentUsername, score, total: quizData.length, date: new Date().toLocaleString('vi-VN') };
                dom.resultContent.innerHTML = `<p class="text-lg"><span class="font-semibold">Tên:</span> ${latestResult.name}</p><p class="text-3xl font-bold my-4 ${latestResult.score / latestResult.total >= 0.5 ? 'text-green-600' : 'text-red-600'}">${latestResult.score} / ${latestResult.total}</p><p class="text-gray-500">Ngày làm: ${latestResult.date}</p>`;
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
                } catch (e) { console.error("Could not save to localStorage:", e); }
            };

            // --- UI & RENDER FUNCTIONS ---
            const showTab = (tabId) => {
                dom.tabContents.forEach(content => content.classList.add('hide'));
                document.getElementById(tabId)?.classList.remove('hide');
                dom.tabs.forEach(tab => tab.classList.toggle('active', tab.dataset.tab === tabId && !tab.disabled));
            };
            
            const loadQuiz = () => {
                dom.quizContainer.innerHTML = quizData.map((q, index) => `<div class="bg-gray-50 p-5 rounded-lg border"><p class="font-semibold text-lg mb-4">${index + 1}. ${q.question}</p><div class="space-y-2">${q.options.map(option => `<label class="flex items-center p-3 rounded-lg border hover:bg-blue-100 cursor-pointer has-[:checked]:bg-blue-100 has-[:checked]:border-blue-400"><input type="radio" name="question${index}" value="${option}" class="mr-3"><span class="text-left">${option}</span></label>`).join('')}</div></div>`).join('');
            };
            const loadAnswers = () => {
                dom.answersContainer.innerHTML = quizData.map((q, index) => {
                    const userAnswer = userAnswers[index];
                    const isCorrect = userAnswer === q.answer;
                    let resultHtml;
                    if (userAnswer === null) resultHtml = `<p class="text-sm font-medium text-yellow-600"><strong>➖ Bạn chưa trả lời</strong></p>`;
                    else if (isCorrect) resultHtml = `<p class="text-sm font-medium text-green-600"><strong>✔️ Bạn đã chọn đúng:</strong> ${userAnswer}</p>`;
                    else resultHtml = `<p class="text-sm font-medium text-red-600"><strong>❌ Bạn đã chọn sai:</strong> ${userAnswer}</p>`;
                    return `<div class="bg-gray-50 p-5 rounded-lg border"><p class="font-semibold text-lg mb-2">${index + 1}. ${q.question}</p>${resultHtml}<p class="text-sm font-medium text-blue-600 mt-2"><strong>Đáp án đúng:</strong> ${q.answer}</p></div>`;
                }).join('');
            };
            const loadHistory = () => {
                let history = [];
                try { history = JSON.parse(localStorage.getItem('vocabTestHistory')) || []; } catch (e) { console.error("Could not read from localStorage:", e); }
                if (history.length === 0) {
                    dom.historyContainer.innerHTML = '<p class="text-center text-gray-500">Chưa có lịch sử làm bài.</p>';
                    return;
                }
                dom.historyContainer.innerHTML = `<table class="min-w-full bg-white border rounded-lg"><thead class="bg-gray-50"><tr><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Tên</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Điểm số</th><th class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase">Ngày</th></tr></thead><tbody class="divide-y">${history.map(item => `<tr><td class="px-6 py-4">${item.name}</td><td class="px-6 py-4 font-semibold">${item.score} / ${item.total}</td><td class="px-6 py-4">${item.date}</td></tr>`).join('')}</tbody></table>`;
            };

            // --- EXPORT FUNCTION ---
            const exportXlsx = () => {
                if (!latestResult) { alert('Không có kết quả để xuất!'); return; }
                try {
                    const summary = [
                        { A: 'Tên', B: latestResult.name },
                        { A: 'Ngày làm', B: latestResult.date },
                        { A: 'Điểm', B: `${latestResult.score}/${latestResult.total}` }
                    ];
                    const results = quizData.map((q, index) => {
                        const userAnswer = userAnswers[index];
                        const isCorrect = userAnswer === q.answer;
                        return {
                            'STT': index + 1,
                            'Từ vựng': q.word,
                            'Câu trả lời của bạn': userAnswer || 'Chưa trả lời',
                            'Đáp án đúng': q.answer,
                            'Kết quả': isCorrect ? 'Đúng' : 'Sai'
                        };
                    });
                    const summary_ws = XLSX.utils.json_to_sheet(summary, {skipHeader: true});
                    const results_ws = XLSX.utils.json_to_sheet(results);
                    
                    summary_ws['!cols'] = [{ wch: 10 }, { wch: 40 }];
                    results_ws['!cols'] = [{ wch: 5 }, { wch: 25 }, { wch: 40 }, { wch: 40 }, { wch: 10 }];
                    
                    const wb = XLSX.utils.book_new();
                    XLSX.utils.book_append_sheet(wb, summary_ws, "Tổng kết");
                    XLSX.utils.book_append_sheet(wb, results_ws, "Chi tiết");
                    
                    XLSX.writeFile(wb, `${getFileName()}.xlsx`);
                } catch(error) {
                    console.error("Lỗi khi tạo XLSX:", error);
                    alert("Đã xảy ra lỗi khi tạo file Excel. Vui lòng thử lại.");
                }
            };
            
            // --- EVENT LISTENERS & INITIALIZATION ---
            dom.startBtn.addEventListener('click', startQuiz);
            dom.submitBtn.addEventListener('click', () => { if (confirm('Bạn có chắc chắn muốn nộp bài không?')) submitQuiz(); });
            dom.reviewAnswersBtn.addEventListener('click', () => showTab('answers'));
            dom.retakeBtn.addEventListener('click', () => location.reload());
            dom.exportXlsxBtn.addEventListener('click', exportXlsx);
            dom.tabs.forEach(tab => tab.addEventListener('click', () => !tab.disabled && showTab(tab.dataset.tab)));
            
            allVocab = parseCSV(vocabularyCSV);
            loadHistory();
            showTab('name');
        });
    </script>
</body>
</html>

