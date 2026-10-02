<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>QA Grid — Cuộc Gọi Chốt Lịch Hẹn · Pax Clinic</title>
<style>
:root {
  --blue: #1D5FAD; --blue-light: #E6F1FB; --blue-mid: #B5D4F4;
  --teal: #0F6E56; --teal-light: #E1F5EE;
  --red: #A32D2D; --red-light: #FCEBEB;
  --amber: #633806; --amber-light: #FAEEDA;
  --purple: #3C3489; --purple-light: #EEEDFE;
  --gray: #F5F4F0; --gray2: #E8E7E2; --gray3: #888780;
  --text: #1A1A1A; --text2: #555; --white: #fff;
  --radius: 10px; --shadow: 0 1px 4px rgba(0,0,0,0.08);
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}
* { box-sizing: border-box; margin: 0; padding: 0; }
body { background: #F0EFE9; color: var(--text); padding: 0 0 40px; min-height: 100vh; }

/* HEADER */
.header { background: var(--blue); padding: 20px 20px 16px; color: white; }
.header h1 { font-size: 18px; font-weight: 600; letter-spacing: .01em; }
.header p { font-size: 13px; opacity: .85; margin-top: 4px; line-height: 1.5; }
.score-bar { display: flex; gap: 10px; margin-top: 14px; flex-wrap: wrap; }
.score-pill { background: rgba(255,255,255,.18); border-radius: 20px; padding: 5px 14px; font-size: 13px; font-weight: 500; display: flex; align-items: center; gap: 6px; }
.score-num { font-size: 15px; font-weight: 700; }
.score-num.green { color: #7EE8A2; }
.score-num.amber { color: #FBBF24; }
.score-num.red { color: #FCA5A5; }

/* GUIDE BOX */
.guide-wrap { margin: 14px 14px 0; }
.guide-toggle { width: 100%; background: var(--white); border: none; border-radius: var(--radius); padding: 12px 16px; display: flex; align-items: center; justify-content: space-between; font-size: 13px; font-weight: 600; color: var(--blue); cursor: pointer; box-shadow: var(--shadow); }
.guide-body { background: var(--white); border-radius: 0 0 var(--radius) var(--radius); padding: 0 16px; max-height: 0; overflow: hidden; transition: max-height .3s ease, padding .3s; box-shadow: var(--shadow); }
.guide-body.open { max-height: 600px; padding: 12px 16px 14px; }
.guide-cols { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 12px; }
.guide-col h4 { font-size: 12px; font-weight: 600; color: var(--blue); margin-bottom: 6px; display: flex; align-items: center; gap: 5px; }
.guide-col ul { padding-left: 0; list-style: none; }
.guide-col ul li { font-size: 12px; color: var(--text2); padding: 3px 0; border-bottom: .5px solid var(--gray2); line-height: 1.5; display: flex; gap: 6px; }
.guide-col ul li::before { content: "•"; color: var(--blue); flex-shrink: 0; }

/* SECTION */
.section-wrap { margin: 14px 14px 0; }
.section-header { border-radius: var(--radius) var(--radius) 0 0; padding: 13px 16px; cursor: pointer; display: flex; align-items: center; justify-content: space-between; user-select: none; }
.section-header.s1 { background: #1D5FAD; color: white; }
.section-header.s2 { background: #FAEEDA; color: #412402; }
.section-header.s3 { background: #EEEDFE; color: #26215C; }
.section-title-wrap { flex: 1; }
.section-title { font-size: 14px; font-weight: 700; }
.section-sub { font-size: 11px; opacity: .8; margin-top: 2px; }
.section-score { font-size: 20px; font-weight: 700; background: rgba(255,255,255,.25); border-radius: 8px; padding: 4px 10px; margin-left: 10px; }
.chevron { font-size: 18px; transition: transform .25s; margin-left: 8px; }
.chevron.open { transform: rotate(180deg); }

.criteria-list { background: var(--white); border-radius: 0 0 var(--radius) var(--radius); overflow: hidden; box-shadow: var(--shadow); display: none; }
.criteria-list.open { display: block; }

/* CRITERIA ITEM */
.criteria-item { border-bottom: .5px solid var(--gray2); }
.criteria-item:last-child { border-bottom: none; }
.criteria-toggle { width: 100%; background: none; border: none; padding: 12px 16px; display: flex; align-items: flex-start; gap: 10px; cursor: pointer; text-align: left; }
.criteria-toggle:hover { background: var(--gray); }
.cri-left { flex: 1; }
.cri-num { font-size: 11px; font-weight: 600; color: var(--blue); margin-bottom: 2px; }
.cri-name { font-size: 13px; font-weight: 600; color: var(--text); line-height: 1.4; }
.cri-sub { font-size: 11px; color: var(--text2); margin-top: 1px; }
.hard-badge { display: inline-flex; align-items: center; gap: 3px; background: var(--red-light); color: var(--red); font-size: 10px; font-weight: 600; padding: 2px 7px; border-radius: 20px; margin-left: 6px; vertical-align: middle; }
.score-badge { flex-shrink: 0; font-size: 12px; font-weight: 700; padding: 3px 9px; border-radius: 20px; }
.score-badge.green { background: #DCFCE7; color: #14532D; }
.score-badge.amber { background: #FEF3C7; color: #78350F; }
.score-badge.blue { background: var(--blue-light); color: var(--blue); }
.score-badge.na { background: var(--gray2); color: var(--gray3); }
.cri-chevron { font-size: 16px; color: var(--gray3); transition: transform .2s; margin-top: 1px; flex-shrink: 0; }
.cri-chevron.open { transform: rotate(180deg); }

/* CRITERIA DETAIL */
.criteria-detail { display: none; background: var(--gray); padding: 0 16px 14px 42px; }
.criteria-detail.open { display: block; }
.detail-section { margin-top: 12px; }
.detail-label { font-size: 11px; font-weight: 600; color: var(--gray3); text-transform: uppercase; letter-spacing: .05em; margin-bottom: 5px; }
.detail-text { font-size: 12px; color: var(--text2); line-height: 1.6; }
.checklist { margin-top: 6px; }
.check-item { display: flex; align-items: flex-start; gap: 8px; padding: 5px 0; border-bottom: .5px solid var(--gray2); cursor: pointer; }
.check-item:last-child { border-bottom: none; }
.check-box { width: 16px; height: 16px; min-width: 16px; border-radius: 4px; border: 1.5px solid #C0BEB8; margin-top: 1px; display: flex; align-items: center; justify-content: center; transition: all .15s; flex-shrink: 0; }
.check-box.checked { background: var(--teal); border-color: var(--teal); }
.check-box.checked::after { content: ''; display: block; width: 8px; height: 5px; border-left: 1.5px solid white; border-bottom: 1.5px solid white; transform: rotate(-45deg) translateY(-1px); }
.check-label { font-size: 12px; color: var(--text2); line-height: 1.5; flex: 1; }
.check-label.checked { color: #AAAAAA; text-decoration: line-through; }
.hard-dot { color: var(--red); font-size: 11px; font-weight: 700; flex-shrink: 0; }

/* BẢNG TỪ CHỐI */
.rejection-wrap { margin: 14px 14px 0; }
.rejection-header { background: #712B13; color: white; border-radius: var(--radius) var(--radius) 0 0; padding: 12px 16px; cursor: pointer; display: flex; align-items: center; justify-content: space-between; }
.rejection-header .rh-title { font-size: 13px; font-weight: 700; }
.rejection-header .rh-sub { font-size: 11px; opacity: .8; margin-top: 1px; }
.rejection-list { background: var(--white); border-radius: 0 0 var(--radius) var(--radius); overflow: hidden; box-shadow: var(--shadow); display: none; }
.rejection-list.open { display: block; }
.rejection-item { border-bottom: .5px solid var(--gray2); }
.rejection-item:last-child { border-bottom: none; }
.rej-toggle { width: 100%; background: none; border: none; padding: 11px 16px; display: flex; align-items: center; gap: 10px; cursor: pointer; text-align: left; }
.rej-toggle:hover { background: var(--gray); }
.rej-type { font-size: 12px; font-weight: 600; color: var(--red); flex: 1; }
.rej-detail { display: none; background: var(--red-light); padding: 10px 16px 12px; }
.rej-detail.open { display: block; }
.rej-label { font-size: 10px; font-weight: 600; color: var(--red); text-transform: uppercase; letter-spacing: .05em; margin-bottom: 3px; }
.rej-text { font-size: 12px; color: #4A1B0C; line-height: 1.6; margin-bottom: 8px; }
.rej-script { background: white; border-left: 3px solid var(--red); border-radius: 0 6px 6px 0; padding: 8px 10px; font-size: 12px; color: var(--text2); font-style: italic; line-height: 1.5; }

/* ĐIỂM KHÓ */
.hard-wrap { margin: 14px 14px 0; }
.hard-header { background: #3C3489; color: white; border-radius: var(--radius) var(--radius) 0 0; padding: 12px 16px; cursor: pointer; display: flex; align-items: center; justify-content: space-between; }
.hard-header .hh-title { font-size: 13px; font-weight: 700; }
.hard-header .hh-sub { font-size: 11px; opacity: .8; margin-top: 1px; }
.hard-list { background: var(--white); border-radius: 0 0 var(--radius) var(--radius); overflow: hidden; box-shadow: var(--shadow); display: none; }
.hard-list.open { display: block; }
.hard-item { border-bottom: .5px solid var(--gray2); padding: 13px 16px; }
.hard-item:last-child { border-bottom: none; }
.hard-item-title { font-size: 12px; font-weight: 700; color: var(--purple); margin-bottom: 6px; display: flex; align-items: center; gap: 6px; }
.hard-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; }
.hard-cell-label { font-size: 10px; font-weight: 600; color: var(--gray3); text-transform: uppercase; letter-spacing: .05em; margin-bottom: 3px; }
.hard-cell-text { font-size: 12px; color: var(--text2); line-height: 1.5; }
.hard-fix { background: var(--teal-light); border-radius: 6px; padding: 8px 10px; margin-top: 8px; }
.hard-fix-label { font-size: 10px; font-weight: 700; color: var(--teal); text-transform: uppercase; letter-spacing: .05em; margin-bottom: 3px; }
.hard-fix-text { font-size: 12px; color: #04342C; line-height: 1.5; }

/* PROGRESS */
.progress-wrap { margin: 14px 14px 0; background: var(--white); border-radius: var(--radius); padding: 14px 16px; box-shadow: var(--shadow); }
.progress-title { font-size: 13px; font-weight: 600; color: var(--text); margin-bottom: 10px; display: flex; justify-content: space-between; align-items: center; }
.progress-count { font-size: 12px; color: var(--gray3); font-weight: 400; }
.progress-bar-wrap { background: var(--gray2); border-radius: 99px; height: 8px; overflow: hidden; }
.progress-bar { height: 8px; border-radius: 99px; background: var(--teal); transition: width .3s; }
.section-progress { margin-bottom: 10px; }
.section-progress:last-child { margin-bottom: 0; }
.sp-label { font-size: 11px; color: var(--text2); margin-bottom: 4px; display: flex; justify-content: space-between; }
</style>
</head>
<body>

<div class="header">
  <h1>QA Grid — Cuộc Gọi Chốt Lịch Hẹn</h1>
  <p>Pax Clinic · Mục tiêu: Chốt lịch khám</p>
  <div class="score-bar">
    <div class="score-pill">Tổng <span class="score-num amber" id="total-score">0%</span></div>
    <div class="score-pill">Phần 1 <span class="score-num amber" id="s1-score">0%</span></div>
    <div class="score-pill">Phần 2 <span class="score-num amber" id="s2-score">0%</span></div>
    <div class="score-pill">Phần 3 <span class="score-num amber" id="s3-score">0%</span></div>
  </div>
</div>

<!-- PROGRESS -->
<div class="progress-wrap">
  <div class="progress-title">Tiến độ hoàn thành checklist <span class="progress-count" id="prog-count">0 / 0 mục</span></div>
  <div class="section-progress">
    <div class="sp-label"><span>Phần 1 — Customers outcome & impact</span><span id="p1-pct">0%</span></div>
    <div class="progress-bar-wrap"><div class="progress-bar" id="p1-bar" style="width:0%"></div></div>
  </div>
  <div class="section-progress">
    <div class="sp-label"><span>Phần 2 — Customers relationship & trust</span><span id="p2-pct">0%</span></div>
    <div class="progress-bar-wrap"><div class="progress-bar" id="p2-bar" style="width:0%"></div></div>
  </div>
  <div class="section-progress">
    <div class="sp-label"><span>Phần 3 — Customer Continuity & Compliance</span><span id="p3-pct">0%</span></div>
    <div class="progress-bar-wrap"><div class="progress-bar" id="p3-bar" style="width:0%"></div></div>
  </div>
</div>

<!-- HƯỚNG DẪN -->
<div class="guide-wrap">
  <button class="guide-toggle" onclick="toggleGuide()">
    <span>📌 Hướng dẫn sử dụng QA Grid</span>
    <span id="guide-chevron" class="chevron">▾</span>
  </button>
  <div class="guide-body" id="guide-body">
    <div class="guide-cols">
      <div class="guide-col">
        <h4>🎯 Mục tiêu cuộc gọi</h4>
        <ul>
          <li>① Tìm hiểu nhanh vấn đề khách</li>
          <li>② Tạo hook — lý do phải đến khám</li>
          <li>③ Chốt ngày giờ trước khi cúp máy</li>
        </ul>
      </div>
      <div class="guide-col">
        <h4>⏱ Thời lượng lý tưởng</h4>
        <ul>
          <li>Tổng cuộc gọi: 5–10 phút</li>
          <li>Tìm hiểu vấn đề: 2–3 phút</li>
          <li>Tạo hook & đề xuất: 2–3 phút</li>
          <li>Chốt lịch & kết thúc: 1–2 phút</li>
        </ul>
      </div>
      <div class="guide-col">
        <h4>☑ Cách dùng checklist</h4>
        <ul>
          <li>Tick trước mỗi cuộc gọi để nhắc nhở</li>
          <li>Sau call: supervisor review những gì đạt</li>
          <li>Phần 1 là quan trọng</li>
          <li>🔴 Điểm khó — cần chú ý đặc biệt</li>
        </ul>
      </div>
    </div>
  </div>
</div>

<!-- PHẦN 1 -->
<div class="section-wrap">
  <div class="section-header s1" onclick="toggleSection('s1')">
    <div class="section-title-wrap">
      <div class="section-title">PHẦN 1 — Customers outcome & impact</div>
      <div class="section-sub">Quan trọng nhất — bắt buộc đạt · 7 tiêu chí</div>
    </div>
    <span class="chevron open" id="s1-chev">▾</span>
  </div>
  <div class="criteria-list open" id="s1-list">

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c11')">
        <div class="cri-left">
          <div class="cri-num">1.1</div>
          <div class="cri-name">Mở đầu cuộc gọi</div>
          <div class="cri-sub">Tạo ấn tượng chuyên nghiệp & an toàn ngay từ đầu</div>
        </div>
        <span class="cri-chevron" id="c11-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c11">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Mở đầu trong vòng 30 giây: nói tên, tên phòng khám, lý do gọi. Hỏi xác nhận khách có thể nói chuyện ngay bây giờ không.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Giới thiệu rõ: tên, bác sĩ / chuyên viên tại Pax Clinic</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Hỏi: "Bạn có đang tiện nghe máy không ạ?" trước khi vào nội dung</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nhắc lại lý do khách để lại thông tin (bài đăng / quảng cáo nào)</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không đọc script cứng nhắc — nghe tự nhiên, ấm áp</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không tiết lộ thông tin nhạy cảm khi chưa xác minh đúng người</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c12')">
        <div class="cri-left">
          <div class="cri-num">1.2</div>
          <div class="cri-name">Khám phá & Kết nối <span class="hard-badge">🔴 Khó nhất</span></div>
          <div class="cri-sub">Hỏi đúng để hiểu vấn đề nhanh</div>
        </div>
        <span class="cri-chevron" id="c12-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c12">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Hỏi tối đa 3–4 câu mở để xác định: (1) Vấn đề chính, (2) Đã kéo dài bao lâu, (3) Ảnh hưởng đến sinh hoạt như thế nào. Không hỏi quá nhiều, không tư vấn ngay.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Hỏi câu mở: "Bạn đang gặp khó khăn gì khiến bạn quan tâm đến sức khoẻ tâm lý vậy?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Lắng nghe trọn vẹn — KHÔNG ngắt lời hoặc vội vàng đưa ra giải pháp</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Xác nhận đã hiểu: "Mình hiểu rồi, vậy bạn đang..." (tóm tắt lại ngắn gọn)</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Hỏi thêm: "Tình trạng này đã kéo dài bao lâu rồi ạ?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Hỏi ảnh hưởng: "Điều này có ảnh hưởng đến công việc / giấc ngủ / các mối quan hệ không?"</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c13')">
        <div class="cri-left">
          <div class="cri-num">1.3</div>
          <div class="cri-name">Tạo nhận thức & Hook <span class="hard-badge">🔴 Khó nhất</span></div>
          <div class="cri-sub">Lý do khách PHẢI đến khám</div>
        </div>
        <span class="cri-chevron" id="c13-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c13">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Dùng thông tin khách vừa chia sẻ để nói: "Với những gì bạn mô tả, đây là điều tôi muốn đánh giá kỹ hơn cho bạn..." — tạo cảm giác cần thiết và cá nhân hoá, không phán xét.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Kết nối vấn đề khách nói với lý do cụ thể cần đến khám</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Không chẩn đoán qua điện thoại — nói: "Để xác định chính xác, tôi cần gặp trực tiếp"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Dùng ngôn ngữ tạo sự cấp thiết nhẹ nhàng: "Những dấu hiệu như vậy nếu để lâu có thể..."</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Đề cao giá trị buổi khám đầu tiên: "Buổi đầu tiên chỉ để lắng nghe và đánh giá toàn diện"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không dùng thuật ngữ y khoa nặng — giữ ngôn ngữ gần gũi, không khiến khách sợ</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Câu kết: "Tôi muốn gặp bạn để chúng ta hiểu rõ hơn và có hướng giúp bạn cụ thể"</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c14')">
        <div class="cri-left">
          <div class="cri-num">1.4</div>
          <div class="cri-name">Đề xuất buổi khám</div>
          <div class="cri-sub">Giới thiệu đúng dịch vụ phù hợp với vấn đề</div>
        </div>
        <span class="cri-chevron" id="c14-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c14">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Đề xuất dịch vụ cụ thể, giải thích quy trình buổi đầu ngắn gọn (Pax Clinic làm gì trong buổi đầu, kéo dài bao lâu, điều gì xảy ra sau đó). Tạo cảm giác rõ ràng và an toàn.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Đề xuất đúng dịch vụ phù hợp với vấn đề khách đang gặp</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Giải thích buổi đầu gồm gì: "Buổi đầu khoảng 60 phút, bác sĩ sẽ lắng nghe và đánh giá..."</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nêu tên bác sĩ / chuyên viên sẽ tiếp nhận nếu có thể</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Giải thích địa chỉ và cách đến Pax Clinic nếu khách hỏi</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c15')">
        <div class="cri-left">
          <div class="cri-num">1.5</div>
          <div class="cri-name">Chốt lịch hẹn <span class="hard-badge">🔴 Khó nhất</span></div>
          <div class="cri-sub">Kỹ năng sales quan trọng nhất</div>
        </div>
        <span class="cri-chevron" id="c15-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c15">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Đề xuất 2 lựa chọn thời gian cụ thể (technique: "Anh/chị tiện buổi sáng hay chiều?"), xác nhận lịch, và nhắc lại thông tin lịch hẹn trước khi kết thúc call.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Chủ động đề xuất lịch: "Bạn có thể đến Pax Clinic vào thứ X hoặc Y tuần này không?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Dùng kỹ thuật 2 lựa chọn: "Sáng hay chiều tiện hơn cho bạn?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Xác nhận lịch hẹn rõ ràng: ngày / giờ / địa chỉ</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Nếu khách do dự: không bỏ qua — hỏi lý do và xử lý (xem tiêu chí 1.6)</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nhắc lại lịch hẹn trước khi cúp máy: "Vậy mình gặp nhau lúc X ngày Y tại Pax Clinic nhé"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Hỏi: "Bạn có muốn mình gửi tin nhắn xác nhận lịch không?"</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c16')">
        <div class="cri-left">
          <div class="cri-num">1.6</div>
          <div class="cri-name">Xử lý từ chối & Rào cản <span class="hard-badge">🔴 Khó nhất</span></div>
          <div class="cri-sub">Không bỏ cuộc quá sớm</div>
        </div>
        <span class="cri-chevron" id="c16-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c16">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Khi khách nêu lý do từ chối: xác nhận đã nghe (empathy), hỏi thêm để hiểu rào cản thật sự, và đưa ra phản hồi cụ thể giúp khách vượt qua rào cản đó.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Nhận diện đúng loại từ chối: bận / chi phí / ngại / chưa sẵn sàng</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Phản hồi đúng từng loại — xem bảng xử lý từ chối bên dưới</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">"Bạn muốn suy nghĩ thêm" → hỏi: "Có điều gì bạn còn băn khoăn không?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">"Bận" → "Tuần sau bạn tiện hơn không? Mình đặt lịch linh hoạt được"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">"Chi phí" → Giải thích giá trị buổi đầu tiên / chi phí cụ thể nếu biết</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">Nếu khách thật sự chưa sẵn sàng: hỏi cho phép theo dõi sau 1 tuần</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không tạo áp lực quá mức — giữ cảm giác hỗ trợ, không phải bán hàng</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c17')">
        <div class="cri-left">
          <div class="cri-num">1.7</div>
          <div class="cri-name">Kết thúc cuộc gọi</div>
          <div class="cri-sub">Đảm bảo rõ ràng & tạo kỳ vọng cho bước tiếp theo</div>
        </div>
        <span class="cri-chevron" id="c17-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c17">
        <div class="detail-section">
          <div class="detail-label">Kỳ vọng</div>
          <div class="detail-text">Tóm tắt ngắn gọn: lịch hẹn đã đặt (hoặc sẽ gọi lại khi nào), bước tiếp theo khách cần làm. Đảm bảo không có câu hỏi nào còn bỏ ngỏ.</div>
        </div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="1">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Tóm tắt lịch hẹn: "Vậy mình gặp nhau lúc [giờ] ngày [ngày] tại Pax Clinic"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nhắc địa chỉ một lần nữa hoặc hỏi có cần hướng dẫn đường không</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Xác nhận sẽ gửi tin nhắn nhắc lịch qua Zalo / SMS</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nếu chưa chốt: nói rõ khi nào sẽ gọi lại hoặc khách nên liên lạc kênh nào</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Kết thúc ấm áp: "Bạn cứ yên tâm, đội ngũ Pax Clinic sẽ đồng hành cùng bạn"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="hard-dot">🔴</span><span class="check-label">KHÔNG kết thúc call khi chưa có kết quả: lịch hẹn HOẶC lịch gọi lại</span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- PHẦN 2 -->
<div class="section-wrap">
  <div class="section-header s2" onclick="toggleSection('s2')">
    <div class="section-title-wrap">
      <div class="section-title">PHẦN 2 — Customers relationship & trust</div>
      <div class="section-sub">Trải nghiệm khách trong cuộc gọi · 4 tiêu chí</div>
    </div>
    <span class="chevron" id="s2-chev">▾</span>
  </div>
  <div class="criteria-list" id="s2-list">

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c21')">
        <div class="cri-left">
          <div class="cri-num">2.1</div>
          <div class="cri-name">Cấu trúc & Dẫn dắt cuộc gọi</div>
          <div class="cri-sub">Làm chủ nhịp cuộc trò chuyện</div>
        </div>
        <span class="cri-chevron" id="c21-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c21">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Giữ cuộc gọi trong 5–10 phút. Chuyển từng phần một cách tự nhiên, không đột ngột. Ưu tiên thời gian cho phần chốt lịch.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="2">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Cuộc gọi có cấu trúc rõ ràng: mở đầu → tìm hiểu → hook → chốt</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không để khách kể quá dài mà quên mục tiêu chính của call</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Chủ động chuyển sang đề xuất lịch khi đã hiểu đủ vấn đề</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ưu tiên thời gian: không dành quá 3 phút cho phần khám phá</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Tự tin dẫn dắt — không bị động theo chiều khách kéo</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c22')">
        <div class="cri-left">
          <div class="cri-num">2.2</div>
          <div class="cri-name">Giao tiếp rõ ràng & Dễ hiểu</div>
          <div class="cri-sub">Nói để khách hiểu, không để thể hiện</div>
        </div>
        <span class="cri-chevron" id="c22-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c22">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Giải thích bất kỳ khái niệm nào bằng ví dụ dễ hiểu. Kiểm tra khách đã hiểu khi cần. Tốc độ nói vừa phải, giọng ấm và tự tin.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="2">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nói bằng ngôn ngữ đời thường, không dùng thuật ngữ chuyên ngành</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Tốc độ nói vừa phải — không quá nhanh khi thông báo lịch hẹn</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Kiểm tra hiểu biết: "Bạn có muốn mình giải thích thêm không?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Tránh dùng câu quá dài hoặc phức tạp</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c23')">
        <div class="cri-left">
          <div class="cri-num">2.3</div>
          <div class="cri-name">Lắng nghe & Đồng cảm</div>
          <div class="cri-sub">Khách cảm thấy được nghe và không bị phán xét</div>
        </div>
        <span class="cri-chevron" id="c23-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c23">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Biểu hiện đồng cảm khi khách chia sẻ khó khăn. Không phán xét. Khuyến khích khách tiếp tục chia sẻ bằng câu hỏi mở và xác nhận nhẹ nhàng.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="2">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không ngắt lời khi khách đang chia sẻ cảm xúc</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Phản hồi đồng cảm: "Mình hiểu điều đó khá khó khăn với bạn"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không phán xét hoặc so sánh với người khác</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Khuyến khích: "Bạn không cần lo lắng — chia sẻ thế này là đúng rồi"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Biết khi nào nên dừng hỏi và chuyển sang đề xuất</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c24')">
        <div class="cri-left">
          <div class="cri-num">2.4</div>
          <div class="cri-name">Chuyên nghiệp & Tôn trọng</div>
          <div class="cri-sub">Đại diện xứng đáng cho thương hiệu Pax Clinic</div>
        </div>
        <span class="cri-chevron" id="c24-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c24">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Lịch sự và tôn trọng từ đầu đến cuối. Xưng hô phù hợp (anh/chị). Không tạo cảm giác bán hàng quá lộ liễu.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="2">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Xưng hô phù hợp: anh/chị theo tuổi và ngữ cảnh</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Lịch sự, không vội vàng hay tỏ thái độ khi khách do dự</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không nói xấu phòng khám khác hoặc so sánh</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Giữ bí mật thông tin khách — không chia sẻ với bên thứ ba</span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- PHẦN 3 -->
<div class="section-wrap">
  <div class="section-header s3" onclick="toggleSection('s3')">
    <div class="section-title-wrap">
      <div class="section-title">PHẦN 3 — Customer Continuity & Compliance</div>
      <div class="section-sub">Sau cuộc gọi & hệ thống · 4 tiêu chí</div>
    </div>
    <span class="chevron" id="s3-chev">▾</span>
  </div>
  <div class="criteria-list" id="s3-list">

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c31')">
        <div class="cri-left">
          <div class="cri-num">3.1</div>
          <div class="cri-name">Lên lịch theo dõi</div>
          <div class="cri-sub">Không để khách bị mất sau cuộc gọi</div>
        </div>
        <span class="cri-chevron" id="c31-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c31">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Mọi cuộc gọi đều phải có bước kế tiếp rõ ràng: lịch hẹn đã đặt hoặc lịch gọi lại. Không kết thúc mà không có cam kết nào.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="3">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Đã chốt lịch → Xác nhận sẽ gửi SMS/Zalo nhắc lịch trước 24h</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Chưa chốt → Hỏi: "Mình có thể gọi lại cho bạn vào [ngày] không?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi lại thời gian gọi lại và thực hiện đúng hẹn</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nhắn tin xác nhận lịch ngay sau khi kết thúc call (nếu đã chốt)</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c32')">
        <div class="cri-left">
          <div class="cri-num">3.2</div>
          <div class="cri-name">Ghi chú sau cuộc gọi</div>
          <div class="cri-sub">Lưu đủ thông tin để follow-up hiệu quả</div>
        </div>
        <span class="cri-chevron" id="c32-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c32">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Ghi chú đủ để người khác có thể tiếp quản: tên khách, vấn đề, kết quả call, bước tiếp theo. Không ghi chú chung chung.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="3">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi tên khách, SĐT, nguồn (bài đăng nào), ngày giờ gọi</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi vấn đề chính khách đang gặp (1–2 dòng ngắn gọn)</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi kết quả: đã chốt lịch / gọi lại / từ chối / không liên lạc được</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi ngày giờ lịch hẹn đã đặt hoặc ngày gọi lại</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Ghi note đặc biệt: khách nhạy cảm / cần tiếp cận thêm cẩn thận</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c33')">
        <div class="cri-left">
          <div class="cri-num">3.3</div>
          <div class="cri-name">Nhắn tin sau cuộc gọi</div>
          <div class="cri-sub">Duy trì kết nối và nhắc lịch</div>
        </div>
        <span class="cri-chevron" id="c33-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c33">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Tin nhắn xác nhận ngắn gọn, đủ thông tin: tên phòng khám, địa chỉ, ngày giờ, số điện thoại liên hệ nếu cần thay đổi.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="3">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Gửi tin nhắn xác nhận trong vòng 10 phút sau call</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Nội dung: tên PK, địa chỉ, ngày giờ lịch hẹn, số điện thoại</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Gửi nhắc lịch 24h trước buổi hẹn</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Gửi nhắc lịch 2h trước buổi hẹn</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Hỏi lại nếu khách chưa xác nhận sau 24h</span></div>
          </div>
        </div>
      </div>
    </div>

    <div class="criteria-item">
      <button class="criteria-toggle" onclick="toggleCriteria('c34')">
        <div class="cri-left">
          <div class="cri-num">3.4</div>
          <div class="cri-name">Bảo mật thông tin</div>
          <div class="cri-sub">Bảo vệ khách hàng và phòng khám</div>
        </div>
        <span class="cri-chevron" id="c34-chev">▾</span>
      </button>
      <div class="criteria-detail" id="c34">
        <div class="detail-section"><div class="detail-label">Kỳ vọng</div><div class="detail-text">Xác minh danh tính trước khi trao đổi. Không ghi âm nếu không được phép. Không chia sẻ thông tin chẩn đoán hoặc hồ sơ qua điện thoại.</div></div>
        <div class="detail-section">
          <div class="detail-label">Checklist</div>
          <div class="checklist" data-section="3">
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Xác nhận đang nói đúng người: "Tôi đang nói chuyện với [tên] đúng không ạ?"</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không chia sẻ thông tin nhạy cảm nếu không xác minh được</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Không nói tên hay vấn đề của khách khi có người thứ ba nghe</span></div>
            <div class="check-item" onclick="toggleCheck(this)"><div class="check-box"></div><span class="check-label">Tuân thủ quy định bảo mật thông tin y tế của Pax Clinic</span></div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- BẢNG XỬ LÝ TỪ CHỐI -->
<div class="rejection-wrap">
  <div class="rejection-header" onclick="toggleRejection()">
    <div>
      <div class="rh-title">🚧 Bảng xử lý từ chối</div>
      <div class="rh-sub">Dùng khi khách chưa đồng ý đặt lịch — 5 tình huống thường gặp</div>
    </div>
    <span class="chevron" id="rej-chev">▾</span>
  </div>
  <div class="rejection-list" id="rej-list">
    <div class="rejection-item">
      <button class="rej-toggle" onclick="toggleRej('r1')"><span class="rej-type">😓 "Tôi bận, không có thời gian"</span><span class="cri-chevron" id="r1-chev">▾</span></button>
      <div class="rej-detail" id="r1">
        <div class="rej-label">Cách phản hồi</div>
        <div class="rej-text">Không từ bỏ — hỏi thời gian linh hoạt hơn. Đề xuất lịch sớm hoặc cuối tuần.</div>
        <div class="rej-label">Câu nói mẫu</div>
        <div class="rej-script">"Mình hiểu bạn bận. Pax Clinic có lịch sáng sớm 8h và cuối tuần. Tuần sau bạn có 60 phút rảnh không?"</div>
      </div>
    </div>
    <div class="rejection-item">
      <button class="rej-toggle" onclick="toggleRej('r2')"><span class="rej-type">🤔 "Tôi muốn suy nghĩ thêm"</span><span class="cri-chevron" id="r2-chev">▾</span></button>
      <div class="rej-detail" id="r2">
        <div class="rej-label">Cách phản hồi</div>
        <div class="rej-text">Hỏi thêm để hiểu rào cản thật sự. Đặt lịch tạm và cho phép đổi lịch.</div>
        <div class="rej-label">Câu nói mẫu</div>
        <div class="rej-script">"Bạn còn băn khoăn điều gì không? Mình có thể đặt lịch tạm, nếu không tiện bạn báo mình đổi được."</div>
      </div>
    </div>
    <div class="rejection-item">
      <button class="rej-toggle" onclick="toggleRej('r3')"><span class="rej-type">💰 "Chi phí khám có đắt không?"</span><span class="cri-chevron" id="r3-chev">▾</span></button>
      <div class="rej-detail" id="r3">
        <div class="rej-label">Cách phản hồi</div>
        <div class="rej-text">Giải thích cụ thể chi phí. Đề cao giá trị buổi đầu tiên. Không so sánh.</div>
        <div class="rej-label">Câu nói mẫu</div>
        <div class="rej-script">"Buổi đầu tiên là [giá] và bao gồm đánh giá toàn diện. Đây là bước quan trọng để hiểu đúng bạn cần gì."</div>
      </div>
    </div>
    <div class="rejection-item">
      <button class="rej-toggle" onclick="toggleRej('r4')"><span class="rej-type">😰 "Tôi ngại đến phòng khám tâm lý"</span><span class="cri-chevron" id="r4-chev">▾</span></button>
      <div class="rej-detail" id="r4">
        <div class="rej-label">Cách phản hồi</div>
        <div class="rej-text">Chuẩn hoá trải nghiệm, giảm kỳ thị. Mô tả phòng khám như nơi an toàn.</div>
        <div class="rej-label">Câu nói mẫu</div>
        <div class="rej-script">"Rất nhiều người cảm thấy vậy lần đầu. Pax Clinic là không gian riêng tư, ấm áp — không phải bệnh viện."</div>
      </div>
    </div>
    <div class="rejection-item">
      <button class="rej-toggle" onclick="toggleRej('r5')"><span class="rej-type">💪 "Tôi tự xử lý được"</span><span class="cri-chevron" id="r5-chev">▾</span></button>
      <div class="rej-detail" id="r5">
        <div class="rej-label">Cách phản hồi</div>
        <div class="rej-text">Tôn trọng nhưng tạo nhận thức về giới hạn tự xử lý. Không ép buộc.</div>
        <div class="rej-label">Câu nói mẫu</div>
        <div class="rej-script">"Mình hiểu và tôn trọng điều đó. Nếu bạn thấy khó khăn hơn, Pax Clinic luôn sẵn sàng. Mình gửi thông tin để bạn tham khảo nhé?"</div>
      </div>
    </div>
  </div>
</div>

<!-- PHÂN TÍCH ĐIỂM KHÓ -->
<div class="hard-wrap">
  <div class="hard-header" onclick="toggleHard()">
    <div>
      <div class="hh-title">⚠️ Phân tích điểm khó nhất — Bác sĩ cần chú ý đặc biệt</div>
      <div class="hh-sub">4 điểm khó trong thực tế + cách khắc phục cụ thể</div>
    </div>
    <span class="chevron" id="hard-chev">▾</span>
  </div>
  <div class="hard-list" id="hard-list">
    <div class="hard-item">
      <div class="hard-item-title"><span style="background:#FCEBEB;color:#A32D2D;padding:2px 8px;border-radius:20px;font-size:11px">1.3</span> Tạo Hook — Lý do phải đến khám</div>
      <div class="hard-grid">
        <div><div class="hard-cell-label">Tại sao khó</div><div class="hard-cell-text">Bác sĩ quen tư vấn y khoa — khó tạo urgency mà không phán xét hay chẩn đoán sớm</div></div>
        <div><div class="hard-cell-label">Biểu hiện thường gặp</div><div class="hard-cell-text">Hay nói quá chung chung: "Bạn nên đến khám" mà không có lý do cụ thể từ vấn đề khách</div></div>
      </div>
      <div class="hard-fix"><div class="hard-fix-label">✅ Cách khắc phục</div><div class="hard-fix-text">Dùng chính lời khách nói: "Với [điều X] bạn vừa nói, đây chính xác là điều tôi cần đánh giá kỹ cho bạn"</div></div>
    </div>
    <div class="hard-item">
      <div class="hard-item-title"><span style="background:#FCEBEB;color:#A32D2D;padding:2px 8px;border-radius:20px;font-size:11px">1.5</span> Chốt lịch — Kỹ năng sales</div>
      <div class="hard-grid">
        <div><div class="hard-cell-label">Tại sao khó</div><div class="hard-cell-text">Bác sĩ không được đào tạo sales — ngại đề xuất trực tiếp, sợ khách cảm thấy bị ép</div></div>
        <div><div class="hard-cell-label">Biểu hiện thường gặp</div><div class="hard-cell-text">Kết thúc call bằng "bạn suy nghĩ thêm nhé" mà không đề xuất lịch cụ thể — khách lạnh dần</div></div>
      </div>
      <div class="hard-fix"><div class="hard-fix-label">✅ Cách khắc phục</div><div class="hard-fix-text">Thực hành câu cứng: "Tôi muốn đặt lịch cho bạn ngay. Thứ X hay Y tuần này bạn tiện hơn?"</div></div>
    </div>
    <div class="hard-item">
      <div class="hard-item-title"><span style="background:#FCEBEB;color:#A32D2D;padding:2px 8px;border-radius:20px;font-size:11px">1.6</span> Xử lý từ chối — Không bỏ cuộc sớm</div>
      <div class="hard-grid">
        <div><div class="hard-cell-label">Tại sao khó</div><div class="hard-cell-text">Bác sĩ coi từ chối là quyết định của khách — không muốn "ép" vì tôn trọng tự chủ</div></div>
        <div><div class="hard-cell-label">Biểu hiện thường gặp</div><div class="hard-cell-text">Ngay khi nghe "tôi suy nghĩ thêm" là đồng ý và kết thúc — không hỏi thêm</div></div>
      </div>
      <div class="hard-fix"><div class="hard-fix-label">✅ Cách khắc phục</div><div class="hard-fix-text">Phân biệt: từ chối thật (khách thật sự không muốn) vs rào cản (có thể tháo gỡ). Luôn hỏi thêm 1 câu</div></div>
    </div>
    <div class="hard-item">
      <div class="hard-item-title"><span style="background:#FCEBEB;color:#A32D2D;padding:2px 8px;border-radius:20px;font-size:11px">1.2</span> Khám phá — Hỏi đúng, không tư vấn</div>
      <div class="hard-grid">
        <div><div class="hard-cell-label">Tại sao khó</div><div class="hard-cell-text">Bản năng bác sĩ là tư vấn giải pháp ngay — khó dừng ở mức "tìm hiểu" mà không chẩn đoán</div></div>
        <div><div class="hard-cell-label">Biểu hiện thường gặp</div><div class="hard-cell-text">Hỏi 1 câu rồi bắt đầu giải thích dài — khách không cảm thấy được nghe</div></div>
      </div>
      <div class="hard-fix"><div class="hard-fix-label">✅ Cách khắc phục</div><div class="hard-fix-text">Đặt mục tiêu: trong 3 phút đầu chỉ được hỏi, không được đưa giải pháp. Dùng đồng hồ bấm giờ khi luyện tập</div></div>
    </div>
  </div>
</div>

<div style="height:20px"></div>

<script>
function toggleGuide(){
  const b=document.getElementById('guide-body');
  const c=document.getElementById('guide-chevron');
  b.classList.toggle('open');
  c.classList.toggle('open');
}
function toggleSection(id){
  const list=document.getElementById(id+'-list');
  const chev=document.getElementById(id+'-chev');
  list.classList.toggle('open');
  chev.classList.toggle('open');
}
function toggleCriteria(id){
  const d=document.getElementById(id);
  const c=document.getElementById(id+'-chev');
  d.classList.toggle('open');
  c.classList.toggle('open');
}
function toggleRejection(){
  const l=document.getElementById('rej-list');
  const c=document.getElementById('rej-chev');
  l.classList.toggle('open');
  c.classList.toggle('open');
}
function toggleRej(id){
  const d=document.getElementById(id);
  const c=document.getElementById(id+'-chev');
  d.classList.toggle('open');
  c.classList.toggle('open');
}
function toggleHard(){
  const l=document.getElementById('hard-list');
  const c=document.getElementById('hard-chev');
  l.classList.toggle('open');
  c.classList.toggle('open');
}
function toggleCheck(el){
  const box=el.querySelector('.check-box');
  const lbl=el.querySelector('.check-label');
  box.classList.toggle('checked');
  lbl.classList.toggle('checked');
  updateProgress();
}
function updateProgress(){
  const secs=[1,2,3];
  let totalChecked=0,totalAll=0;
  secs.forEach(s=>{
    const items=document.querySelectorAll(`.checklist[data-section="${s}"] .check-box`);
    const checked=document.querySelectorAll(`.checklist[data-section="${s}"] .check-box.checked`);
    const pct=items.length?Math.round(checked.length/items.length*100):0;
    document.getElementById('p'+s+'-pct').textContent=pct+'%';
    document.getElementById('p'+s+'-bar').style.width=pct+'%';
    document.getElementById('s'+s+'-score').textContent=pct+'%';
    const el=document.getElementById('s'+s+'-score');
    el.className='score-num '+(pct>=80?'green':pct>=50?'amber':'red');
    totalChecked+=checked.length;
    totalAll+=items.length;
  });
  const total=totalAll?Math.round(totalChecked/totalAll*100):0;
  document.getElementById('prog-count').textContent=totalChecked+' / '+totalAll+' mục';
  const ts=document.getElementById('total-score');
  ts.textContent=total+'%';
  ts.className='score-num '+(total>=80?'green':total>=50?'amber':'red');
}
updateProgress();
</script>
</body>
</html>
