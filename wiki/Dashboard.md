# Dashboard

Web-based dashboard for monitoring and managing Loki Mode sessions.

---

## Overview

The Loki Mode dashboard provides:

- Real-time session monitoring
- Kanban-style task management
- Project registry
- Cross-project learnings view

---

## Starting the Dashboard

```bash
# Start dashboard server
loki dashboard start

# With custom port
loki dashboard start --port 8080

# Open in browser
loki dashboard open
```

Default URL: `http://localhost:57374`

---

## Dashboard Views

### Session Monitor

Real-time view of the current session:

| Element | Description |
|---------|-------------|
| Status indicator | Running, paused, stopped |
| Current phase | SDLC phase being executed |
| Task queue | Pending and completed tasks |
| Agent activity | Active agent count and types |
| Log stream | Live log output |

### Kanban Board

Drag-and-drop task management:

| Column | Description |
|--------|-------------|
| Backlog | Unstarted tasks |
| In Progress | Active tasks |
| Review | Tasks awaiting review |
| Done | Completed tasks |

**Keyboard shortcuts:**
- `j/k` - Navigate tasks
- `Enter` - Edit task
- `d` - Delete task
- `m` - Move to next column

### Project Registry

Manage multiple projects:

- View all registered projects
- Check project health
- Sync project data
- Auto-discover projects

### Learnings View

Browse cross-project learnings:

- Filter by type (patterns, mistakes, successes)
- Search learnings
- View statistics
- Export/import learnings

---

## Dashboard CLI Commands

### `loki dashboard start`

Start the dashboard server.

```bash
loki dashboard start [OPTIONS]
```

**Options:**
| Option | Default | Description |
|--------|---------|-------------|
| `--port` | 57374 | Server port |
| `--host` | localhost | Server host |

### `loki dashboard stop`

Stop the dashboard server.

```bash
loki dashboard stop
```

### `loki dashboard status`

Check if dashboard is running.

```bash
loki dashboard status
```

### `loki dashboard url`

Get the dashboard URL.

```bash
loki dashboard url
loki dashboard url --format json
```

### `loki dashboard open`

Open dashboard in default browser.

```bash
loki dashboard open
```

---

## Configuration

### Dashboard Settings

```yaml
# .loki/config.yaml
dashboard:
  port: 57374
  host: localhost
  auto_open: false
  theme: dark
```

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `LOKI_DASHBOARD_PORT` | 57374 | Dashboard port |
| `LOKI_DASHBOARD_HOST` | localhost | Dashboard host |

---

## API Integration

The dashboard uses the HTTP API at port 9898 for data:

```javascript
// Dashboard fetches from API
const status = await fetch('http://localhost:9898/status').then(r => r.json());
const logs = await fetch('http://localhost:9898/logs?lines=100').then(r => r.json());
```

SSE for real-time updates:
```javascript
const events = new EventSource('http://localhost:9898/events');
events.onmessage = (e) => updateUI(JSON.parse(e.data));
```

---

## Troubleshooting

### Dashboard Won't Start

```bash
# Check if port is in use
lsof -i :57374

# Kill existing process
lsof -i :57374 | awk 'NR>1 {print $2}' | xargs kill

# Use different port
loki dashboard start --port 8080
```

### Dashboard Shows No Data

```bash
# Verify API server is running
loki api status

# Start API server
loki serve

# Check status endpoint
curl http://localhost:9898/status
```

### Connection Refused

```bash
# Check dashboard status
loki dashboard status

# Restart dashboard
loki dashboard stop
loki dashboard start
```

---

## See Also

- [[API Reference]] - HTTP API documentation
- [[CLI Reference]] - Dashboard CLI commands
- [[Cross-Project Learning]] - Learnings system
