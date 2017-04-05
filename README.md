# up_emotions_audio
This RESTful webservice aims to extract arousal and valence from audio.
The input argument is either an uploaded audio/video file to the server or a URL. The output is the predicted emotion in terms of Arousal and Valence within the JSON-LD format.

To set up the module, you need:

- change the content of the 'rest_vars' pointing to 'classifiers' directory and an empty 'download' directory.

- define the path to the 'rest_vars' in the er/src/com/opensmile/maven/path.java as 'var_file' value.

- change the directory of 'weka' in the 'classifiers/RF_models/run_*.sh'

- if using your own asr, change the bash commands in 'classifiers/asr/*.sh' file to your own asr service.

Example:

    http://localhost:8888/er/aer/getdims?dims=arousal,valence&url=http://tv-download.dw.com/dwtv_video/flv/wikoe/wikoe20151114_wiruebli_sd_avc.mp4&timing=9,15;147,152

where:

    getdims: desired dimensions separated by comma (arousal,valence)

    url: the url of the video/audio or the name of the uploaded file

    timing: start and end of the segments (in seconds): start1,end1;start2,end2, it can be also 'asr' if ASR is available.


To upload an audio/video file use curl:

    Windows: curl -v -H "Content-Type:multipart/form-data" --user meuser -i -X POST -F "file=@D:\path\to\sample.wav" http://localhost:8888/er/aer/upload

    Linux: curl -v -H "Content-Type:multipart/form-data" --user meuser -i -X POST -F 'file=@./sample.wav' http://localhost:8888/er/aer/upload

Moreover, this repository handles the fusion of audio and video outputs.

    See http://localhost:8888/er/general for more information


Licenses:

openSMILE:
    distributed free of charge for research and personal use (http://www.audeering.com/research-and-open-source/files/openSMILE-open-source-license.txt)
    WEKA
    GPL 3

In case of using this module, please cite the following papers:

    EYBEN, F., WENINGER, F., GROSS, F., AND SCHULLER, B. Recent Developments in openSMILE, the Munich Open-Source Multimedia Feature Extractor. In Proceedings of the 21st ACM International Conference on Multimedia, MM 2013 (Barcelona, Spain, October 2013), ACM, ACM, pp. 835–838.
    SCHMITT, M., RINGEVAL, F., AND SCHULLER, B. At the Border of Acoustics and Linguistics: Bag-of-Audio-Words for the Recognition of Emotions in Speech. In Proceedings INTERSPEECH 2016, 17th Annual Conference of the International Speech Communication Association
