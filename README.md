# AdaIN-VC
This is an unofficial implementation of the paper [One-shot Voice Conversion by Separating Speaker and Content Representations with Instance Normalization](https://arxiv.org/abs/1904.05742) modified from the official one.
<img src="https://github.com/cyhuang-tw/AdaIN-VC/blob/master/model.png" width="400" img align="right">
# Dependencies
- Python >= 3.6
- torch >= 1.4.0
- numpy >= 1.16.0
- librosa >= 0.6.3
- tensorboardX
<br>

# Differences from the official implementation
The main difference from the official implementation is the use of neural vocoder, which greatly improves the audio quality.
I adopted universal vocoder, whose code was from [yistLin/universal-vocoder](https://github.com/yistLin/universal-vocoder) and checkpoint was from [bshall/UniversalVocoding](https://github.com/bshall/UniversalVocoding#pretrained-models).

# Preprocess
The code ```preprocess.py``` is for [CSTR VCTK Corpus](https://datashare.is.ed.ac.uk/handle/10283/3443).
- **--config**: The config of neural vocoder. The format of spectrogram must follow what the vocoder requires.
- **--n_test_speakers**: The number of speakers for testing. Utterances of these speakers are not included in the training set.
- **--valid_proportion**: The proportion of utterances of each speaker used for validation during training.
- **--segment_size**: The size of segments used for training.
- **--train_samples**: The number of samples used for training. Samples are generated by randomly sampling segments from utterances.

# Training
The training starts with either ```main.py``` or ```train.sh```.
- **--config**: The config of AdaIN-VC.
- **--data_dir**: The directory containing processed files generated by ```preprocess.py```.
- **--train_set**: The pkl file containing training data.
- **--train_index_file**: The json file storing sampled indices used for extracting segments.
- **log_dir**: The path for logging.
- **--load_model**: To load a trained model or not. If specified, the path of model must be given via ```--load_path```.
- **--save_path**: The path to save model and optimizer.
- **--load_path**: The path containing the previous model and optimizer.
- **--summary_steps**: To record training information every n steps.
- **--save_steps**: To save the model and optimizer every n steps.
- **--tag**: The tag for tensorboard.
- **--iters**: The number of training steps.

# Inference
You can use ```inference.py``` to perform one-shot voice conversion.
```
python inference.py <model_path> <source> <target> <output>
```
- **model_path**: The path of trained model directory.
- **source**: The source utterance providing linguistic content.
- **tageget**: The utterance providing target speaker timbre.
- **output**: The path of converted utterance.
- **--vocoder_path**: The path of vocoder directory.

# Reference
Please cite the paper if you find AdaIN-VC useful.
```
@article{chou2019one,
  title={One-shot Voice Conversion by Separating Speaker and Content Representations with Instance Normalization},
  author={Chou, Ju-chieh and Yeh, Cheng-chieh and Lee, Hung-yi},
  journal={arXiv preprint arXiv:1904.05742},
  year={2019}
}
```
