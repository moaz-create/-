<!doctype html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>حاسبة العمر — تفصيلية وجميلة</title>
  <link href="https://fonts.googleapis.com/css2?family=Almarai:wght@300;400;700;800&display=swap" rel="stylesheet">
  <style>
    :root{
      --bg:#0f172a; /* غامق للخلفية */
      --card:#0b1220;
      --accent:#06b6d4;
      --muted:#94a3b8;
      --glass: rgba(255,255,255,0.04);
      --success: #10b981;
    }
    *{box-sizing:border-box}
    body{font-family: 'Almarai', Tahoma, Arial; margin:0;min-height:100vh;background:linear-gradient(180deg,var(--bg),#071022 120%);color:#e6eef8;display:flex;align-items:center;justify-content:center;padding:28px}
    .wrap{width:100%;max-width:920px}

    header{display:flex;align-items:center;gap:14px;margin-bottom:18px}
    .logo{width:64px;height:64px;border-radius:12px;background:linear-gradient(135deg,var(--accent),#7c3aed);display:flex;align-items:center;justify-content:center;font-weight:800;color:#021124;font-size:26px;box-shadow:0 8px 30px rgba(2,6,23,0.6)}
    h1{margin:0;font-size:20px}
    p.lead{margin:0;color:var(--muted);font-size:14px}

    .card{background:linear-gradient(180deg,var(--card), rgba(8,12,22,0.6));border-radius:14px;padding:20px;box-shadow:0 10px 40px rgba(2,6,23,0.6);border:1px solid rgba(255,255,255,0.03)}

    .grid{display:grid;grid-template-columns:1fr 360px;gap:18px}
    @media (max-width:880px){.grid{grid-template-columns:1fr}}

    .form-row{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-bottom:12px}
    @media (max-width:540px){.form-row{grid-template-columns:1fr}}

    label{display:block;font-size:13px;color:var(--muted);margin-bottom:6px}
    input, select{width:100%;padding:10px 12px;border-radius:10px;border:1px solid rgba(255,255,255,0.04);background:var(--glass);color:inherit;font-size:15px}
    input[type=date]::-webkit-inner-spin-button, input[type=date]::-webkit-calendar-picker-indicator{filter:invert(1)}

    .controls{display:flex;gap:8px;margin-top:6px}
    button{cursor:pointer;padding:10px 14px;border-radius:10px;border:0;font-weight:700}
    .btn-calc{background:linear-gradient(90deg,var(--accent),#7c3aed);color:#021124}
    .btn-clear{background:transparent;border:1px solid rgba(255,255,255,0.06);color:var(--muted)}

    .result-box{background:linear-gradient(180deg, rgba(255,255,255,0.02), rgba(255,255,255,0.01));padding:14px;border-radius:10px;border:1px solid rgba(255,255,255,0.03)}
    .result-box h2{margin:0 0 8px;font-size:16px}
    .big{font-size:22px;font-weight:800;color:#fff}
    .muted{color:var(--muted);font-size:13px}

    .details{margin-top:10px;display:flex;flex-direction:column;gap:6px}
    .chip{display:inline-block;padding:6px 8px;border-radius:999px;background:rgba(255,255,255,0.03);font-weight:700}

    .info{font-size:13px;color:var(--muted);margin-top:10px}
    footer{margin-top:12px;color:var(--muted);font-size:13px}

    /* small helper */
    .error{color:#ff6b6b;font-weight:700}
  </style>
</head>
<body>
  <div class="wrap">
    <header>
      <div class="logo">ع</div>
      <div>
        <h1>حاسبة العمر — تفصيلية</h1>
        <p class="lead">ادخل تاريخ ميلادك وحدد السنة أو التاريخ المرجعي — ستظهر النتيجة بالسنوات، الأشهر، الأيام، وحتى الساعات والدقائق إن رغبت.</p>
      </div>
    </header>

    <div class="card">
      <div class="grid">
        <!-- form -->
        <div>
          <div class="form-row">
            <div>
              <label for="birth">تاريخ الميلاد</label>
              <input id="birth" type="date" aria-label="تاريخ الميلاد" />
            </div>
            <div>
              <label for="birthTime">الوقت (اختياري)</label>
              <input id="birthTime" type="time" aria-label="وقت الميلاد" />
            </div>
          </div>

          <div class="form-row">
            <div>
              <label for="refDate">التاريخ المرجعي (اختياري)</label>
              <input id="refDate" type="date" aria-label="التاريخ المرجعي" />
            </div>
            <div>
              <label for="refTime">وقت المرجع (اختياري)</label>
              <input id="refTime" type="time" aria-label="وقت المرجع" />
            </div>
          </div>

          <div class="form-row">
            <div>
              <label for="useYearOnly">أو ادخل السنة فقط</label>
              <input id="useYearOnly" type="number" min="0" placeholder="مثال: 2025" />
            </div>
            <div>
              <label for="dayMode">طريقة حساب اليوم/الشهر</label>
              <select id="dayMode">
                <option value="same">استخدم نفس اليوم والشهر من التاريخ (مناسب لحساب حتى اليوم)</option>
                <option value="start">استخدم 1 يناير من السنة المدخلة (حساب مبسط للسنة)</option>
              </select>
            </div>
          </div>

          <div class="controls">
            <button id="calc" class="btn-calc">احسب العمر الآن</button>
            <button id="clear" class="btn-clear">إعادة ضبط الحقول</button>
            <button id="calcHours" class="btn-clear">اظهر بالساعات/دقائق</button>
          </div>

          <div id="message" class="info" role="status" aria-live="polite"></div>
        </div>

        <!-- output -->
        <aside>
          <div class="result-box">
            <h2>النتيجة</h2>
            <div id="mainResult" class="big">—</div>
            <div id="subResult" class="muted">لم يتم حساب أي شيء بعد.</div>

            <div class="details" id="extraDetails" style="display:none">
              <div><span class="chip" id="yearsChip">سنوات: —</span> <span class="chip" id="monthsChip">شهور: —</span></div>
              <div class="muted" id="totalDays">إجمالي الأيام: —</div>
              <div class="muted" id="birthInfo">تاريخ الميلاد: —</div>
              <div class="muted" id="refInfo">التاريخ المرجعي: —</div>
            </div>
          </div>

          <footer>إذا أردت ملفًا قابلًا للطباعة أو إضافة تصدير CSV قلّي.</footer>
        </aside>
      </div>
    </div>
  </div>

  <script>
    // العناصر
    const birthEl = document.getElementById('birth');
    const birthTimeEl = document.getElementById('birthTime');
    const refDateEl = document.getElementById('refDate');
    const refTimeEl = document.getElementById('refTime');
    const yearOnlyEl = document.getElementById('useYearOnly');
    const dayModeEl = document.getElementById('dayMode');

    const calcBtn = document.getElementById('calc');
    const clearBtn = document.getElementById('clear');
    const showHoursBtn = document.getElementById('calcHours');

    const message = document.getElementById('message');
    const mainResult = document.getElementById('mainResult');
    const subResult = document.getElementById('subResult');
    const extraDetails = document.getElementById('extraDetails');
    const yearsChip = document.getElementById('yearsChip');
    const monthsChip = document.getElementById('monthsChip');
    const totalDaysEl = document.getElementById('totalDays');
    const birthInfo = document.getElementById('birthInfo');
    const refInfo = document.getElementById('refInfo');

    // Helpers
    function parseDateInput(dateStr, timeStr){
      if(!dateStr) return null;
      // dateStr format YYYY-MM-DD, timeStr HH:MM
      const parts = dateStr.split('-').map(Number);
      let year = parts[0], month = parts[1]-1, day = parts[2];
      if(timeStr){
        const t = timeStr.split(':').map(Number);
        return new Date(year, month, day, t[0], t[1], 0, 0);
      }
      return new Date(year, month, day, 12, 0, 0); // منتصف اليوم لتلافي فروق التوقيت
    }

    function calcDetailed(birth, ref){
      // تأكد من أن ref >= birth
      if(ref < birth) return null;
      let by = birth.getFullYear(), bm = birth.getMonth(), bd = birth.getDate();
      let ry = ref.getFullYear(), rm = ref.getMonth(), rd = ref.getDate();

      let years = ry - by;
      let months = rm - bm;
      let days = rd - bd;

      if(days < 0){
        // الحصول على عدد أيام الشهر السابق
        const prevMonthLastDay = new Date(ref.getFullYear(), ref.getMonth(), 0).getDate();
        days += prevMonthLastDay;
        months -= 1;
      }
      if(months < 0){
        months += 12;
        years -= 1;
      }

      return {years, months, days};
    }

    function totalDays(birth, ref){
      const msPerDay = 1000*60*60*24;
      return Math.floor((ref - birth)/msPerDay);
    }

    function totalHours(birth, ref){
      const msPerHour = 1000*60*60;
      return Math.floor((ref - birth)/msPerHour);
    }

    function fmtArabicParts(d){
      const parts = [];
      if(d.years) parts.push(d.years + ' سنة');
      if(d.months) parts.push(d.months + ' شهر');
      if(d.days || parts.length===0) parts.push(d.days + ' يوم');
      return parts.join('، ');
    }

    function showError(text){
      message.innerHTML = '<span class="error">' + text + '</span>';
    }

    function clearMessage(){ message.textContent = ''; }

    function updateUI(result, birth, ref){
      if(!result){
        mainResult.textContent = 'خطأ في الحساب';
        subResult.textContent = '';
        extraDetails.style.display = 'none';
        return;
      }
      mainResult.textContent = fmtArabicParts(result);
      subResult.textContent = `تفصيلي: ${result.years} سنة و ${result.months} شهر و ${result.days} يوم.`;
      yearsChip.textContent = 'سنوات: ' + result.years;
      monthsChip.textContent = 'شهور: ' + (result.years*12 + result.months);
      totalDaysEl.textContent = 'إجمالي الأيام: ' + totalDays(birth, ref);
      birthInfo.textContent = 'تاريخ الميلاد: ' + birth.toLocaleString('ar-EG');
      refInfo.textContent = 'التاريخ المرجعي: ' + ref.toLocaleString('ar-EG');
      extraDetails.style.display = 'block';
    }

    // العملية الأساسية: تحديد التاريخ المرجعي حسب الإدخالات
    function buildReferenceDate(){
      // إذا تم إدخال تاريخ مرجعي صريح
      const refDateStr = refDateEl.value;
      const refTimeStr = refTimeEl.value;
      if(refDateStr){
        const d = parseDateInput(refDateStr, refTimeStr);
        return d;
      }

      // إن لم يدخلوا تاريخ مرجعي: راجع حقل السنة فقط
      const yearOnly = parseInt(yearOnlyEl.value);
      const today = new Date();
      if(!isNaN(yearOnly)){
        if(dayModeEl.value === 'same'){
          // استخدم نفس اليوم والشهر من اليوم الحالي
          const m = today.getMonth();
          const day = today.getDate();
          return new Date(yearOnly, m, day, 12, 0, 0);
        } else {
          return new Date(yearOnly, 0, 1, 12, 0, 0);
        }
      }

      // افتراضي: استخدم الآن
      return new Date();
    }

    // حدث حساب
    calcBtn.addEventListener('click', ()=>{
      clearMessage();
      const birthDateStr = birthEl.value;
      if(!birthDateStr){ showError('رجاءً اختر تاريخ الميلاد'); return; }
      const birthTimeStr = birthTimeEl.value;

      const birth = parseDateInput(birthDateStr, birthTimeStr);
      const ref = buildReferenceDate();

      if(ref < birth){ showError('التاريخ المرجعي قبل تاريخ الميلاد — تحقق من القيم'); return; }

      const detailed = calcDetailed(birth, ref);
      if(!detailed){ showError('حدث خطأ أثناء الحساب'); return; }

      updateUI(detailed, birth, ref);
      message.textContent = 'تم الحساب بنجاح.';
    });

    // عرض بالساعات/دقائق
    showHoursBtn.addEventListener('click', ()=>{
      clearMessage();
      const birthDateStr = birthEl.value;
      if(!birthDateStr){ showError('رجاءً اختر تاريخ الميلاد'); return; }
      const birth = parseDateInput(birthDateStr, birthTimeEl.value);
      const ref = buildReferenceDate();
      if(ref < birth){ showError('التاريخ المرجعي قبل تاريخ الميلاد — تحقق من القيم'); return; }

      const ms = ref - birth;
      const mins = Math.floor(ms / (1000*60));
      const hrs = Math.floor(ms / (1000*60*60));
      const days = Math.floor(ms / (1000*60*60*24));

      mainResult.textContent = `${hrs.toLocaleString('ar-EG')} ساعة`;
      subResult.textContent = `${mins.toLocaleString('ar-EG')} دقيقة — ${days.toLocaleString('ar-EG')} يوم`;
      extraDetails.style.display = 'none';
      message.textContent = 'عرض بالوحدات الزمنية الكبيرة.';
    });

    clearBtn.addEventListener('click', ()=>{
      birthEl.value = '';
      birthTimeEl.value = '';
      refDateEl.value = '';
      refTimeEl.value = '';
      yearOnlyEl.value = '';
      mainResult.textContent = '—';
      subResult.textContent = 'لم يتم حساب أي شيء بعد.';
      extraDetails.style.display = 'none';
      clearMessage();
    });

    // نضع قيمة افتراضية للسنة الحالية
    (function setDefaults(){
      const now = new Date();
      yearOnlyEl.value = now.getFullYear();
    })();

  </script>
</body>
</html>
