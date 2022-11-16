# Task18

Transcribing a file with LM ASR models

## 2022-11-16T14:55:25

Finding the file: I found 3:

```shell
(base) peterr@kt-gpu-vm-1TB:~/macocu/task18$ ls /home/nikolal/transfer/
sample1.wav  sample2.wav  sample3.wav
```

The files are way oversampled:

```shell
(base) peterr@kt-gpu-vm-1TB:~/macocu/task18$ soxi data/*

Input File     : 'data/sample1.wav'
Channels       : 2
Sample Rate    : 44100
Precision      : 16-bit
Duration       : 00:00:42.03 = 1853440 samples = 3152.11 CDDA sectors
File Size      : 7.41M
Bit Rate       : 1.41M
Sample Encoding: 16-bit Signed Integer PCM


Input File     : 'data/sample2.wav'
Channels       : 2
Sample Rate    : 44100
Precision      : 16-bit
Duration       : 00:00:25.05 = 1104895 samples = 1879.07 CDDA sectors
File Size      : 4.42M
Bit Rate       : 1.41M
Sample Encoding: 16-bit Signed Integer PCM


Input File     : 'data/sample3.wav'
Channels       : 2
Sample Rate    : 44100
Precision      : 16-bit
Duration       : 00:00:26.17 = 1154069 samples = 1962.7 CDDA sectors
File Size      : 4.62M
Bit Rate       : 1.41M
Sample Encoding: 16-bit Signed Integer PCM

Total Duration of 3 files: 00:01:33.25
```

This will be corrected next with `for file in ls *.wav; do cp $file temp; ffmpeg -i temp -ar 16000 -ac 1 "$file"; rm temp; done`

Now all 3 files are correctly sampled. Let's dust off the old code for transcribing.
