import os
import subprocess
import time
from flask import Flask, render_template_string, request, redirect, jsonify

app = Flask(__name__)
UPLOAD_FOLDER = 'my_bots'
os.makedirs(UPLOAD_FOLDER, exist_ok=True)

# لتخزين العمليات الحية للبوتات {bot_name: process_object}
running_processes = {}
start_time = time.time()

HTML_TEMPLATE = '''
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>⚡ CyberHost Pro - السيرفر المتكامل</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --bg-main: #060913;
            --bg-card: #0d1222;
            --border-color: #1e2942;
            --text-main: #ffffff;
            --text-sub: #7f8fa4;
            --primary: #00d2ff;
            --purple: #7000ff;
            --success: #00ff66;
            --danger: #ff3366;
            --gold: #ffcc00;
        }
        .light-mode {
            --bg-main: #f0f2f5;
            --bg-card: #ffffff;
            --border-color: #dcdde1;
            --text-main: #1e272e;
            --text-sub: #718093;
            --primary: #00a8ff;
            --purple: #9c88ff;
        }
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, sans-serif; transition: background 0.3s, border-color 0.3s; }
        body { background: var(--bg-main); color: var(--text-main); padding: 15px; }
        .container { max-width: 900px; margin: 0 auto; }
        
        /* الهيدر وشريط الحالة */
        header { display: flex; justify-content: space-between; align-items: center; padding-bottom: 15px; border-bottom: 2px solid var(--purple); margin-bottom: 20px; }
        header h1 { font-size: 1.4rem; color: var(--primary); text-shadow: 0 0 10px rgba(0,210,255,0.2); }
        
        /* شبكة اللوحات (Grid Control) */
        .grid-panels { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 12px; margin-bottom: 15px; }
        
        .card { background: var(--bg-card); border: 1px solid var(--border-color); border-radius: 12px; padding: 15px; box-shadow: 0 4px 15px rgba(0,0,0,0.15); margin-bottom: 15px; }
        .card-title { font-size: 0.9rem; font-weight: bold; margin-bottom: 12px; display: flex; align-items: center; gap: 8px; color: var(--gold); }
        
        /* صناديق الإحصائيات */
        .stat-box { display: flex; align-items: center; gap: 12px; padding: 10px; background: rgba(255,255,255,0.02); border-radius: 8px; border: 1px solid var(--border-color); }
        .stat-box i { font-size: 1.5rem; color: var(--primary); }
        .stat-box .num { font-size: 1.1rem; font-weight: bold; }
        .stat-box .lbl { font-size: 0.65rem; color: var(--text-sub); }

        /* أزرار وعناصر التحكم */
        .btn { border: none; color: white; padding: 6px 12px; border-radius: 6px; cursor: pointer; font-weight: bold; font-size: 0.75rem; display: inline-flex; align-items: center; gap: 4px; }
        .btn-primary { background: linear-gradient(135deg, var(--primary), var(--purple)); }
        .btn-danger { background: var(--danger); }
        .btn-success { background: var(--success); color: #000; }
        .btn-secondary { background: rgba(255,255,255,0.1); color: var(--text-main); border: 1px solid var(--border-color); }
        
        /* منطقة الرفع السريع */
        .upload-zone { border: 2px dashed var(--border-color); padding: 20px; text-align: center; border-radius: 10px; cursor: pointer; }
        .upload-zone:hover { border-color: var(--primary); background: rgba(0,210,255,0.02); }
        
        /* جدول وإدارة البوتات */
        .bot-list { display: flex; flex-direction: column; gap: 8px; }
        .bot-row { display: flex; justify-content: space-between; align-items: center; padding: 10px 14px; background: rgba(255,255,255,0.01); border: 1px solid var(--border-color); border-radius: 8px; flex-wrap: wrap; gap: 8px; }
        .bot-info { display: flex; align-items: center; gap: 10px; }
        .bot-name { font-size: 0.85rem; font-weight: bold; }
        
        .badge { font-size: 0.65rem; padding: 2px 8px; border-radius: 20px; font-weight: bold; }
        .badge-on { background: rgba(0,255,102,0.15); color: var(--success); border: 1px solid rgba(0,255,102,0.2); }
        .badge-off { background: rgba(255,51,51,0.15); color: var(--danger); border: 1px solid rgba(255,51,51,0.2); }
        
        /* التيرمنال والمحرر المدمج */
        .terminal { background: #000; color: var(--success); font-family: monospace; padding: 10px; border-radius: 8px; font-size: 0.7rem; max-height: 120px; overflow-y: auto; box-shadow: inset 0 0 10px #000; }
        textarea { width: 100%; min-height: 180px; background: #000; color: #fff; font-family: monospace; padding: 10px; border-radius: 8px; font-size: 0.75rem; border: 1px solid var(--border-color); outline: none; }
        
        .modal { display: none; position: fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.8); z-index:100; align-items:center; justify-content:center; padding:15px; }
        .modal.show { display: flex; }
        .modal-body { background: var(--bg-card); border: 1px solid var(--primary); padding: 20px; border-radius: 12px; width: 100%; max-width: 600px; }
    </style>
</head>
<body>
    <div class="container">
        
        <!-- الهيدر الرئيسي -->
        <header>
            <h1><i class="fa-solid fa-circle-nodes"></i> CyberHost Multi-Panel</h1>
            <div>
                <button class="btn btn-secondary" onclick="toggleTheme()"><i class="fa-solid fa-moon"></i> الوضع</button>
            </div>
        </header>

        <!-- اللوحة الأولي: لوحة الإحصائيات والمراقبة (Monitor Panel) -->
        <div class="grid-panels">
            <div class="stat-box">
                <i class="fa-solid fa-robot"></i>
                <div><div class="num">{{ bots|length }}</div><div class="lbl">إجمالي السكربتات</div></div>
            </div>
            <div class="stat-box">
                <i class="fa-solid fa-circle-check" style="color:var(--success);"></i>
                <div><div class="num" style="color:var(--success);">{{ running_count }}</div><div class="lbl">بوتات متصلة الآن</div></div>
            </div>
            <div class="stat-box">
                <i class="fa-solid fa-hourglass-start" style="color:var(--gold);"></i>
                <div><div class="num" id="uptime">0s</div><div class="lbl">مدة نشاط السيرفر</div></div>
            </div>
        </div>

        <!-- اللوحة الثانية: لوحة الرفع السريع الذكية (Upload Panel) -->
        <div class="card">
            <div class="card-title"><i class="fa-solid fa-upload"></i> لوحة رفع ملفات البايثون (`.py`)</div>
            <form action="/upload" method="post" enctype="multipart/form-data">
                <label class="upload-zone" for="fileInput">
                    <i class="fa-solid fa-folder-open" style="font-size: 2rem; color: var(--primary); margin-bottom: 5px;"></i>
                    <p style="font-size:0.8rem; color:var(--text-sub);">اسحبي أو اختاري ملف البوت الحقيقي لتشغيله فوراً</p>
                </label>
                <input type="file" id="fileInput" name="file" accept=".py" onchange="this.form.submit()">
            </form>
        </div>

        <!-- اللوحة الثالثة: لوحة الإدارة والتشغيل والتحرير (Control Panel) -->
        <div class="card">
            <div class="card-title" style="color: var(--success);"><i class="fa-solid fa-sliders"></i> لوحة تحكم وإدارة العمليات الحية</div>
            <div class="bot-list">
                {% if not bots %}
                <p style="text-align:center; font-size:0.75rem; color:var(--text-sub);">لا توجد بوتات مرفوعة بالسيرفر السحابي حالياً.</p>
                {% endif %}
                {% for bot in bots %}
                <div class="bot-row">
                    <div class="bot-info">
                        <i class="fa-brands fa-python" style="color: var(--gold); font-size:1.2rem;"></i>
                        <span class="bot-name">{{ bot.name }}</span>
                    </div>
                    <div>
                        <span class="badge {% if bot.running %}badge-on{% else %}badge-off{% endif %}">
                            {% if bot.running %}● متصل ومتفاعل{% else %}○ متوقف حالياً{% endif %}
                        </span>
                    </div>
                    <div style="display:flex; gap:6px; align-items:center;">
                        {% if not bot.running %}
                        <a href="/start/{{ bot.name }}" class="btn btn-success"><i class="fa-solid fa-play"></i></a>
                        {% else %}
                        <a href="/stop/{{ bot.name }}" class="btn btn-danger"><i class="fa-solid fa-stop"></i></a>
                        {% endif %}
                        <button class="btn btn-secondary" onclick="openEditor('{{ bot.name }}')"><i class="fa-solid fa-pen-to-square" style="color:var(--primary);"></i></button>
                        <a href="/delete/{{ bot.name }}" class="btn btn-secondary" style="color:var(--danger);"><i class="fa-solid fa-trash"></i></a>
                    </div>
                </div>
                {% endfor %}
            </div>
        </div>

        <!-- اللوحة الرابعة: شاشة تتبع البث والأخطاء (Live Terminal Panel) -->
        <div class="card">
            <div class="card-title" style="color:var(--primary);"><i class="fa-solid fa-terminal"></i> سجل حركة ومراقبة النظام (System Logs)</div>
            <div class="terminal" id="terminalLog">
                [SYSTEM] السيرفر السحابي يعمل بكفاءة قصوى وجاهز لاستقبال الاتصالات وتفعيل الأوامر الحية...
            </div>
        </div>

    </div>

    <!-- لوحة التحرير السحرية (Editor Modal) -->
    <div class="modal" id="editorModal">
        <div class="modal-body">
            <div style="display:flex; justify-content:space-between; margin-bottom:10px;">
                <h3 id="editTitle" style="font-size:0.9rem;">📝 تعديل كود البوت</h3>
                <button onclick="closeEditor()" style="background:none; border:none; color:var(--danger); font-size:1.2rem; cursor:pointer;">✕</button>
            </div>
            <form action="/save_code" method="post">
                <input type="hidden" id="editFilename" name="filename">
                <textarea id="editArea" name="code" spellcheck="false"></textarea>
                <div style="margin-top:10px; text-align:left;">
                    <button type="submit" class="btn btn-primary">💾 حفظ التعديلات وتحديث السكربت</button>
                </div>
            </form>
        </div>
    </div>

    <script>
        function toggleTheme() { document.body.classList.toggle('light-mode'); }
        
        // حساب الـ Uptime حياً
        let startTime = {{ start_time }};
        setInterval(() => {
            let seconds = Math.floor(Date.now() / 1000 - startTime);
            document.getElementById('uptime').innerText = seconds + 's';
        }, 1000);

        // فتح محرر الأكواد وجلب محتوى الملف فوراً
        async function openEditor(filename) {
            document.getElementById('editTitle').innerText = "📝 تعديل كود السكربت: " + filename;
            document.getElementById('editFilename').value = filename;
            
            let res = await fetch('/get_code/' + filename);
            let data = await res.json();
            
            document.getElementById('editArea').value = data.code;
            document.getElementById('editorModal').classList.add('show');
        }
        function closeEditor() { document.getElementById('editorModal').classList.remove('show'); }
    </script>
</body>
</html>
'''

