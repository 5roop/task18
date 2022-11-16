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


## 2022-11-16T15:35:23 results:

|    | model                                           | file        | transcription                                                                                                                                                                                                                                                                                                                                                                                                                                   |
|---:|:------------------------------------------------|:------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  0 | classla/wav2vec2-large-slavic-parlaspeech-hr-lm | sample1.wav | a spominjalo se specijalitet iz svog mjesta ali možete mi reći kako se priprema specijalitet je ovog mjesta za dobro mislite na ovu pogače pa pripremaju se u onoj velikoj pećipožseskajma sad ne znam kako ste u prav a što se tiče možda vaših omenjenihtee možete reći o tom području volim gledat ocshopove volim taj tip odnosa s gostom filmom domaće filmove najviše moj najdraži domaći film ironično ima naziv na engleskom za se gost |
|  1 | classla/wav2vec2-xls-r-parlaspeech-hr-lm        | sample1.wav | a cili specijalitet zbog mjesta zove se dobro mislite ne vi pogače pa pripremaju se onoj velikoj peći žuseskajmakom sa ne znam kako se pravi što se tiče volim gledati okove taj tip odnosa s gostom dva domaće move najviše najdraži domaće ironično ima naszid na engleskom zove se ga est                                                                                                                                                    |
|  2 | classla/wav2vec2-large-slavic-parlaspeech-hr-lm | sample2.wav | a sada ložite i prepričajte me priču što više možete možete koristiti sve pojedinosti koje znate u priči i slikalo koje ste upravo poklodali dakle postao jedan otok i postao je jedan svjetionik svjetionik je bio bijeli i na vrhu je postao taj dio pomoću kojeg se odražava i projicira svjetnost i pored svetionika je postala jedna kućica                                                                                                |
|  3 | classla/wav2vec2-xls-r-parlaspeech-hr-lm        | sample2.wav | dakle postao je jedan otok i postao je jedan svjetionik setionik je bio bijeli i na vrhu je postao taj dio pomoć kojeg se država i projicira svjetlost i pored setljonika je postala jedna kućica a                                                                                                                                                                                                                                             |
|  4 | classla/wav2vec2-large-slavic-parlaspeech-hr-lm | sample3.wav | dakle bio je vrući dan i postojala jedna žena ptica koja je bila žena tog grućeg dana međutim nije nigdje mogla pronaći nikakvu vodu i onda je oda u park gdje je ispunjene klupe i vidjela vrćsuvodu kad je došlo do tog vrćasjala je na njega i osjetila je da tu na puno bolje i svojim kljunom nije mogla dohvatiti jer je ta voda bila pred nju                                                                                            |
|  5 | classla/wav2vec2-xls-r-parlaspeech-hr-lm        | sample3.wav | dakle bio je vrući dan i postojala je jedna jedna ptica koja bila jedna tog vrućih dana međutim nije nigdje mogla pronać nikakvu vodu i onda je odšla park gdje je istodjednem klupe vidjela vrćsvodum kad je došlo do tog vrćasjela je na njega i osjetila je da tu nema puno bode i svojim klunom nije mogla dohvatiti jer je ta voda bila pri nu                                                                                             |
