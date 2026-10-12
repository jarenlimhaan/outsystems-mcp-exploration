# Read-only connection check

Captured during the retrospective reconstruction on 10 October 2026.

Request: list the modules currently loaded in Service Studio.

Sanitized result:

```json
{
  "apps": [
    {
      "name": "EmployeeTest",
      "kind": "eSpace",
      "isOpen": true,
      "isReference": false,
      "moduleType": "Service"
    }
  ]
}
```

No mutation or publish tool was called. The module key was omitted because it adds no value to the demonstration.
