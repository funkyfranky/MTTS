This python script converts text to speech using the Google Cloud engine. Furthermore, radio effects (high, low pass filters and white noise) can be added to the speech output.
The input text is read from an Excel or csv file.

# Data Table
The input data is provided as a table in either `xlsx` or `csv format:

![image](https://github.com/funkyfranky/MTTS/assets/28947887/79ca2b46-cd24-493e-84c4-598ef34b3958)

The `xlsx` or `csv` files need to have the following columns:
* `Text`: The text that is converted to speech. This can contain SSML syntax.
* `File Name`: The output file name. This will be saved as in `.ogg` format.
* `Subtitle`: An optional subtitle if different from the `Text` column.
* `Voice Name`: The Google voice if other than the default voice `en-US-Standard-A`.
* `Highpass`: The high pass filter frequency in Hz. Default 4000 Hz.
* `Lowpass`: The low pass filter frequency in Hz. Default 3000 Hz.
* `Nfilter`: Number of times the high and or low pass filters are applied. Default 3.
* `Volume Boost`: The volume boost in dB applied to the final normalized output. Default 0 dB.
* `Noise Boost`: The white noise boost in [dB]. Default `None`. If set, white noise is added. Try a negative value of -25 dB first.
* `Emphasis`: Add emphasis to the voice, c.f. https://cloud.google.com/text-to-speech/docs/ssml#emphasis.
* `Rate`: Adjust speech rate, c.f. https://cloud.google.com/text-to-speech/docs/ssml#prosody
* `Pitch`: Adjust the pitch of the voice, c.f. https://cloud.google.com/text-to-speech/docs/ssml#prosody
* `Click In`: Add a radio click at the beginning of the sound file.
* `Click Out`: Add a radio click at the end of the sound file.

# Usage
Change to the directory, where the mtts.py file is located and type
```
python mtts.py --credentials X:\<Path to JSON file>\google-credentials.json
```
where the parameter `--credentials` points to your Google cloud credentials file. Alternatively, you can set the environment variable `GOOGLE_APPLICATION_CREDENTIALS` to point to the credentials file.

This will scan the current directory for all `xlsx` files and start the conversion process.
For each input files, a directory named as the input file is created that contains the sound `.ogg` files.
Additionally, a `csv` file with the parameters is created that also contains the duration of the sound file as additional column.
This `csv` file can be used as input for various MOOSE classes (e.g. ATIS, RANGE, AIRBOSS).

## Command Line Parameters
The following command line parameters can be used:
* `--filetype`: Specify whether you want Excel `xlsx` or comma-separated value `csv` files as input.
* `--inputdir`: Specify the path of the directory where the input files are located.
* `--inputfile`: Specify the path to a single input file (if you do not want to convert all files in a directory).
* `--credentials`: Path to your Google credentials file.

### Specify File Type
```
python mtts.py --filetype csv
```
### Specify Input Directory
```
python mtts.py --inputdir <Path To Input Files>
```
### Specify Input File
```
python mtts.py --inputfile <Path to Input File>
```
