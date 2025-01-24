Audio-to-Subtitle Synchronization System

This project involved the development of a system that converts the audio of a video into accurate subtitles and synchronizes them seamlessly with the video playback. The system ensures that subtitles appear at the bottom of the video in real time, maintaining proper alignment with the audio.

The process consisted of:

Audio Processing and Speech Recognition: Leveraged advanced speech-to-text technologies to transcribe audio into text. The system accurately captured spoken words, including nuances like tone and pauses.
Subtitle Formatting: Parsed the transcribed text into readable and time-coded subtitle segments, ensuring a natural flow for the viewer.
Synchronization: Implemented precise algorithms to sync the subtitles with the video, ensuring they display at the exact moment the corresponding audio is spoken.
User Interface: Designed an intuitive video player that overlays subtitles at the bottom of the screen, enhancing viewer engagement and accessibility.
Key Features:

Real-time audio-to-text transcription.
Automated subtitle generation with time-stamp accuracy.
Integration with various video formats.
Improved accessibility for individuals with hearing impairments or language barriers.
This project showcases expertise in speech recognition, natural language processing, and multimedia application development. It is particularly valuable in media localization, e-learning, and accessibility solutions.

Here's the code:
import whisper

# Load Whisper model
model = whisper.load_model("base", device="cpu")

def convert_to_srt_time(seconds):
    hrs, secs = divmod(seconds, 3600)
    mins, secs = divmod(secs, 60)
    millisecs = int((secs - int(secs)) * 1000)
    return f"{int(hrs):02}:{int(mins):02}:{int(secs):02},{millisecs:03}"
        
# Transcribe audio
result = model.transcribe("audio_file.wav")
with open("subtitles.srt", "w") as f:
    for i, segment in enumerate(result['segments']):
        start = segment['start']
        end = segment['end']
        text = segment['text']
        f.write(f"{i+1}\n")
        f.write(f"{convert_to_srt_time(start)} --> {convert_to_srt_time(end)}\n")
        f.write(f"{text.strip()}\n\n")
import os
print("Saving subtitles to:", os.path.abspath("subtitles.srt"))
