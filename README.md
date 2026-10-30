<!doctype html>
<html lang="vi"><head><meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self' 'unsafe-inline' https://cdn.jsdelivr.net https://cdnjs.cloudflare.com; style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; font-src https://fonts.gstatic.com; connect-src 'self' https://*.supabase.co https://cdnjs.cloudflare.com https://api.github.com https://raw.githubusercontent.com; worker-src blob:; img-src 'self' data: blob:; base-uri 'none'; object-src 'none'">
<script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2.45.4/dist/umd/supabase.min.js"></script>
<title>GDQP&AN – Trợ lý AI</title>
<!-- Đổi sang font Inter hiện đại -->
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<script src="https://cdnjs.cloudflare.com/ajax/libs/qrcodejs/1.0.0/qrcode.min.js"></script>
<style>
/* LỘT XÁC GIAO DIỆN MỚI */
:root {
  --bg: #f3f4f6;          /* Nền trang sáng dịu */
  --sf: #ffffff;          /* Nền card trắng */
  --tx: #111827;          /* Chữ đen đậm */
  --mu: #6b7280;          /* Chữ xám */
  --ln: #e5e7eb;          /* Viền xám nhạt */
  --pr: #10b981;          /* Xanh lá GDQP chủ đạo */
  --pr-hover: #059669;    /* Xanh lá đậm khi hover */
  --ok: #10b981;          
  --no: #ef4444;          /* Đỏ báo lỗi */
  --am: #f59e0b;          /* Cam cảnh báo */
  --sh: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
  box-sizing: border-box;
}

@media(prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#11
