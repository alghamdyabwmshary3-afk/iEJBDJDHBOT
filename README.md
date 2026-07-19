import os
import sys
import subprocess
import signal
import time
import threading
import json
import shutil
from datetime import datetime
from flask import Flask, render_template_string, request, redirect, jsonify, send_from_directory, session
from werkzeug.utils import secure_filename
from functools import wraps

# ==================== الإعدادات ====================
app = Flask(__name__)
app.secret_key = 'your-secret-key-here-change-it'

# مجلدات التخزين
BOTS_FOLDER = 'bots_data'
LOGS_FOLDER = 'bots_logs'
BACKUP_FOLDER = 'bots_backups'
os.makedirs(BOTS_FOLDER, exist_ok=True)
os.makedirs(LOGS_FOLDER, exist_ok=True)
os.makedirs(BACKUP_FOLDER, exist_ok=True)

# ==================== بيانات المستخدمين (يمكن ربطها بقاعدة بيانات) ====================
USERS = {
    'admin': 'admin123',
    'user1': 'pass123'
}

# العمليات النشطة
active_bots = {}
auto_restart = {}

# ==================== وظيفة التحقق من الدخول ====================
def login_required(f):
    @wraps(f)
    def decorated(*args, **kwargs):
        if not session.get('logged_in'):
            return redirect('/login')
        return f(*args, **kwargs)
    return decorated

