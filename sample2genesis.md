---
layout: default
---

# Audio Sample to Genesis Synthesis Estimator

## Personal project, September 2022 - Present

Objective: Given an audio sample, use neural networks to predict the YM2612 synthesizer chip registers (settings) needed to replicate the sound (or a close approximation of it).

Progress:

- Preprocessed audio sample data taken from Sega Genesis audio output by analyzing spectra, identifying the samples’ fundamental frequencies, and applying dimension reduction techniques to the raw audio sample data.

- Trained neural network models on the spectra, reduced audio data, and YM2612 synthesizer chip registers.

Latest update:

(October 17, 2022) I am currently putting this project on hold while I devise a scalable solution to collect more audio samples for the Y12 files contained in the training data set. I currently have about 550 samples, and I have about 5,000 Y12 files that do not yet have samples. See the README.MD in the GitHub repository for more information.

### Background

Sega Enterprises released the Mega Drive in Japan in October 1988, and in North America in August 1989, rebranded as the Genesis. Its onboard audio hardware included, in addition to the SN76496 PSG chip used in the Sega Master System, the Yamaha YM2612, a 6-channel frequency-modulation (FM) synthesizer chip.

Frequency modulation synthesis, to be brief, is fast vibrato applied to a primitive sound wave (called the *carrier*). This vibrato comes in the form of another sound wave (called the *modulator*). Usually, sine waves are used in both roles, though many professional FM synthesizers allow square, triangle, sawtooth or other simple waveforms to be used as well. At lower frequencies, the modulation simply causes audible vibrato (the pitch moves up and down), but at faster frequencies, one begins to hear a new kind of sound, but at the original carrier's pitch with no audible vibrato. With this technique, a much wider range of sounds is possible than, for instance, additive synthesis, which is limited to adding sine waves together.

The YM2612 chip in the Sega Genesis has 6 channels for FM, each capable of producing one type of sound at a time. Within each channel, 4 sine waves are used (called *operators*). *How* they are used depends on the *algorithm* chosen: for example, algorithm 7 is simply adding the four operators together, while algorithm 4 is two modulator-carrier pairs added together.

Throughout the Genesis' tenure in the early 1990s, many Western developers struggled with creating sounds using FM synthesis, and opted instead to use preset libraries provided by, for instance, the Sega GEMS (Genesis Editor for Music and Sound Effects) tool. Even understanding the mathematics involved does not help musicians who are just starting out with FM. (This is history repeating itself, as most professional users of the famous Yamaha DX7 FM synthesizer rarely ventured beyond the factory preset patches. Many songs from the most famous artists of the 1980s feature these same sounds.)

### What is this project?

Given an audio sample of some instrument or sound, can we train a neural network to predict the appropriate register inputs for the YM2612 chip to replicate it?

The training data consists of:

- Many instrument patches, stored in the Y12 file format (target data)

- Recorded audio samples of each instrument patch being played for almost a second (feature data). To keep things simple, every instrument plays a 4th octave C.

- To start off, I used PCA (principal component analysis) on the audio sample data, reducing the dimensions from ~35,000 to only 64, with ~91% explained variance (and harshly diminishing returns beyond that point- see the Jupyter notebook for this step for details).

As mentioned above, the chip is capable of producing sounds with 4 sine wave operators, used in algorithms ranging from simple additive synthesis (algorithm 7) to a single modulation chain (algorithm 0). There is significant overlap between the sound capabilities of the algorithms (for instance, many algorithm 0 sounds could be produced just as well with algorithm 4). To avoid confusion stemming from this, 8 models will be constructed, one for each algorithm, and the training data will be split according to how it was produced.

For the models, I used a neural network of depth 4. I have not conducted rigorous analysis on the accuracy yet because...

### Current status as of October 17, 2022: model constructed, but need many more instrument patches/samples!

Currently, I have around 560 instruments in the training set, only 13 of which were produced with algorithm 7. This leaves approximately 78 instruments on average for each of the other algorithms. This is nowhere near enough to train a neural network, so I am pausing this project while I devise a scalable means of recording audio samples of each of the remaining 5,000 Y12 patch files I plan to use.

My proposed solution is to write a Genesis program that contains the entire patch collection I wish to use (I have around 5,600 patches) and plays a 4th octave C with each patch for about a second, one after the other (in Windows directory order, so I don't have to sort anything). After compiling the ROM, I can run it on a sound-accurate Genesis emulator (like Regen, for instance), while Audacity records the output. Then a simple Python loop can separate the (large) WAV file into individual files. My original motivation for this project was to use it to create instrument patches for Genesis homebrew projects, so I look forward to putting some of those 68K assembly programming skills I've learned to practice!

[back](./)
