# VideoJS Web Player

A powerful web-based video player built with Video.js and Flask that supports various video formats including MP4, WebM, M3U8 (HLS), DASH (MPD), and MKV (via live HLS conversion) along with subtitle support.

## Features

### 1. Video/Subtitle Input & Playback
- Support for video URLs and file uploads
- Support for subtitle URLs and file uploads
- Video.js player with plugins for various formats
- MP4, WebM, M3U8 (HLS), DASH (MPD), MKV (via live HLS conversion)
- Subtitle support with format conversion to VTT

### 2. On-the-Fly MKV to HLS Conversion
- FFmpeg-based conversion of MKV files to HLS
- In-memory storage using /dev/shm for faster streaming
- Efficient caching of converted files

### 3. Subtitle Format Conversion
- Automatic conversion of .srt, .ass, .ssa to WebVTT
- Format detection and handling

### 4. History Tracking
- Last 10 videos played are stored
- Session-based history tracking

### 5. Smart Browser Playback
- Last playback position remembered per video
- Local buffering capabilities
- State restoration on revisit

## Technology Stack

- **Backend**: Flask API
- **Video Processing**: FFmpeg
- **Frontend Player**: Video.js + videojs-contrib-hls + Dash.js
- **Storage**: /dev/shm for in-memory HLS storage
- **Client-side**: JavaScript for caching and position tracking
- **Server-side**: Werkzeug/Flask Cache + Session for history tracking

## Installation

### Prerequisites
- Python 3.7+
- FFmpeg installed on your system
- Docker (optional, for containerized deployment)

### Setup Using Docker (Recommended)

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/videojs-web-player.git
   cd videojs-web-player
   ```

2. Build and run the Docker container:
   ```
   docker build -t videojs-player .
   docker run -p 5000:5000 videojs-player
   ```

3. Access the application at `http://localhost:5000`

### Manual Setup

1. Clone the repository:
   ```
   git clone https://github.com/yourusername/videojs-web-player.git
   cd videojs-web-player
   ```

2. Install FFmpeg if not already installed:
   - Ubuntu/Debian: `sudo apt-get install ffmpeg`
   - macOS: `brew install ffmpeg`
   - Windows: Download from [FFmpeg website](https://ffmpeg.org/download.html)

3. Create a virtual environment and activate it:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

4. Install the required packages:
   ```
   pip install -r requirements.txt
   ```

5. Run the application:
   ```
   python app.py
   ```

6. Access the application at `http://localhost:5000`

## Usage

1. **Load a video via URL**:
   - Enter a video URL in the "Video URL" field
   - Optionally, enter a subtitle URL in the "Subtitle URL" field
   - Click "Play Video"

2. **Upload a video file**:
   - Use the "Upload video file" option to select a video from your computer
   - Optionally, upload a subtitle file
   - Click "Play Video"

3. **MKV Streaming**:
   - The player automatically converts MKV files to HLS for streaming
   - Just provide an MKV file or URL, and the system handles the conversion

4. **Subtitle Management**:
   - Upload or link subtitle files in various formats (.srt, .ssa, .ass)
   - The system automatically converts them to WebVTT

5. **Playback History**:
   - Your last 10 videos are shown in the "Recent Videos" section
   - Click "Play" on any history item to resume watching

## API Endpoints

- `POST /api/upload`: Upload video and subtitle files
- `GET /api/convert_mkv?url=<mkv_url>`: Convert MKV from URL to HLS
- `GET /api/convert_subtitle?url=<subtitle_url>`: Convert subtitle to VTT
- `GET /api/history`: Get user's video history

## File Structure

```
videojs-web-player/
├── app.py                # Main application entry point
├── backend.py            # Backend Flask API
├── Dockerfile            # Docker configuration
├── requirements.txt      # Python dependencies
├── static/               # Static files
│   └── index.html        # Main HTML page
└── templates/            # Flask templates (if needed)
```

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- [Video.js](https://videojs.com/) for the awesome player
- [FFmpeg](https://ffmpeg.org/) for video processing capabilities
- [Flask](https://flask.palletsprojects.com/) for the web framework
