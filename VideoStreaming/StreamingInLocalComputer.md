```bash
Web Camera
  |
  |--> Capture Video (C# Application)
  |
  v
C# Application (Running on the same computer)
  |
  |--> Encode Video (Optional, for format compatibility)
  |      (Use FFmpeg if encoding is needed)
  |
  |--> Serve Video Stream (Using WebSockets or HTTP Server)
  |
  v
Web Browser (On the same computer)
  |
  |--> Display Video
        (Using HTML5 <video> or <img> element)
```
