# BotForge Plugins

ที่รวม plugins สำหรับ BotForge - ระบบรวม AI agents มากมาย

## Plugins

### 1. botforge-task-queue

Local plugin สำหรับจัดการ long-running tasks ใน LINE Bot แก้ปัญหา webhook timeout

**Features:**
- ✅ Background task processing
- ✅ Job queue management
- ✅ Progress tracking
- ✅ Job status tracking
- ✅ Push notification เมื่อเสร็จ
- ✅ แก้ปัญหา webhook timeout (10 วินาที)

**Installation:**
```bash
cd /workspace/projects/botforge-plugin
pip install -r requirements.txt
```

**Quick Start:**
```python
from botforge_plugin import TaskQueuePlugin

task_queue = TaskQueuePlugin(bot=line_bot, storage_type="sqlite")

# Submit task
job_id = task_queue.submit(
    user_id="U123456",
    task_type="process_file",
    params={"file": "document.pdf"}
)

# Check status
status = task_queue.get_status(job_id)

# Register task handler
@task_queue.register("process_file")
def process_file(user_id, params):
    result = do_work(params)
    return result
```

**Storage Options:** SQLite (default), Redis

**MCP Server (stdio):** `python mcp_server.py`

| MCP Tool | Description |
|----------|-------------|
| `task_queue_submit` | ส่งงานใหม่เข้าคิว |
| `task_queue_status` | ตรวจสอบสถานะงาน |
| `task_queue_result` | ดึงผลลัพธ์ |
| `task_queue_cancel` | ยกเลิกงาน |
| `task_queue_user_jobs` | ดูงานทั้งหมดของ user |

[ดูเอกสารเพิ่มเติม](./plugins/botforge-task-queue/README.md)

---

### 2. botforge-network-drive

SMB/Network Drive plugin สำหรับ BotForge - เข้าถึง shared folders และ network drives

**Features:**
- ✅ เชื่อมต่อ SMB/CIFS shares (v1/v2/v3)
- ✅ อ่าน/เขียนไฟล์บน network drive
- ✅ ดูรายการไฟล์และโฟลเดอร์
- ✅ ค้นหาไฟล์
- ✅ Upload/Download ไฟล์
- ✅ Progress tracking สำหรับไฟล์ใหญ่
- ✅ รองรับ multiple connections
- ✅ NTLM/NTLMv2 authentication + SMB Encryption

**Installation:**
```bash
pip install -r requirements.txt
```

**Quick Start:**
```python
from botforge_network_drive import NetworkDrivePlugin

drive = NetworkDrivePlugin()

# เพิ่ม connection
drive.add_connection(
    name="office-server",
    server="192.168.1.100",
    share="SharedFolder",
    username="user",
    password="pass"
)

# ดูรายการไฟล์
files = drive.list_files("office-server", "/documents")

# อ่านไฟล์
content = drive.read_file("office-server", "/documents/report.pdf")

# ค้นหาไฟล์
results = drive.search("office-server", "*.pdf", "/documents")
```

**MCP Server (Streamable HTTP):** `python mcp_server.py` (port 3002)

| MCP Tool | Description |
|----------|-------------|
| `drive_add_connection` | เพิ่ม SMB connection |
| `drive_remove_connection` | ลบ connection |
| `drive_list_connections` | ดูรายการ connections |
| `drive_list_files` | ดูรายการไฟล์ |
| `drive_read_file` | อ่านไฟล์ (text/base64) |
| `drive_write_file` | เขียนไฟล์ (text/base64) |
| `drive_delete_file` | ลบไฟล์ |
| `drive_create_folder` | สร้างโฟลเดอร์ |
| `drive_delete_folder` | ลบโฟลเดอร์ |
| `drive_get_file_info` | ดูข้อมูลไฟล์ |
| `drive_search` | ค้นหาไฟล์ |

[ดูเอกสารเพิ่มเติม](./plugins/botforge-network-drive/README.md)

---

## MCP Configuration

### task-queue (stdio)
```json
{
  "mcpServers": {
    "task-queue": {
      "command": "python",
      "args": ["mcp_server.py"],
      "cwd": "/path/to/botforge-task-queue"
    }
  }
}
```

### network-drive (Streamable HTTP)
```json
{
  "mcpServers": {
    "network-drive": {
      "url": "http://localhost:3002/mcp"
    }
  }
}
```

---

## เพิ่ม Plugin ใหม่

สนใจร่วมพัฒนา plugin ใหม่? อ่าน [CONTRIBUTING.md](./CONTRIBUTING.md)

### โครงสร้าง

```
botforge-plugins/
├── plugins/
│   ├── botforge-task-queue/
│   ├── botforge-network-drive/
│   ├── botforge-<name>/
│   └── ...
├── docs/
└── README.md
```

### การตั้งชื่อ

- **Plugin name:** `botforge-<name>` (เช่น `botforge-task-queue`)
- **Package:** `botforge_<name>` (เช่น `botforge_task_queue`)

## License

MIT
