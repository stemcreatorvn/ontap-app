<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>Ôn tập KHTN 7 – Chân Trời Sáng Tạo (Bài 1→Bài 10 - Tên bạn cung cấp)</title>
<style>
  :root{
    --bg:#0f172a; --card:#111827; --muted:#94a3b8; --text:#e5e7eb; --acc:#22c55e; --accent2:#38bdf8; --wrong:#ef4444;
  }
  html,body{background:linear-gradient(135deg,#07111b,#071427 60%,#07111b);color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Inter,Arial,sans-serif;margin:0}
  header{padding:22px 16px;border-bottom:1px solid #22314b;background:#06111acc;backdrop-filter:blur(6px);position:sticky;top:0;z-index:5}
  h1{margin:0;font-size:clamp(20px,2.6vw,28px);display:flex;gap:10px;align-items:center}
  .wrap{max-width:1100px;margin:20px auto;padding:0 16px}
  .toolbar{display:flex;flex-wrap:wrap;gap:10px;align-items:center;margin:12px 0 18px}
  select,button{background:#07121b;border:1px solid #223547;color:var(--text);padding:10px 12px;border-radius:10px;font-size:14px}
  button{cursor:pointer}
  button.primary{background:linear-gradient(135deg,#16a34a,#22c55e);border-color:#16a34a;color:#05130a}
  button.ghost{border-color:#334155}
  button:disabled{opacity:.5;cursor:not-allowed}
  .grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(300px,1fr));gap:16px;margin-top:16px}
  .card{background:var(--card);border:1px solid #1f2937;border-radius:12px;padding:14px}
  .q{font-weight:700;margin-bottom:8px}
  .ans{display:grid;gap:8px}
  .ans label{display:flex;gap:10px;align-items:flex-start;background:#06131a;border:1px solid #243047;padding:10px;border-radius:10px;cursor:pointer}
  .ans input{margin-top:3px}
  .badge{display:inline-flex;align-items:center;gap:6px;background:#071526;border:1px solid #243a4d;color:var(--muted);padding:6px 10px;border-radius:999px;font-size:12px}
  .pill{display:inline-block;background:#05221a;border:1px solid #14532d;color:#a7f3d0;padding:2px 8px;border-radius:999px;font-size:12px}
  .muted{color:var(--muted)}
  .footer{margin-top:18px;display:flex;gap:10px;flex-wrap:wrap;align-items:center}
  .correct{outline:2px solid var(--acc)}
  .wrong{outline:2px solid var(--wrong)}
  details{background:#081826;border:1px dashed #334155;border-radius:12px;padding:10px}
  summary{cursor:pointer}
  .score{font-weight:800}
  .small{font-size:13px;color:var(--muted);margin-top:8px}
  .mono{font-family:ui-monospace,SFMono-Regular,Menlo,monospace}
</style>
</head>
<body>
<header>
  <div class="wrap">
    <h1>🧠 Ôn tập KHTN 7 — Tùy chỉnh tên bài của bạn <span class="badge">Bài 1→Bài 10</span></h1>
    <p class="small">✅ Tên các bài đã được cập nhật theo danh sách bạn gửi. Chọn bài, số câu và bắt đầu luyện.</p>
    <div class="toolbar">
      <label>📚 Chọn bài:
        <select id="lessonSel">
          <option value="mix">Ngẫu nhiên (tất cả bài)</option>
          <option value="1">Bài 1: Phương Pháp và Kỹ Năng Học Tập Môn Khóa Học Tự nhiên</option>
          <option value="2">Bài 2: Nguyên tử</option>
          <option value="3">Bài 3: Nguyên tố hóa học</option>
          <option value="4">Bài 4: Sơ lược bản tuần hoàng các nguyên tố hóa học</option>
          <option value="5">Bài 5: Phân tử đơn chất, hợp chất</option>
          <option value="6">Bài 6: Giới thiệu về liên kết hóa học</option>
          <option value="7">Bài 7: Hóa trị và công thức hóa học</option>
          <option value="8">Bài 8: Tốc độ chuyển động</option>
          <option value="9">Bài 9: Độ thủy khoảng đường thời gian</option>
          <option value="10">Bài 10: Đo tốc độ</option>
        </select>
      </label>
      <label>🔀 Số câu:
        <select id="numSel">
          <option>10</option>
          <option>15</option>
          <option selected>20</option>
          <option>30</option>
        </select>
      </label>
      <button class="primary" id="startBtn">▶️ Bắt đầu</button>
      <button class="ghost" id="checkBtn" disabled>🧩 Nộp bài / Chấm điểm</button>
      <button class="ghost" id="showKeyBtn" disabled>🗝️ Hiện đáp án</button>
      <button class="ghost" id="retryBtn" disabled>🔁 Làm lại</button>
      <span id="status" class="pill">Sẵn sàng</span>
    </div>
  </div>
</header>

<main class="wrap">
  <div id="quiz" class="grid"></div>

  <div class="footer">
    <div id="result" class="score"></div>
    <div id="feedback" class="muted"></div>
  </div>

  <details style="margin-top:18px">
    <summary>ℹ️ Hướng dẫn nhanh</summary>
    <ul>
      <li>Chọn bài & số câu → nhấn <b>Bắt đầu</b>.</li>
      <li>Tích vào đáp án cho mỗi câu. Nhấn <b>Nộp bài</b> để chấm.</li>
      <li>Nhấn <b>Hiện đáp án</b> để xem gợi ý & đáp án đúng.</li>
      <li>Nhấn <b>Làm lại</b> để trộn câu mới.</li>
    </ul>
  </details>
</main>

<script>
const bank = [
/* ===== BÀI 1: Phương Pháp và Kỹ Năng Học Tập Môn Khóa Học Tự nhiên ===== */
{lesson:1,q:"Trình tự chuẩn của phương pháp khoa học thường gồm bước nào sau đây?",choices:["Quan sát → Đặt vấn đề → Đặt giả thuyết → Thí nghiệm → Kết luận ✔","Đặt giả thuyết → Quan sát → Kết luận → Thí nghiệm","Thí nghiệm → Kết luận → Đặt giả thuyết → Quan sát","Quan sát → Kết luận → Thí nghiệm → Đặt giả thuyết"],a:0,why:"Phương pháp khoa học: bắt đầu bằng quan sát, nêu vấn đề, đề xuất giả thuyết, kiểm tra bằng thí nghiệm, rồi rút kết luận."},
{lesson:1,q:"Kỹ thuật học tập nào được chứng minh giúp ghi nhớ lâu hơn?",choices:["Đọc đi đọc lại một lần là đủ","Ôn tập chủ động (active recall) và luyện tập có khoảng cách ✔","Chỉ nghe giảng mà không ôn lại","Ghi chép rồi để đó không xem lại"],a:1,why:"Active recall và spaced repetition giúp củng cố trí nhớ lâu dài."},
{lesson:1,q:"Khi chuẩn bị làm thí nghiệm, việc quan trọng nhất là:",choices:["Đọc kỹ hướng dẫn và mặc đồ bảo hộ (PPE) ✔","Mang đồ ăn vào phòng thí nghiệm","Tự ý thay đổi hóa chất thử nghiệm","Không cần chuẩn bị, làm theo cảm tính"],a:0,why:"An toàn và hiểu quy trình là điều cần thiết trước khi thực hành."},
{lesson:1,q:"Ghi chú hiệu quả trong giờ học thường dùng phương pháp nào?",choices:["Phương pháp Cornell (ghi, tóm tắt, câu hỏi) ✔","Ghi tất cả lời giảng nguyên văn","Không ghi gì, chỉ chụp ảnh bảng","Chỉ vẽ sơ đồ mà không ghi từ khóa"],a:0,why:"Cornell giúp tổ chức thông tin, dễ ôn tập và tạo câu hỏi."},
{lesson:1,q:"Mục tiêu học tập theo nguyên tắc SMART là:",choices:["Cụ thể, Đo lường được, Có thể đạt, Thực tế, Có thời hạn ✔","Tự do, Mơ hồ, Không cần đánh giá, Lâu dài","Chỉ tập trung vào điểm số","Đặt quá nhiều mục tiêu cùng lúc"],a:0,why:"SMART giúp mục tiêu rõ ràng và khả thi."},
{lesson:1,q:"Kỹ thuật Pomodoro thường áp dụng là:",choices:["25 phút làm việc, 5 phút nghỉ ✔","2 giờ làm việc liên tục không nghỉ","10 phút làm, 50 phút nghỉ","Làm việc liên tục cả ngày"],a:0,why:"Pomodoro: 25' tập trung, 5' nghỉ giúp tăng hiệu quả và tránh mệt mỏi."},

/* ===== BÀI 2: Nguyên tử ===== */
{lesson:2,q:"Nguyên tử gồm những hạt cơ bản nào?",choices:["Proton, Nơtron và Electron ✔","Proton, Photon, Electron","Electron, Photon, Gluon","Quark, Meson, Lepton"],a:0,why:"Nguyên tử gồm proton, neutron (trong hạt nhân) và electron (vỏ electron)."},
{lesson:2,q:"Số nguyên tử (Z) biểu thị:",choices:["Số proton trong hạt nhân ✔","Tổng số proton và nơtron","Số electron trên toàn bộ vỏ","Khối lượng nguyên tử"],a:0,why:"Z = số proton, đặc trưng cho một nguyên tố."},
{lesson:2,q:"Một nguyên tử trung hòa về điện có đặc điểm:",choices:["Số proton = số electron ✔","Proton nhiều hơn electron","Electron nhiều hơn proton","Không có nơtron"],a:0,why:"Trung hòa nghĩa là tổng điện tích bằng 0 → proton = electron."},
{lesson:2,q:"Khối lượng nguyên tử xấp xỉ bằng:",choices:["Số proton + số nơtron trong hạt nhân ✔","Số electron","Số proton × electron","Số proton trừ nơtron"],a:0,why:"Mass number ≈ proton + neutron (electron rất nhẹ)."},
{lesson:2,q:"Electron ở nguyên tử chủ yếu phân bố ở:",choices:["Vỏ electron xung quanh hạt nhân ✔","Bên trong hạt nhân","Ở ngoài không gian vô tận","Chỉ ở một điểm cố định"],a:0,why:"Electron di chuyển trong các lớp (vỏ) quanh hạt nhân."},
{lesson:2,q:"Đơn vị thường dùng để ghi khối lượng nguyên tử (đvt đại diện) là:",choices:["đvC (u) hoặc amu ✔","kg","mol","J"],a:0,why:"Đơn vị khối lượng nguyên tử thường ghi bằng đơn vị nguyên tử (u)."},


/* ===== BÀI 3: Nguyên tố hóa học ===== */
{lesson:3,q:"Nguyên tố hóa học là:",choices:["Các nguyên tử có cùng số proton (Z) ✔","Hợp chất tạo từ nhiều nguyên tố","Hỗn hợp của nhiều chất","Mẫu khoáng vật"],a:0,why:"Nguyên tố là tập hợp nguyên tử có cùng số proton."},
{lesson:3,q:"Ký hiệu hóa học của sắt là:",choices:["Fe ✔","Fs","Sr","Sf"],a:0,why:"Sắt có ký hiệu Fe (từ tiếng Latin Ferrum)."},
{lesson:3,q:"Đặc tính chung của kim loại là:",choices:["Dẫn điện và dẫn nhiệt tốt, có độ dẻo, bề mặt sáng ✔","Không dẫn điện, dễ vỡ","Luôn ở trạng thái khí ở điều kiện thường","Không phản ứng với axit"],a:0,why:"Kim loại thường dẫn điện, dẫn nhiệt tốt và có tính dẻo."},
{lesson:3,q:"Một nguyên tố không thể phân tách thành chất đơn giản hơn bằng phương pháp hóa học là:",choices:["Đúng ✔","Sai","Chỉ khi đun nóng","Chỉ trong phòng thí nghiệm"],a:0,why:"Định nghĩa: nguyên tố không thể tách thành chất đơn giản bằng phản ứng hóa học."},
{lesson:3,q:"Nguyên tố có 8 proton là:",choices:["O (Oxy) ✔","N (Nitơ)","C (Cacbon)","F (Flo)"],a:0,why:"Số proton = 8 tương ứng với oxy."},
{lesson:3,q:"Khí hiếm (khí trơ) thuộc nhóm nào trong bảng tuần hoàn?",choices:["Nhóm 18 (He, Ne, Ar...) ✔","Nhóm 1","Nhóm 2","Nhóm 17"],a:0,why:"Khí hiếm nằm ở nhóm 18, thường ít phản ứng."},


/* ===== BÀI 4: Sơ lược bản tuần hoàng các nguyên tố hóa học ===== */
{lesson:4,q:"Trong bảng tuần hoàn, 'nhóm' là gì?",choices:["Các cột dọc có tính chất hóa học tương tự ✔","Các hàng ngang có cùng số lớp electron","Các nguyên tố không liên quan","Những nguyên tố kim loại nặng"],a:0,why:"Nhóm = cột dọc; nguyên tố cùng nhóm có tính chất tương tự do cấu hình electron hóa trị giống nhau."},
{lesson:4,q:"'Chu kỳ' (period) trong bảng tuần hoàn là:",choices:["Hàng ngang, tương ứng số lớp electron ✔","Cột dọc","Các nguyên tố khí","Các nguyên tố phóng xạ"],a:0,why:"Chu kỳ = hàng ngang; số chu kỳ tương ứng số lớp electron."},
{lesson:4,q:"Độ âm điện (electronegativity) thường tăng theo hướng nào?",choices:["Tăng từ trái sang phải và tăng từ dưới lên trên ✔","Tăng từ phải sang trái","Tăng từ trên xuống dưới","Không thay đổi"],a:0,why:"Nhìn chung, độ âm điện tăng sang phải và lên trên bảng tuần hoàn."},
{lesson:4,q:"Nguyên tố thuộc nhóm 1 (kim loại kiềm) có đặc điểm:",choices:["Rất phản ứng, có một electron hóa trị ✔","Ít phản ứng, đầy đủ vỏ","Là khí hiếm","Luôn ở trạng thái lỏng"],a:0,why:"Kim loại kiềm (như Na, K) có 1 electron hóa trị, rất phản ứng, đặc biệt với nước."},
{lesson:4,q:"Các nguyên tố chuyển tiếp thường nằm ở:",choices:["Phần giữa của bảng (khối d) ✔","Bên phải bảng (phi kim)","Nhóm 18","Hàng cuối cùng"],a:0,why:"Nguyên tố chuyển tiếp nằm ở khối d giữa bảng tuần hoàn."},
{lesson:4,q:"Nguyên tố phi kim thường có tính chất nào?",choices:["Dễ hóa hợp, không dẫn điện tốt ✔","Dẫn điện tốt","Luôn có màu sáng kim","Là kim loại nặng"],a:0,why:"Phi kim thường cách điện, dễ nhận electron và tạo liên kết cộng hóa trị."},


/* ===== BÀI 5: Phân tử đơn chất, hợp chất ===== */
{lesson:5,q:"Phân tử đơn chất là gì?",choices:["Phân tử gồm các nguyên tử cùng loại (ví dụ O₂) ✔","Phân tử gồm nguyên tử khác loại (ví dụ H₂O)","Hỗn hợp nhiều chất","Hợp chất ion"],a:0,why:"Phân tử đơn chất gồm các nguyên tử cùng nguyên tố."},
{lesson:5,q:"Hợp chất là:",choices:["Chất gồm hai hay nhiều nguyên tố liên kết theo tỉ lệ xác định (ví dụ H₂O) ✔","Hỗn hợp các chất","Nguyên tố tinh khiết","Dung môi vô cơ"],a:0,why:"Hợp chất có tỉ lệ nguyên tố cố định và tính chất mới khác thành phần."},
{lesson:5,q:"Ví dụ phân tử đơn chất:",choices:["O₂ (oxy phân tử) ✔","H₂O (nước)","NaCl (muối ăn)","CO₂ (cacbonic)"],a:0,why:"O₂ gồm hai nguyên tử O — là phân tử của nguyên tố (đơn chất)."},
{lesson:5,q:"Nước muối (nước + muối) là:",choices:["Hỗn hợp (dung dịch) ✔","Hợp chất","Phân tử đơn chất","Nguyên tố"],a:0,why:"Nước muối là dung dịch, thành phần giữ tính chất riêng không biến thành một chất mới."},
{lesson:5,q:"Tỉ lệ các nguyên tố trong hợp chất có phải lúc nào cũng cố định?",choices:["Có (ví dụ H₂O luôn có 2 H và 1 O) ✔","Không, phụ thuộc nhiệt độ","Không, hợp chất thay đổi tùy lúc","Chỉ đúng với kim loại"],a:0,why:"Hợp chất có tỉ lệ nguyên tố cố định theo công thức phân tử."},
{lesson:5,q:"Phân tử được tạo bởi:",choices:["Các nguyên tử liên kết với nhau ✔","Nguyên tử rời rạc","Nguyên tố tinh khiết","Các ion tự do"],a:0,why:"Phân tử = đơn vị cấu trúc gồm nguyên tử liên kết."},


/* ===== BÀI 6: Giới thiệu về liên kết hóa học ===== */
{lesson:6,q:"Loại liên kết hình thành khi một nguyên tử chuyển electron cho nguyên tử khác là:",choices:["Liên kết ion (ion bond) ✔","Liên kết cộng hóa trị (covalent)","Liên kết kim loại","Liên kết hydro"],a:0,why:"Liên kết ion hình thành do trao đổi electron, tạo ion trái dấu hút nhau."},
{lesson:6,q:"Loại liên kết do hai nguyên tử chia sẻ electron là:",choices:["Liên kết cộng hóa trị ✔","Liên kết ion","Liên kết kim loại","Lực Van der Waals"],a:0,why:"Cộng hóa trị: chia sẻ electron để đạt cấu hình bền."},
{lesson:6,q:"Liên kết kim loại có đặc điểm:",choices:["Điện tử hóa trị 'chung' chuyển động tự do → dẫn điện tốt ✔","Không dẫn điện","Luôn yếu","Chỉ tồn tại ở nhiệt độ thấp"],a:0,why:"Trong kim loại, electron hóa trị delocalized giúp dẫn điện và dẻo."},
{lesson:6,q:"Nguyên nhân các nguyên tử liên kết là để:",choices:["Đạt cấu hình electron bền (thường giống khí hiếm) ✔","Tăng khối lượng nguyên tử","Giảm số proton","Tạo năng lượng âm"],a:0,why:"Liên kết giúp nguyên tử đạt cấu hình electron ổn định hơn."},
{lesson:6,q:"Trong phân tử H₂, hai H tạo liên kết gì?",choices:["Liên kết cộng hóa trị đơn (chia sẻ một cặp electron) ✔","Liên kết ion","Liên kết kim loại","Không liên kết"],a:0,why:"Hai nguyên tử H chia sẻ cặp electron tạo liên kết cộng hóa trị đơn."},
{lesson:6,q:"Na và Cl tạo NaCl qua cơ chế nào?",choices:["Trao electron → liên kết ion ✔","Chia sẻ electron → cộng hóa trị","Tạo liên kết kim loại","Không phản ứng"],a:0,why:"Na cho 1e cho Cl → Na⁺ và Cl⁻ tạo liên kết ion."},


/* ===== BÀI 7: Hóa trị và công thức hóa học ===== */
{lesson:7,q:"Hóa trị của một nguyên tử biểu thị:",choices:["Số electron tham gia liên kết (khả năng liên kết) ✔","Trọng lượng nguyên tử","Số nguyên tử trong phân tử","Độ pH của nguyên tố"],a:0,why:"Hóa trị cho biết khả năng liên kết (ví dụ H=1, O=2)."},
{lesson:7,q:"Hóa trị của H = 1, O = 2 → công thức phân tử của nước là:",choices:["H₂O ✔","HO","H₂O₂","OH"],a:0,why:"Để trung hòa hóa trị: 2 H (2×1) kết hợp 1 O (2) → H₂O."},
{lesson:7,q:"Công thức hóa học của natri clorua là:",choices:["NaCl ✔","NaCl₂","Na₂Cl","NCl"],a:0,why:"Natri (hóa trị 1) + Clo (hóa trị 1) → NaCl."},
{lesson:7,q:"Công thức phân tử của cacbon dioxide là:",choices:["CO₂ ✔","C₂O","CO","C₂O₂"],a:0,why:"C (hóa trị 4) + O (2) → CO₂ theo tỉ lệ cân bằng hóa trị."},
{lesson:7,q:"Khi viết công thức, tổng hóa trị các nguyên tố trong hợp chất phải:",choices:["Bằng 0 (trung hòa điện) trong hợp chất trung hòa ✔","Luôn dương","Luôn âm","Bằng tổng khối lượng"],a:0,why:"Tổng hóa trị phải cân bằng (trung hòa) nếu hợp chất không mang điện tích."},
{lesson:7,q:"Số oxi hóa và hóa trị có phải luôn giống nhau?",choices:["Không luôn giống nhau nhưng có liên quan ✔","Luôn giống nhau","Hoàn toàn khác nhau và không liên quan","Chỉ áp dụng cho kim loại"],a:0,why:"Số oxi hóa và hóa trị liên quan nhưng không phải lúc nào cũng trùng khớp."},


/* ===== BÀI 8: Tốc độ chuyển động ===== */
{lesson:8,q:"Tốc độ (speed) là đại lượng nào?",choices:["Đại lượng vô hướng (chỉ độ lớn) ✔","Đại lượng có hướng","Tương đương với quãng đường","Luôn có giá trị âm"],a:0,why:"Tốc độ là vô hướng, chỉ cho biết bao nhiêu khoảng cách đi được trên đơn vị thời gian."},
{lesson:8,q:"Công thức tính tốc độ trung bình (v):",choices:["v = quãng đường / thời gian (v = s / t) ✔","v = t / s","v = s × t","v = s² / t"],a:0,why:"Tốc độ trung bình = tổng quãng đường chia tổng thời gian."},
{lesson:8,q:"Đơn vị tốc độ trong SI thường dùng là:",choices:["m/s (mét trên giây) ✔","kg","J","mol"],a:0,why:"Đơn vị tiêu chuẩn tốc độ là m/s."},
{lesson:8,q:"36 km/h bằng bao nhiêu m/s?",choices:["10 m/s ✔","100 m/s","1 m/s","0.1 m/s"],a:0,why:"Chuyển đổi: 36 ÷ 3.6 = 10 m/s."},
{lesson:8,q:"Tốc độ tức thời khác tốc độ trung bình ở điểm nào?",choices:["Tốc độ tức thời là giá trị tại một thời điểm, trung bình là trên cả quãng đường/thời gian ✔","Giống hệt nhau luôn","Tốc độ tức thời là trung bình của nhiều lần đo","Chỉ dùng trong vật lý hạt"],a:0,why:"Tốc độ tức thời phản ánh vận tốc tại một thời điểm cụ thể."},
{lesson:8,q:"Vận tốc (velocity) khác tốc độ ở chỗ nào?",choices:["Vận tốc có hướng (vector), tốc độ không có hướng ✔","Vận tốc là vô hướng","Không khác gì","Vận tốc luôn dương"],a:0,why:"Vận tốc là đại lượng có hướng; đổi chiều thì vận tốc đổi dấu."},


/* ===== BÀI 9: Độ thủy khoảng đường thời gian ===== */
{lesson:9,q:"Trên đồ thị quãng đường - thời gian (s - t), độ dốc (slope) của đường biểu diễn thể hiện:",choices:["Tốc độ của vật ✔","Khả năng chịu lực","Lực tác dụng lên vật","Nhiệt độ môi trường"],a:0,why:"Độ dốc s-t = Δs/Δt = tốc độ trung bình trên đoạn đó."},
{lesson:9,q:"Đường thẳng nghiêng đều trên đồ thị s - t biểu thị:",choices:["Chuyển động thẳng đều (tốc độ không đổi) ✔","Chuyển động biến đổi đều","Vật đứng yên","Tốc độ tăng dần theo cấp số nhân"],a:0,why:"Đường thẳng với độ dốc không đổi → tốc độ không đổi."},
{lesson:9,q:"Nếu đồ thị s - t là đường cong, điều đó có nghĩa là:",choices:["Tốc độ thay đổi theo thời gian (không đều) ✔","Vật đứng yên","Đoạn đường là hằng số","Thời gian bằng 0"],a:0,why:"Đường cong cho thấy tốc độ biến đổi → có gia tốc."},
{lesson:9,q:"Phần vị trí nằm ở phía âm trên trục s (âm) biểu thị:",choices:["Vật nằm ở phía ngược chiều của mốc quy ước (độ dời âm) ✔","Vật đang tăng tốc dương","Vật bị mất năng lượng","Vật ở nơi không xác định"],a:0,why:"Giá trị vị trí âm nghĩa là vật ở phía quy ước ngược chiều."},
{lesson:9,q:"Đơn vị thường dùng để đo quãng đường trong chương trình là:",choices:["m (mét) ✔","kg","s","A"],a:0,why:"Quãng đường thường đo bằng mét (m)."},
{lesson:9,q:"Một vật chuyển động với v = 5 m/s trong 10 s thì quãng đường đi được là:",choices:["50 m ✔","5 m","500 m","0.5 m"],a:0,why:"s = v × t = 5 × 10 = 50 m."},


/* ===== BÀI 10: Đo tốc độ ===== */
{lesson:10,q:"Khi đo tốc độ bằng thước và đồng hồ bấm giây, nguồn sai số lớn nhất thường là:",choices:["Phản xạ của người bấm giờ và sai số đo khoảng cách ✔","Sai số do màu sắc của vật","Ảnh hưởng của âm thanh","Sai số do mùi phòng"],a:0,why:"Thời gian phản ứng của người bấm và đo khoảng cách không chính xác là nguồn sai số lớn."},
{lesson:10,q:"Chuyển 15 m/s sang km/h được bao nhiêu?",choices:["54 km/h ✔","5.4 km/h","150 km/h","40 km/h"],a:0,why:"Nhân m/s × 3.6 → 15 × 3.6 = 54 km/h."},
{lesson:10,q:"Để tăng độ chính xác khi đo tốc độ thực nghiệm nên:",choices:["Đo nhiều lần rồi lấy giá trị trung bình ✔","Đo chỉ một lần là đủ","Luôn rút kết luận từ một phép đo","Không quan tâm đến dụng cụ"],a:0,why:"Lấy trung bình nhiều lần giúp giảm sai số ngẫu nhiên."},
{lesson:10,q:"Để giảm ảnh hưởng của thời gian phản xạ, ta nên chọn đoạn đường đo:",choices:["Dài hơn để sai số thời gian ít ảnh hưởng tương đối ✔","Rất ngắn","Không thay đổi","Ngắn nhất có thể"],a:0,why:"Đo trên đoạn dài làm tỉ lệ sai số do phản xạ nhỏ đi."},
{lesson:10,q:"Thiết bị đo vận tốc tức thời trên ô tô gọi là:",choices:["Speedometer (đồng hồ tốc độ) ✔","Barometer","Thermometer","Hygrometer"],a:0,why:"Speedometer đo vận tốc tức thời trên xe."},
{lesson:10,q:"Một vật đi 20 m trong 4 s. Tốc độ trung bình là:",choices:["5 m/s ✔","0.2 m/s","80 m/s","24 m/s"],a:0,why:"v = s/t = 20/4 = 5 m/s."}
];

// ===== Utility =====
function shuffle(arr){for(let i=arr.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[arr[i],arr[j]]=[arr[j],arr[i]]}return arr}
function pick(lesson,count){
  let pool = lesson==="mix" ? bank.slice() : bank.filter(x=>x.lesson==lesson);
  shuffle(pool);
  if(lesson!=="mix"){
    // nếu bài có ít câu hơn yêu cầu, lặp vòng sao cho đủ (giữ trộn)
    const base = bank.filter(x=>x.lesson==lesson);
    while(pool.length<count){
      const add = shuffle(base.slice()).slice(0,Math.min(count-pool.length, base.length));
      pool = pool.concat(add);
    }
  }
  return pool.slice(0,count);
}
const quizBox = document.getElementById('quiz');
const resEl = document.getElementById('result');
const feedEl = document.getElementById('feedback');
const startBtn = document.getElementById('startBtn');
const checkBtn = document.getElementById('checkBtn');
const showKeyBtn = document.getElementById('showKeyBtn');
const retryBtn = document.getElementById('retryBtn');
const lessonSel = document.getElementById('lessonSel');
const numSel = document.getElementById('numSel');

let current=[], locked=false;

function render(){
  quizBox.innerHTML='';
  current.forEach((item,idx)=>{
    const card=document.createElement('div'); card.className='card';
    const title=document.createElement('div'); title.className='q';
    title.innerHTML=`<span class="pill">Bài ${item.lesson}</span> &nbsp; Câu ${idx+1}. ${item.q}`;
    const ans=document.createElement('div'); ans.className='ans';
    const order=[0,1,2,3]; shuffle(order);
    order.forEach((k,i)=>{
      const label=document.createElement('label');
      label.innerHTML=`<input type="radio" name="q${idx}" value="${k}"><span>${item.choices[k]}</span>`;
      ans.appendChild(label);
    });
    const why = document.createElement('div'); why.className='small muted'; why.style.display='none';
    why.textContent='💡 Gợi ý/giải thích: '+item.why;
    card.appendChild(title); card.appendChild(ans); card.appendChild(why);
    quizBox.appendChild(card);
  });
  resEl.textContent=''; feedEl.textContent='';
  locked=false;
  checkBtn.disabled=false; showKeyBtn.disabled=false; retryBtn.disabled=false;
}

startBtn.onclick=()=>{
  const lesson=lessonSel.value;
  const count=parseInt(numSel.value,10);
  current=pick(lesson,count);
  document.getElementById('status').textContent = lesson==='mix' ? 'Luyện tổng hợp' : `Bài ${lesson}`;
  render();
  // Kích hoạt nút chấm bài
  checkBtn.disabled=false; showKeyBtn.disabled=false; retryBtn.disabled=false;
};

checkBtn.onclick=()=>{
  if(locked) return;
  let correct=0;
  const cards=[...document.querySelectorAll('.card')];
  cards.forEach((card,idx)=>{
    const item=current[idx];
    const inputs=[...card.querySelectorAll('input[type=radio]')];
    const chosen=inputs.find(i=>i.checked);
    const labels=[...card.querySelectorAll('label')];
    // mark correct answers visually
    labels.forEach((lb,i)=>{
      const val = parseInt(lb.querySelector('input').value,10);
      if(val===item.a) lb.classList.add('correct');
    });
    if(chosen){
      const val=parseInt(chosen.value,10);
      if(val===item.a) correct++;
      else labels.find(lb=>lb.querySelector('input').checked).classList.add('wrong');
    }
    card.querySelector('.small').style.display='block';
  });
  const total=current.length;
  const pct=Math.round(correct/total*100);
  resEl.textContent=`🏁 Điểm: ${correct}/${total} (${pct}%)`;
  feedEl.textContent = pct>=85 ? "Tuyệt vời! Tiếp tục phát huy 💪" : pct>=60 ? "Ổn rồi, luyện thêm là bứt phá 🚀" : "Cần ôn lại trọng tâm, đừng nản nhé 🌱";
  locked=true;
};

showKeyBtn.onclick=()=>{
  const cards=[...document.querySelectorAll('.card')];
  cards.forEach((card,idx)=>{
    const item=current[idx];
    const labels=[...card.querySelectorAll('label')];
    labels.forEach(lb=>{
      const val=parseInt(lb.querySelector('input').value,10);
      if(val===item.a){ lb.classList.add('correct'); }
    });
    card.querySelector('.small').style.display='block';
  });
};

retryBtn.onclick=()=>{ startBtn.click(); };
</script>
</body>
</html>