# ==================== واجهة الموقع ====================
HTML_TEMPLATE = '''
<!DOCTYPE html>
<html dir="rtl" lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🚀 منصة استضافة البوتات السحابية</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Tahoma', sans-serif; }
        body {
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }
        .container { max-width: 1200px; margin: 0 auto; }
        
        header {
            background: rgba(255,255,255,0.05);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: 20px;
            padding: 30px;
            text-align: center;
            margin-bottom: 30px;
        }
        header h1 {
            font-size: 2.5rem;
            background: linear-gradient(135deg, #00f0ff, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        header p { color: #94a3b8; margin-top: 10px; }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
            gap: 15px;
            margin-bottom: 30px;
        }
        .stat-card {
            background: rgba(255,255,255,0.05);
            border: 1px solid rgba(255,255,255,0.08);
            border-radius: 15px;
            padding: 20px;
            text-align: center;
        }
        .stat-card h3 { font-size: 2rem; color: #00f0ff; }
        .stat-card p { color: #94a3b8; font-size: 0.9rem; }
        
        .panel {
            background: rgba(255,255,255,0.05);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.08);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 25px;
        }
        .panel-title {
            font-size: 1.3rem;
            color: #00f0ff;
            margin-bottom: 20px;
            border-bottom: 2px solid rgba(0,240,255,0.2);
            padding-bottom: 10px;
        }
        
        .upload-zone {
            border: 2px dashed rgba(0,240,255,0.3);
            padding: 40px;
            text-align: center;
            border-radius: 15px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .upload-zone:hover {
            border-color: #00f0ff;
            background: rgba(0,240,255,0.05);
        }
        .upload-zone i { font-size: 3rem; color: #00f0ff; margin-bottom: 15px; }
        
        .bot-card {
            background: rgba(255,255,255,0.03);
            border: 1px solid rgba(255,255,255,0.06);
            border-radius: 12px;
            padding: 15px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 10px;
        }
        .bot-card:hover { background: rgba(255,255,255,0.06); }
        .bot-name { font-weight: bold; font-size: 1.1rem; }
        .status { padding: 4px 12px; border-radius: 20px; font-size: 0.8rem; }
        .status-active { background: rgba(16,185,129,0.2); color: #10b981; border: 1px solid rgba(16,185,129,0.3); }
        .status-inactive { background: rgba(239,68,68,0.2); color: #ef4444; border: 1px solid rgba(239,68,68,0.3); }
        
        .btn {
            border: none;
            padding: 7px 15px;
            border-radius: 8px;
            cursor: pointer;
            text-decoration: none;
            color: #fff;
            font-weight: 600;
            display: inline-flex;
            align-items: center;
            gap: 6px;
            font-size: 0.85rem;
            transition: all 0.3s ease;
        }
        .btn:hover { transform: scale(1.05); }
        .btn-start { background: linear-gradient(135deg, #059669, #10b981); }
        .btn-stop { background: linear-gradient(135deg, #dc2626, #ef4444); }
        .btn-download { background: #475569; }
        .btn-delete { background: rgba(239,68,68,0.2); color: #ef4444; border: 1px solid rgba(239,68,68,0.2); }
        .btn-delete:hover { background: #ef4444; color: #fff; }
        .btn-edit { background: #7c3aed; }
        
        .terminal {
            background: #0a0a0f;
            border: 1px solid rgba(255,255,255,0.05);
            border-radius: 10px;
            padding: 15px;
            font-family: 'Courier New', monospace;
            color: #34d399;
            height: 300px;
            overflow-y: auto;
            font-size: 0.8rem;
            white-space: pre-wrap;
        }
        
        select {
            background: #1e293b;
            color: #fff;
            border: 1px solid rgba(255,255,255,0.1);
            padding: 8px 15px;
            border-radius: 8px;
            width: 100%;
            max-width: 300px;
            margin-bottom: 15px;
        }
        
        .logout-btn {
            background: rgba(239,68,68,0.2);
            color: #ef4444;
            border: 1px solid rgba(239,68,68,0.2);
            padding: 8px 20px;
            border-radius: 10px;
            text-decoration: none;
            float: left;
        }
        .logout-btn:hover { background: #ef4444; color: #fff; }
        
        @media (max-width: 768px) {
            .bot-card { flex-direction: column; align-items: stretch; }
            .actions { display: flex; flex-wrap: wrap; gap: 5px; }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1><i class="fa-solid fa-cloud-upload-alt"></i> منصة استضافة البوتات السحابية</h1>
            <p>استضافة وتشغيل البوتات الخاصة بك بسهولة وأمان</p>
            <a href="/logout" class="logout-btn"><i class="fa-solid fa-sign-out-alt"></i> خروج</a>
        </header>
        
        <div class="stats">
            <div class="stat-card"><h3 id="total-bots">0</h3><p>إجمالي البوتات</p></div>
            <div class="stat-card"><h3 id="active-bots" style="color: #10b981;">0</h3><p>يعمل الآن</p></div>
            <div class="stat-card"><h3 id="inactive-bots" style="color: #ef4444;">0</h3><p>متوقف</p></div>
            <div class="stat-card"><h3 style="color: #a855f7;"><i class="fa-solid fa-shield-halved"></i></h3><p>حماية نشطة</p></div>
        </div>
        
        <div class="panel">
            <div class="panel-title"><i class="fa-solid fa-upload"></i> رفع بوت جديد</div>
            <form action="/upload" method="post" enctype="multipart/form-data">
                <div class="upload-zone" onclick="document.getElementById('fileInput').click()">
                    <i class="fa-solid fa-file-code"></i>
                    <p>انقر لرفع ملف البوت</p>
                    <p style="font-size:0.8rem; color:#64748b;">يدعم: .py, .js, .jar, .sh</p>
                </div>
                <input type="file" id="fileInput" name="file" style="display:none;" onchange="this.form.submit()">
            </form>
        </div>
        
        <div class="panel">
            <div class="panel-title"><i class="fa-solid fa-list"></i> البوتات المرفوعة</div>
            {% if not bots %}
            <p style="color: #64748b; text-align: center; padding: 20px;">لا توجد بوتات مرفوعة بعد</p>
            {% endif %}
            {% for bot in bots %}
            <div class="bot-card">
                <div class="bot-name">
                    <i class="fa-solid {{ 'fa-robot' if bot.running else 'fa-robot' }}"></i>
                    {{ bot.name }}
                    <span class="status {{ 'status-active' if bot.running else 'status-inactive' }}">
                        <i class="fa-solid {{ 'fa-bolt' if bot.running else 'fa-power-off' }}"></i>
                        {{ 'يعمل' if bot.running else 'متوقف' }}
                    </span>
                </div>
                <div class="actions">
                    {% if not bot.running %}
                    <a href="/start/{{ bot.name }}" class="btn btn-start"><i class="fa-solid fa-play"></i> تشغيل</a>
                    {% else %}
                    <a href="/stop/{{ bot.name }}" class="btn btn-stop"><i class="fa-solid fa-stop"></i> إيقاف</a>
                    {% endif %}
                    <a href="/download/{{ bot.name }}" class="btn btn-download"><i class="fa-solid fa-download"></i></a>
                    <a href="/edit/{{ bot.name }}" class="btn btn-edit"><i class="fa-solid fa-edit"></i></a>
                    <a href="/delete/{{ bot.name }}" class="btn btn-delete" onclick="return confirm('حذف البوت نهائياً؟')"><i class="fa-solid fa-trash"></i></a>
                </div>
            </div>
            {% endfor %}
        </div>
        
        <div class="panel">
            <div class="panel-title"><i class="fa-solid fa-terminal"></i> مراقبة السجلات</div>
            <select id="logSelect" onchange="loadLogs()">
                <option value="">-- اختر البوت --</option>
                {% for bot in bots %}
                <option value="{{ bot.name }}">{{ bot.name }}</option>
                {% endfor %}
            </select>
            <div class="terminal" id="terminal">[نظام] انتظر اختيار بوت لعرض سجلاته</div>
        </div>
    </div>
    
    <script>
        function updateStats() {
            const cards = document.querySelectorAll('.bot-card');
            const active = document.querySelectorAll('.status-active');
            document.getElementById('total-bots').textContent = cards.length;
            document.getElementById('active-bots').textContent = active.length;
            document.getElementById('inactive-bots').textContent = cards.length - active.length;
        }
        updateStats();
        
        function loadLogs() {
            const bot = document.getElementById('logSelect').value;
            if (!bot) return;
            fetch('/logs/' + bot)
                .then(res => res.json())
                .then(data => {
                    document.getElementById('terminal').textContent = data.logs || '[لا توجد سجلات]';
                });
        }
        
        setInterval(() => {
            if (document.getElementById('logSelect').value) loadLogs();
        }, 3000);
    </script>
</body>
</html>
'''