@app.route('/')
def index():
    files = os.listdir(UPLOAD_FOLDER)
    bots_status = []
    running_count = 0
    for f in files:
        if f.endswith('.py'):
            is_running = f in running_processes and running_processes[f].poll() is None
            if is_running: running_count += 1
            bots_status.append({'name': f, 'running': is_running})
            
    return render_template_string(
        HTML_TEMPLATE, 
        bots=bots_status, 
        running_count=running_count, 
        start_time=start_time
    )

@app.route('/upload', methods=['POST'])
def upload_file():
    if 'file' not in request.files: return redirect('/')
    file = request.files['file']
    if file.filename == '' or not file.filename.endswith('.py'): return redirect('/')
    file.save(os.path.join(UPLOAD_FOLDER, file.filename))
    return redirect('/')

@app.route('/start/<filename>')
def start_bot(filename):
    file_path = os.path.join(UPLOAD_FOLDER, filename)
    if filename not in running_processes or running_processes[filename].poll() is not None:
        if os.path.exists(file_path):
            # تشغيل السكربت كعملية فرعية مستقلة بالكامل داخل معالج Replit
            process = subprocess.Popen(['python3', file_path])
            running_processes[filename] = process
    return redirect('/')

@app.route('/stop/<filename>')
def stop_bot(filename):
    if filename in running_processes:
        process = running_processes[filename]
        process.terminate()
        process.wait()
        del running_processes[filename]
    return redirect('/')

@app.route('/delete/<filename>')
def delete_bot(filename):
    stop_bot(filename)
    file_path = os.path.join(UPLOAD_FOLDER, filename)
    if os.path.exists(file_path): os.remove(file_path)
    return redirect('/')

@app.route('/get_code/<filename>')
def get_code(filename):
    file_path = os.path.join(UPLOAD_FOLDER, filename)
    if os.path.exists(file_path):
        with open(file_path, 'r', encoding='utf-8') as f:
            return jsonify({'code': f.read()})
    return jsonify({'code': ''})

@app.route('/save_code', methods=['POST'])
def save_code():
    filename = request.form.get('filename')
    code = request.form.get('code')
    file_path = os.path.join(UPLOAD_FOLDER, filename)
    if os.path.exists(file_path):
        with open(file_path, 'w', encoding='utf-8') as f:
            f.write(code)
    return redirect('/')

if __name__ == '__main__':
    # المنفذ الرسمي والمعتمد لبيئة تشغيل Replit السحابية
    app.run(host='0.0.0.0', port=8080)
