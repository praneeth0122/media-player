# media-player
# Media Player App Documentation

## 📌 Project Title: Media Player App

## 🎯 Objective
To develop a mobile application capable of playing audio files from local storage, with essential media controls including play, pause, and skip.

## 🛠️ Technologies Used
- **Language**: Kotlin
- **IDE**: Android Studio
- **UI Layout**: XML
- **Media Playback**: Android MediaPlayer API
- **Storage Access**: Local (res/raw)

---

## 📲 Features
- **Audio Playback**: Play MP3/WAV files from local resources.
- **Media Controls**:
  - Play
  - Pause
  - Skip (next track)
- **User Interface**: Minimal and functional with three buttons.
- **MediaPlayer Lifecycle Management**: Proper handling on destruction.

---

## 🧱 Project Files and Structure

### AndroidManifest.xml
```xml
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```

### activity_main.xml
```xml
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:gravity="center"
    android:padding="16dp">

    <Button
        android:id="@+id/btnPlay"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Play" />

    <Button
        android:id="@+id/btnPause"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Pause" />

    <Button
        android:id="@+id/btnSkip"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Skip" />
</LinearLayout>
```

### MainActivity.kt
```kotlin
package com.example.mediaplayer

import android.media.MediaPlayer
import android.os.Bundle
import android.widget.Button
import androidx.appcompat.app.AppCompatActivity

class MainActivity : AppCompatActivity() {

    private lateinit var mediaPlayer: MediaPlayer
    private var currentTrackIndex = 0
    private val trackList = listOf(
        R.raw.audio1, R.raw.audio2, R.raw.audio3
    )

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val playButton: Button = findViewById(R.id.btnPlay)
        val pauseButton: Button = findViewById(R.id.btnPause)
        val skipButton: Button = findViewById(R.id.btnSkip)

        mediaPlayer = MediaPlayer.create(this, trackList[currentTrackIndex])

        playButton.setOnClickListener {
            if (!mediaPlayer.isPlaying) {
                mediaPlayer.start()
            }
        }

        pauseButton.setOnClickListener {
            if (mediaPlayer.isPlaying) {
                mediaPlayer.pause()
            }
        }

        skipButton.setOnClickListener {
            mediaPlayer.stop()
            mediaPlayer.reset()
            currentTrackIndex = (currentTrackIndex + 1) % trackList.size
            mediaPlayer = MediaPlayer.create(this, trackList[currentTrackIndex])
            mediaPlayer.start()
        }
    }

    override fun onDestroy() {
        super.onDestroy()
        if (::mediaPlayer.isInitialized) {
            mediaPlayer.release()
        }
    }
}
```

---

## 📂 Project Structure Summary
```
com.example.mediaplayer/
├── MainActivity.kt
├── res/
│   ├── layout/
│   │   └── activity_main.xml
│   ├── raw/
│       ├── audio1.mp3
│       ├── audio2.mp3
│       └── audio3.mp3
├── AndroidManifest.xml
```

---

## ✅ Deliverables
- Functional APK of Media Player App.
- Project Source Code including all resources.
- Tested audio playback with clean UI.

---

## 🔄 Future Improvements
- Add seek bar and volume control.
- Dynamic file picker for choosing audio.
- Add album art and metadata support.
- Background playback with notification controls.

---

## 📅 Submission Info
- **Submitted to**: CODTECH
- **Developed by**: [Your Name Here]
- **Date**: [Submission Date]

> ✅ Ensure that audio files like `audio1.mp3`, `audio2.mp3` are placed inside `res/raw`.

---

**End of Documentation**
