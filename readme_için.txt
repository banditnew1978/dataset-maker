Windows ortamında powershell kullan admin olarak



git yüklenecek
https://git-scm.com/install/windows
uv yüklenecek
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

Cuda toolkit 12.8 exe olarak 
https://developer.nvidia.com/cuda-12-8-0-download-archive?target_os=Windows&target_arch=x86_64&target_version=11
adresinden indir.

FFmpeg windowsda path kurulu olucak

https://github.com/JarodMica/dataset-maker   adresini clone yap
uv sync yap
bundan sonra problemli olan kısmı gidermek için
uv remove optimum[onnxruntime-gpu]
uv add optimum[onnxruntime-gpu]
huggingface aşağıdaki dosyayı dataset-maker/emilia_models klasörü altında yükle
https://huggingface.co/Jmica/dataset_maker/blob/main/UVR-MDX-NET-Inst_HQ_3.onnx

aşağıdaki adrese gidip grant izin alıp daha sonra sadece read olarak hf token oluştur

https://huggingface.co/pyannote/speaker-diarization-community-1

dataset-maker\Emilia  altında config.example.json dosyasını aç aşağıdaki kısmı bul ve hftoken yaz modelleri indirebilsin diye



    "huggingface_token": "token",
    "filters": {
        "min_duration": 1.5,
        "max_duration": 30,
        "min_dnsmos": 0.5,
        "min_char_count": 1
    }
}

dosyanın ismini config.json yap





bundan sonra datasatmaker içinde 

uv run gradio_interface.py  çalıştır

127.0.0.1:7860 arayüzünde 

New project name yazan yere proje ismini yaz
Create Project de
ses dosyaları uzun olmalı 2 saatten kısa dosyaları Project task altında Combine Small Samples bölümünde combine yap
Daha sonra Transcribe kısmına geç
burada ses dosyalarından altyazıları çıkaracağız.
Language tr seç
Slicing Method Emilia Pipe seç
Emilia Batch Size 16
Emilia Whisper Model large-v3
Eğer ses temiz değil ise arka plan gürltüsü için
Run UVR Seperation tikle
Emilia Whisper Threads 8 olsun
Min Segment Duration (seconds) 0.25
Use File Hash Naming tikli olsun
Verbose Tikli olsun
Start new transcription de

bittiğinde oluşan klasör 

dataset-maker\datasets_folder\hamza\hamza_emilia_dataset

bunu indextts2 için kullanacağız