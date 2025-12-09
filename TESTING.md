# Testing Free Mode Locally

## Quick Start

1. Update your Zed `settings.json`:

```json
{
  "agent_servers": {
    "Amp": {
      "command": "npx",
      "args": ["-y", "amp-acp"],
      "env": {
        "AMP_EXECUTABLE": "/path/to/amp",
        "AMP_MODE": "free"
      }
    }
  }
}
```

2. Restart Zed's agent or reload settings (cmd+shift+p → "reopen connection")
3. Send a prompt in the agent panel
4. Verify ads appear as formatted markdown messages

## Verification Checklist

- [ ] `AMP_MODE=free` is set in Zed settings
- [ ] Ads display with title, description, and CTA
- [ ] Ad format includes visual separator (`---`) and emoji (📢)
- [ ] CTAs are clickable links
- [ ] Regular agent output still works normally
- [ ] Mode can be switched back to `default` without ads

## Debugging

View adapter logs:
```bash
AMP_EXECUTABLE="/path/to/amp" AMP_MODE="free" node src/index.js 2>&1 | grep -E "\[acp\]|\[amp\]" 
```

Check if Amp CLI is being spawned with the flag:
```bash
# Add temporary logging to src/server.js line 71:
console.error('[amp-acp] Args:', args);
```

Then restart the agent in Zed and check stderr for the args being passed.
