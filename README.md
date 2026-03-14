# BotForge Plugins

รวม plugins สำหรับ BotForge - ระบบรวม AI agents มากมาย

## Plugins

| Plugin | คำอธิบาย | MCP Transport |
|--------|---------|---------------|
| [botforge-task-queue](https://github.com/monthop-gmail/botforge-task-queue) | จัดการ long-running tasks ใน LINE Bot แก้ปัญหา webhook timeout | stdio |
| [botforge-network-drive](https://github.com/monthop-gmail/botforge-network-drive) | เข้าถึง SMB/Network Drive, shared folders | Streamable HTTP (port 3002) |

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

## เพิ่ม Plugin ใหม่

สนใจร่วมพัฒนา plugin ใหม่? อ่าน [CONTRIBUTING.md](./CONTRIBUTING.md)

## License

MIT
