<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>个人笔记应用</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;
        }

        body {
            height: 100vh;
            display: flex;
            background-color: #f5f7fa;
            color: #333;
            overflow: hidden;
        }

        .container {
            display: flex;
            width: 100%;
            height: 100vh;
        }

        /* 左侧笔记列表区域 - 宽度减少一半 */
        .notes-sidebar {
            width: 25%;
            min-width: 200px;
            max-width: 300px;
            background-color: #fff;
            border-right: 1px solid #e1e4e8;
            display: flex;
            flex-direction: column;
            box-shadow: 2px 0 10px rgba(0, 0, 0, 0.05);
            z-index: 2;
        }

        .sidebar-header {
            padding: 20px;
            border-bottom: 1px solid #e1e4e8;
            background-color: #f8f9fa;
        }

        .sidebar-header h1 {
            font-size: 1.5rem;
            color: #2c3e50;
            margin-bottom: 5px;
        }

        .sidebar-header p {
            color: #7f8c8d;
            font-size: 0.85rem;
        }

        .notes-list {
            flex: 1;
            overflow-y: auto;
            padding: 12px;
        }

        .note-item {
            padding: 12px;
            border-radius: 6px;
            margin-bottom: 10px;
            background-color: #fff;
            border-left: 3px solid #3498db;
            box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
        }

        .note-item:hover {
            background-color: #f8f9fa;
            transform: translateY(-1px);
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.08);
        }

        .note-item.active {
            background-color: #e8f4fc;
            border-left-color: #2980b9;
        }

        .note-title {
            font-weight: 600;
            font-size: 0.95rem;
            color: #2c3e50;
            margin-bottom: 4px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .note-preview {
            color: #666;
            font-size: 0.85rem;
            line-height: 1.3;
            display: -webkit-box;
            -webkit-line-clamp: 2;
            -webkit-box-orient: vertical;
            overflow: hidden;
        }

        .note-date {
            color: #95a5a6;
            font-size: 0.75rem;
            margin-top: 6px;
        }

        .empty-notes {
            text-align: center;
            color: #bdc3c7;
            padding: 30px 15px;
            font-size: 0.9rem;
        }

        /* 右侧编辑区域 */
        .editor-area {
            flex: 1;
            display: flex;
            flex-direction: column;
            background-color: #fff;
            padding: 20px;
        }

        .editor-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 15px;
            border-bottom: 1px solid #e1e4e8;
        }

        .editor-header h2 {
            color: #2c3e50;
            font-size: 1.4rem;
        }

        .button-group {
            display: flex;
            gap: 8px;
        }

        .editor-button {
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.2s;
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 0.9rem;
        }

        .save-button {
            background-color: #2ecc71;
        }

        .save-button:hover {
            background-color: #27ae60;
        }

        .new-button {
            background-color: #3498db;
        }

        .new-button:hover {
            background-color: #2980b9;
        }

        .editor-button:active {
            transform: translateY(1px);
        }

        .title-input {
            width: 100%;
            padding: 12px 15px;
            font-size: 1.1rem;
            font-weight: 500;
            border: 1px solid #e1e4e8;
            border-radius: 6px;
            margin-bottom: 15px;
            color: #2c3e50;
        }

        .title-input:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.1);
        }

        .note-editor {
            flex: 1;
            width: 100%;
            padding: 20px;
            font-size: 1rem;
            line-height: 1.6;
            border: 1px solid #e1e4e8;
            border-radius: 6px;
            resize: none;
            color: #333;
            background-color: #fff;
        }

        .note-editor:focus {
            outline: none;
            border-color: #3498db;
            box-shadow: 0 0 0 2px rgba(52, 152, 219, 0.1);
        }

        .stats-bar {
            margin-top: 15px;
            display: flex;
            justify-content: space-between;
            color: #95a5a6;
            font-size: 0.85rem;
        }

        .status-indicator {
            display: flex;
            align-items: center;
            gap: 5px;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            background-color: #95a5a6;
        }

        .status-dot.saved {
            background-color: #2ecc71;
        }

        .status-dot.unsaved {
            background-color: #e74c3c;
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .container {
                flex-direction: column;
            }
            
            .notes-sidebar {
                width: 100%;
                max-width: 100%;
                height: 35%;
                border-right: none;
                border-bottom: 1px solid #e1e4e8;
            }
            
            .editor-area {
                height: 65%;
            }
            
            .note-item {
                padding: 10px;
            }
        }

        /* 删除按钮样式 */
        .delete-note {
            position: absolute;
            top: 8px;
            right: 8px;
            background-color: transparent;
            color: #e74c3c;
            border: none;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            opacity: 0;
            transition: opacity 0.2s, background-color 0.2s;
            font-size: 0.8rem;
        }

        .note-item:hover .delete-note {
            opacity: 0.5;
        }

        .delete-note:hover {
            opacity: 1 !important;
            background-color: rgba(231, 76, 60, 0.1);
        }
    </style>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="container">
        <!-- 左侧笔记列表 -->
        <div class="notes-sidebar">
            <div class="sidebar-header">
                <h1><i class="fas fa-book"></i> 笔记</h1>
                <p>点击笔记可重新编辑</p>
            </div>
            <div class="notes-list" id="notesList">
                <!-- 笔记列表将通过JavaScript动态生成 -->
                <div class="empty-notes">
                    <i class="fas fa-sticky-note" style="font-size: 2rem; margin-bottom: 10px;"></i>
                    <p>还没有笔记</p>
                </div>
            </div>
        </div>

        <!-- 右侧编辑区域 -->
        <div class="editor-area">
            <div class="editor-header">
                <h2 id="editorTitle">新建笔记</h2>
                <div class="button-group">
                    <button class="editor-button new-button" id="newNote">
                        <i class="fas fa-plus"></i> 新建
                    </button>
                    <button class="editor-button save-button" id="saveNote">
                        <i class="fas fa-save"></i> 保存
                    </button>
                </div>
            </div>
            
            <input type="text" class="title-input" id="noteTitle" placeholder="笔记标题（可选）...">
            
            <textarea class="note-editor" id="noteEditor" placeholder="输入笔记内容..."></textarea>
            
            <div class="stats-bar">
                <span id="charCount">字符数: 0</span>
                <div class="status-indicator">
                    <span class="status-dot unsaved" id="statusDot"></span>
                    <span id="lastSaved">未保存</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // DOM元素
            const notesList = document.getElementById('notesList');
            const saveButton = document.getElementById('saveNote');
            const newButton = document.getElementById('newNote');
            const noteTitle = document.getElementById('noteTitle');
            const noteEditor = document.getElementById('noteEditor');
            const charCount = document.getElementById('charCount');
            const lastSaved = document.getElementById('lastSaved');
            const editorTitle = document.getElementById('editorTitle');
            const statusDot = document.getElementById('statusDot');
            
            // 当前编辑的笔记状态
            let currentNoteId = null;
            let isNewNote = true;
            let isDirty = false;
            
            // 从localStorage加载笔记或初始化空数组
            let notes = JSON.parse(localStorage.getItem('notes')) || [];
            
            // 初始化显示笔记列表
            renderNotesList();
            
            // 事件监听
            saveButton.addEventListener('click', saveCurrentNote);
            newButton.addEventListener('click', createNewNote);
            
            // 监听输入变化
            noteTitle.addEventListener('input', markAsDirty);
            noteEditor.addEventListener('input', function() {
                updateCharCount();
                markAsDirty();
            });
            
            // 标记内容已更改
            function markAsDirty() {
                if (!isNewNote || noteTitle.value.trim() || noteEditor.value.trim()) {
                    isDirty = true;
                    updateSaveStatus();
                }
            }
            
            // 渲染笔记列表
            function renderNotesList() {
                if (notes.length === 0) {
                    notesList.innerHTML = `
                        <div class="empty-notes">
                            <i class="fas fa-sticky-note" style="font-size: 2rem; margin-bottom: 10px;"></i>
                            <p>还没有笔记</p>
                        </div>
                    `;
                    return;
                }
                
                // 按创建时间降序排序（新的在上面）
                notes.sort((a, b) => new Date(b.createdAt) - new Date(a.createdAt));
                
                const notesHTML = notes.map(note => {
                    // 如果有标题就显示标题，否则显示内容前30个字符
                    const displayTitle = note.title && note.title.trim() 
                        ? note.title 
                        : (note.content.substring(0, 30) + (note.content.length > 30 ? '...' : ''));
                    
                    // 预览内容（如果有标题则显示内容，没有标题则不重复显示）
                    const preview = note.title && note.title.trim()
                        ? (note.content.substring(0, 40) + (note.content.length > 40 ? '...' : ''))
                        : '';
                    
                    return `
                    <div class="note-item ${currentNoteId === note.id ? 'active' : ''}" data-id="${note.id}">
                        <div class="note-title">${displayTitle}</div>
                        ${preview ? `<div class="note-preview">${preview}</div>` : ''}
                        <div class="note-date">${formatDate(note.createdAt)}</div>
                        <button class="delete-note" data-id="${note.id}">
                            <i class="fas fa-trash-alt"></i>
                        </button>
                    </div>
                `}).join('');
                
                notesList.innerHTML = notesHTML;
                
                // 添加点击事件到每个笔记项
                document.querySelectorAll('.note-item').forEach(item => {
                    item.addEventListener('click', function(e) {
                        if (e.target.closest('.delete-note')) return;
                        
                        const noteId = this.getAttribute('data-id');
                        loadNoteForEdit(noteId);
                    });
                });
                
                // 添加删除按钮事件
                document.querySelectorAll('.delete-note').forEach(button => {
                    button.addEventListener('click', function(e) {
                        e.stopPropagation();
                        const noteId = this.getAttribute('data-id');
                        deleteNote(noteId);
                    });
                });
            }
            
            // 保存当前笔记
            function saveCurrentNote() {
                const title = noteTitle.value.trim();
                const content = noteEditor.value.trim();
                
                if (!content) {
                    // 不显示提示框，只是不保存
                    return;
                }
                
                const now = new Date();
                
                if (isNewNote) {
                    // 创建新笔记
                    const noteData = {
                        id: 'note_' + Date.now(),
                        title: title,
                        content: content,
                        createdAt: now.toISOString(),
                        updatedAt: now.toISOString()
                    };
                    
                    // 将新笔记添加到数组开头
                    notes.unshift(noteData);
                    currentNoteId = noteData.id;
                    isNewNote = false;
                } else {
                    // 更新现有笔记
                    const noteIndex = notes.findIndex(n => n.id === currentNoteId);
                    if (noteIndex !== -1) {
                        notes[noteIndex].title = title;
                        notes[noteIndex].content = content;
                        notes[noteIndex].updatedAt = now.toISOString();
                    }
                }
                
                // 保存到localStorage
                localStorage.setItem('notes', JSON.stringify(notes));
                
                // 更新界面
                renderNotesList();
                
                // 更新保存状态
                lastSaved.textContent = `已保存: ${formatTime(now)}`;
                statusDot.className = 'status-dot saved';
                isDirty = false;
            }
            
            // 创建新笔记
            function createNewNote() {
                // 如果有未保存的更改，直接覆盖
                // 不显示确认提示框
                
                // 清空编辑器
                noteTitle.value = '';
                noteEditor.value = '';
                editorTitle.textContent = '新建笔记';
                currentNoteId = null;
                isNewNote = true;
                isDirty = false;
                
                // 更新状态
                updateCharCount();
                updateSaveStatus();
                
                // 取消所有笔记的选中状态
                renderNotesList();
                
                // 自动聚焦到标题输入框
                noteTitle.focus();
            }
            
            // 加载笔记进行编辑
            function loadNoteForEdit(noteId) {
                const note = notes.find(n => n.id === noteId);
                
                if (note) {
                    currentNoteId = noteId;
                    noteTitle.value = note.title || '';
                    noteEditor.value = note.content;
                    editorTitle.textContent = '编辑笔记';
                    isNewNote = false;
                    isDirty = false;
                    
                    // 更新字符计数
                    updateCharCount();
                    
                    // 更新保存状态
                    lastSaved.textContent = `最后保存: ${formatDate(note.updatedAt)}`;
                    statusDot.className = 'status-dot saved';
                    
                    // 重新渲染笔记列表以更新激活状态
                    renderNotesList();
                    
                    // 自动聚焦到内容编辑器
                    noteEditor.focus();
                }
            }
            
            // 删除笔记
            function deleteNote(noteId) {
                // 不显示确认提示框，直接删除
                notes = notes.filter(n => n.id !== noteId);
                localStorage.setItem('notes', JSON.stringify(notes));
                
                // 如果删除的是当前正在编辑的笔记，创建新笔记
                if (currentNoteId === noteId) {
                    createNewNote();
                }
                
                renderNotesList();
            }
            
            // 更新字符计数
            function updateCharCount() {
                const count = noteEditor.value.length;
                charCount.textContent = `字符数: ${count}`;
            }
            
            // 更新保存状态
            function updateSaveStatus() {
                if (isDirty) {
                    statusDot.className = 'status-dot unsaved';
                    lastSaved.textContent = '未保存';
                } else {
                    statusDot.className = 'status-dot saved';
                    if (currentNoteId) {
                        const note = notes.find(n => n.id === currentNoteId);
                        if (note) {
                            lastSaved.textContent = `已保存: ${formatDate(note.updatedAt)}`;
                        }
                    } else {
                        lastSaved.textContent = '已保存';
                    }
                }
            }
            
            // 格式化日期
            function formatDate(dateString) {
                const date = new Date(dateString);
                const now = new Date();
                const diffMs = now - date;
                const diffMins = Math.floor(diffMs / (1000 * 60));
                const diffHours = Math.floor(diffMs / (1000 * 60 * 60));
                const diffDays = Math.floor(diffMs / (1000 * 60 * 60 * 24));
                
                if (diffMins < 1) {
                    return '刚刚';
                } else if (diffMins < 60) {
                    return `${diffMins}分钟前`;
                } else if (diffHours < 24) {
                    return `${diffHours}小时前`;
                } else if (diffDays === 1) {
                    return '昨天';
                } else if (diffDays < 7) {
                    return `${diffDays}天前`;
                } else {
                    return date.toLocaleDateString('zh-CN', {
                        month: 'short',
                        day: 'numeric'
                    });
                }
            }
            
            // 格式化时间
            function formatTime(date) {
                return date.toLocaleTimeString('zh-CN', {
                    hour: '2-digit',
                    minute: '2-digit'
                });
            }
            
            // 添加键盘快捷键
            document.addEventListener('keydown', function(e) {
                if ((e.ctrlKey || e.metaKey) && e.key === 's') {
                    e.preventDefault();
                    saveCurrentNote();
                }
                if ((e.ctrlKey || e.metaKey) && e.key === 'n') {
                    e.preventDefault();
                    createNewNote();
                }
            });
            
            // 初始状态
            updateCharCount();
            updateSaveStatus();
        });
    </script>
</body>
</html>
