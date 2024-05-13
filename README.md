# incas-israel-hamas-war-concern

## How to build project

* Then download model files from [here](https://drive.google.com/file/d/1iqtNm5GQOSlL-zaqqo6ZgXvKKvZLYlxV/view?usp=drive_link). Please keep the file 'annotate.py' and the folder `incas_tuned_model_ih` in the same directory.

The directory should look like this:

````
incas-israel-hamas-concern
├── incas_tuned_model_ih --place models here
├── Readme.md
├── annotate.py
├── requirements.txt
├── small_sample.jsonl
└── prompt_inference.txt

````
## How to run
```
# Install torch
CPU (win): pip3 install torch torchvision torchaudio
CPU (Linux): pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu
(option) GPU: pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# Install other lib
pip install -r requirements.txt

# Run concern model
python annotate.py --file your_file_name

# (option) Run concern model on GPU
python annotate-gpu.py --file your_file_name

PS. If using the gpu version, please the GPU VRAM > 30GB, such as A100, A40, A6000.
```

The input file parameter is a single dictionary file.

The return value is a dictionary whose keys are message IDs and values are lists of DARPA-defined annotation instances.

## Example
```
python annotate.py --file small_sample.jsonl
```

input:
```
{{"id": "84c8aad06b52235727a1e4f957c7a78f7a023c0d", "contentText": "@POTUS Nice try. In an effort to secure Israel with US weapons, you are ensuring Israel has plenty of bombs to hit Gaza and it\u2019s innocent civilians who have no where to hide."}
```

output:
```
{"concern": {"Zionism": 1, "Antisemitism": 0, "Islamophobia": 0, "Two state solution": 0, "US funding of Israel": 1, "Boycott, Divestment, Sanctions (BDS)": 0, "War": 1, "Religion (Islam, Judaism)": 0, "NoneOther": 0}}
```