# ==================== دوال التشغيل ====================

def auto_restart_daemon():
    """داemon لإعادة تشغيل البوتات المتوقفة"""
    while True:
        time.sleep(5)
        for bot_name, should_restart in list(auto_restart.items()):
            if should_restart:
                bot_path = os.path.join(BOTS_FOLDER, bot_name)
                if bot_name not in active_bots or active_bots[bot_name].poll() is not None:
                    if os.path.exists(bot_path):
                        log_path = os.path.join(LOGS_FOLDER, f"{bot_name}.log")
                        with open(log_path, "a", encoding="utf-8") as log:
                            log.write(f"\n[{datetime.now()}] 🔄 إعادة تشغيل تلقائي\n")
                        
                        # تحديد نوع التشغيل
                        ext = os.path.splitext(bot_name)[1].lower()
                        cmd = []
                        if ext == '.py':
                            cmd = [sys.executable, bot_path]
                        elif ext == '.js':
                            cmd = ['node', bot_path]
                        elif ext == '.jar':
                            cmd = ['java', '-jar', bot_path]
                        elif ext == '.sh':
                            cmd = ['bash', bot_path]
                        else:
                            continue
                        
                        process = subprocess.Popen(
                            cmd,
                            stdout=open(log_path, "a", encoding="utf-8"),
                            stderr=subprocess.STDOUT,
                            text=True,
                            preexec_fn=None if os.name == 'nt' else os.setsid
                        )
                        active_bots[bot_name] = process

# تشغيل الداemon
threading.Thread(target=auto_restart_daemon, daemon=True).start()

# ==================== صفحات الموقع ====================

