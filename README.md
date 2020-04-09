# brid-air-purifier
Just a readme of HTTP requests that are useful when automating your bird air purifier

# Background
I recently bought a [brid air purifier](https://brid.com) and found that the app was nice but not great. I found myself opening the app too often and I wanted to automate stuff.

# How I found this
After I found the ip of my brid, I used tcpdump as follows:

```bash
tcpdump dst 192.168.1.117 -X
```

And there it was: 2 endpoints with very simple content!

# Endpoints
## Change settings
Simple HTTP POST to `/settings` with headers:
```
Content-Type: application/json
Accept: */*
User-Agent: Brid/2.0.5 (iPhone; iOS 13.3.1; Scale/3.00)
Accept-Language: nl-NL;q=1
```

### Normal mode
Body:
```json
{"mode": 2}
```

### Night mode
Body:
```json
{"mode": 4}
```

### Boost mode
Body:
```json
{"mode": 3}
```

### Unnamed mode
(I don't know what it does. It seems louder than normal mode)
Body:
```json
{"mode": 1}
```

### Off
Body:
```json
{"mode": 0}
```

### Light off
Body:
```json
{"light_off": 1}
```

### Light on
Body:
```json
{"light_off": 0}
```

## Read status
GET /status

Example output:
```json
{
    "Time": 1586458099,
    "Sensors": {
        "Live": 1847.18,
        "Quality": 2,
        "Temperature": 23.11,
        "Humidity": 38,
        "CO": 0
    },
    "Settings": {
        "CO Presence": 0,
        "Mode": 4,
        "Light": 0,
        "Modules": 0
    },
    "Filters": {
        "HC filter": 97,
        "NWF filter": 96
    }
}
```

Enjoy!
