# Contributing to BotForge Plugins

## ยินดีต้อนรับ!

ขอบคุณที่สนใจร่วมพัฒนา BotForge Plugins! 🎉

## วิธีเพิ่ม Plugin ใหม่

### 1. Fork และ Clone

```bash
git clone https://github.com/monthop-gmail/botforge-plugins.git
cd botforge-plugins
```

### 2. สร้างโครงสร้าง Plugin

```bash
mkdir -p plugins/botforge-<name>
cd plugins/botforge-<name>
```

### 3. เพิ่มไฟล์พื้นฐาน

```
botforge-<name>/
├── __init__.py          # Package init + metadata
├── plugin.py            # Main plugin class
├── mcp_server.py        # MCP server สำหรับ AI agent
├── README.md            # Plugin documentation
├── requirements.txt     # Dependencies
└── examples/            # Usage examples
```

### 4. Metadata ใน `__init__.py`

```python
"""
BotForge <Name> Plugin
คำอธิบายสั้นๆ
"""

__version__ = "1.0.0"
__plugin_name__ = "botforge-<name>"
__plugin_description__ = "คำอธิบาย plugin"
```

### 5. อัปเดต README หลัก

เพิ่ม plugin ของคุณใน `README.md` ของ repo หลัก

### 6. สร้าง Pull Request

```bash
git add -A
git commit -m "feat: Add botforge-<name> plugin"
git push origin main
```

จากนั้นสร้าง PR ที่ GitHub

## Code Style

- ใช้ Python 3.8+
- Type hints เมื่อทำได้
- Docstrings สำหรับ public functions
- Follow PEP 8

## Plugin Ideas

- **botforge-sheets** - Google Sheets integration
- **botforge-database** - Database connections
- **botforge-notification** - Send notifications
- **botforge-scheduler** - Schedule tasks
- **botforge-storage** - Cloud storage integration
- **botforge-api** - HTTP API client
- **botforge-image** - Image processing
- **botforge-pdf** - PDF generation/processing

## License

MIT