@app.route('/login', methods=['GET', 'POST'])
def login():
    if request.method == 'POST':
        username = request.form.get('username')
        password = request.form.get('password')
        if username in USERS and USERS[username] == password:
            session['logged_in'] = True
            session['username'] = username
            return redirect('/')
        return '❌ اسم المستخدم أو كلمة المرور خاطئة', 403
    return '''
    <!DOCTYPE html>
    <html dir="rtl">
    <head>
        <meta charset="UTF-8">
        <title>تسجيل الدخول</title>
        <style>
            body { background: linear-gradient(135deg, #0f0c29, #302b63, #24243e); color: #fff; font-family: Tahoma; display: flex; justify-content: center; align-items: center; height: 100vh; margin: 0; }
            .login-box { background: rgba(255,255,255,0.05); border: 1px solid rgba(255,255,255,0.1); border-radius: 20px; padding: 40px; width: 350px; backdrop-filter: blur(15px); }
            h2 { text-align: center; color: #00f0ff; margin-bottom: 30px; }
            input { width: 100%; padding: 12px; margin: 10px 0; border: 1px solid rgba(255,255,255,0.1); background: #1e293b; color: #fff; border-radius: 10px; }
            button { width: 100%; padding: 12px; background: linear-gradient(135deg, #00f0ff, #a855f7); border: none; border-radius: 10px; color: #fff; font-weight: bold; font-size: 1.1rem; cursor: pointer; }
            button:hover { transform: scale(1.02); }
        </style>
    </head>
    <body>
        <div class="login-box">
            <h2>🔐 تسجيل الدخول</h2>
            <form method="post">
                <input type="text" name="username" placeholder="اسم المستخدم" required>
                <input type="password" name="password" placeholder="كلمة المرور" required>
                <button type="submit">دخول</button>
            </form>
        </div>
    </body>
    </html>
    '''

@app.route('/')
@login_required
def index():
    files = os.listdir(BOTS_FOLDER)
    bots = []
    for f in files:
        if f.endswith(('.py', '.js', '.jar', '.sh')):
            is_running = f in active_bots and active_bots[f].poll() is None
            bots.append({'name': f, 'running': is_running})
    return render_template_string(HTML_TEMPLATE, bots=bots)

@app.route('/upload', methods=['POST'])
@login_required
def upload_file():
    if 'file' not in request.files:
        return redirect('/')
    file = request.files['file']
    if file.filename == '':
        return redirect('/')
    
    ext = os.path.splitext(file.filename)[1].lower()
    if ext not in ('.py', '.js', '.jar', '.sh'):
        return '⚠️ امتداد غير مدعوم', 400
    
    filename = secure_filename(file.filename)
    file.save(os.path.join(BOTS_FOLDER, filename))
    return redirect('/')

@app.route('/start/<filename>')
@login_required
def start_bot(filename):
    bot_path = os.path.join(BOTS_FOLDER, filename)
    if not os.path.exists(bot_path):
        return '❌ البوت غير موجود', 404
    
    log_path = os.path.join(LOGS_FOLDER, f"{filename}.log")
    
    # إيقاف القديم إذا كان يعمل
    if filename in active_bots:
        try:
            active_bots[filename].kill()
        except:
            pass
        del active_bots[filename]
    
    # تشغيل البوت الجديد
    ext = os.path.splitext(filename)[1].lower()
    cmd = []
    if ext == '.py':
        cmd = [sys.executable, bot_path]
    elif ext == '.js':
        cmd = ['node', bot_path]
    elif ext == '.jar':
        cmd = ['java', '-jar', bot_path]
    elif ext == '.sh':
        cmd = ['bash', bot_path]
    else:
        return '⚠️ امتداد غير مدعوم', 400
    
    with open(log_path, "a", encoding="utf-8") as log:
        log.write(f"\n[{datetime.now()}] ✅ تم تشغيل البوت\n")
    
    process = subprocess.Popen(
        cmd,
        stdout=open(log_path, "a", encoding="utf-8"),
        stderr=subprocess.STDOUT,
        text=True,
        preexec_fn=None if os.name == 'nt' else os.setsid
    )
    active_bots[filename] = process
    auto_restart[filename] = True
    
    return redirect('/')

@app.route('/stop/<filename>')
@login_required
def stop_bot(filename):
    auto_restart[filename] = False
    
    if filename in active_bots:
        try:
            if os.name == 'nt':
                active_bots[filename].terminate()
            else:
                os.killpg(os.getpgid(active_bots[filename].pid), signal.SIGTERM)
            time.sleep(1)
            if active_bots[filename].poll() is None:
                active_bots[filename].kill()
        except:
            pass
        del active_bots[filename]
        
        log_path = os.path.join(LOGS_FOLDER, f"{filename}.log")
        with open(log_path, "a", encoding="utf-8") as log:
            log.write(f"\n[{datetime.now()}] ⏹ تم إيقاف البوت\n")
    
    return redirect('/')

@app.route('/download/<filename>')
@login_required
def download_bot(filename):
    return send_from_directory(BOTS_FOLDER, filename, as_attachment=True)

@app.route('/edit/<filename>')
@login_required
def edit_bot(filename):
    bot_path = os.path.join(BOTS_FOLDER, filename)
    if not os.path.exists(bot_path):
        return '❌ البوت غير موجود', 404
    
    with open(bot_path, 'r', encoding='utf-8', errors='ignore') as f:
        content = f.read()
    
    return f'''
    <!DOCTYPE html>
    <html dir="rtl">
    <head>
        <meta charset="UTF-8">
        <title>تعديل {filename}</title>
        <style>
            body {{ background: #0f0c29; color: #fff; padding: 20px; font-family: Tahoma; }}
            .container {{ max-width: 900px; margin: 0 auto; }}
            textarea {{ width: 100%; height: 500px; background: #1e293b; color: #e2e8f0; border: 1px solid #334155; border-radius: 10px; padding: 15px; font-family: 'Courier New', monospace; }}
            .btn {{ background: #00f0ff; color: #000; border: none; padding: 10px 30px; border-radius: 8px; font-weight: bold; cursor: pointer; margin-top: 10px; }}
            .btn:hover {{ background: #a855f7; color: #fff; }}
            a {{ color: #94a3b8; text-decoration: none; margin-top: 10px; display: inline-block; }}
        </style>
    </head>
    <body>
        <div class="container">
            <h2 style="color: #00f0ff;">✏️ تعديل: {filename}</h2>
            <form method="post" action="/save/{filename}">
                <textarea name="content">{content}</textarea><br>
                <button type="submit" class="btn">💾 حفظ</button>
                <a href="/">🔙 رجوع</a>
            </form>
        </div>
    </body>
    </html>
    '''

@app.route('/save/<filename>', methods=['POST'])
@login_required
def save_bot(filename):
    bot_path = os.path.join(BOTS_FOLDER, filename)
    if not os.path.exists(bot_path):
        return '❌ البوت غير موجود', 404
    
    # عمل نسخة احتياطية
    backup_path = os.path.join(BACKUP_FOLDER, f"{filename}_{int(time.time())}.bak")
    shutil.copy2(bot_path, backup_path)
    
    with open(bot_path, 'w', encoding='utf-8') as f:
        f.write(request.form.get('content', ''))
    
    return redirect('/')

@app.route('/delete/<filename>')
@login_required
def delete_bot(filename):
    auto_restart[filename] = False
    if filename in active_bots:
        try:
            active_bots[filename].kill()
        except:
            pass
        del active_bots[filename]
    
    bot_path = os.path.join(BOTS_FOLDER, filename)
    log_path = os.path.join(LOGS_FOLDER, f"{filename}.log")
    if os.path.exists(bot_path):
        os.remove(bot_path)
    if os.path.exists(log_path):
        os.remove(log_path)
    
    return redirect('/')

@app.route('/logs/<filename>')
@login_required
def get_logs(filename):
    log_path = os.path.join(LOGS_FOLDER, f"{filename}.log")
    if os.path.exists(log_path):
        with open(log_path, 'r', encoding='utf-8', errors='ignore') as f:
            return jsonify({'logs': f.read()[-5000:]})
    return jsonify({'logs': '🚀 لا توجد سجلات'})

@app.route('/logout')
def logout():
    session.clear()
    return redirect('/login')

# ==================== تشغيل السيرفر ====================
if __name__ == '__main__':
    print("""
    ╔══════════════════════════════════════════════════════╗
    ║   🚀 منصة استضافة البوتات تعمل الآن!               ║
    ║   📡 الرابط: http://0.0.0.0:5000                   ║
    ║   👤 المستخدم: admin                               ║
    ║   🔑 كلمة المرور: admin123                         ║
    ╚══════════════════════════════════════════════════════╝
    """)
    app.run(host='0.0.0.0', port=5000, debug=False)
