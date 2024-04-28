This repo is based on https://github.com/karpathy/nanoGPT (Original repo)

WINDOWS TERMINAL 
- python3 -m venv venv
- cd venv
- cd Scripts
- activate.bat
- cd ../..
- pip install -r requirements.txt

- git clone https://github.com/cccntu/minLoRA.git
- cd minLoRA
- pip install -e .

- python data/mitos/prepare.py
- python train.py config/train_mitos.py --compile=False
- python sample.py --out_dir=out-mitos
- deactivate.bat

UBUNTU TERMINAL
# With installation of venv 
in windows cmd : pip install venv
in ubuntu terminal : 
- cd /mnt/c/Users/user/Desktop/LoRAnanoGPT
- python3 -m venv venv
- source venv_ubuntu/bin/activate
- pip install -r requirements.txt

- git clone https://github.com/cccntu/minLoRA.git
- cd minLoRA
- pip install -e .

- python data/mitos/prepare.py
- python train.py config/train_mitos.py
- python sample.py --out_dir=out-mitos
- deactivate

# How to run it in ubuntu terminal 
- cd /mnt/c/Users/user/Desktop/LoRAnanoGPT
- source venv_ubuntu/bin/activate
- python data/mitos/prepare.py
- python train.py config/train_mitos.py
- python sample.py --out_dir=out-mitos
- deactivate

# Results after training the model
# - python train.py config/train_mitos.py : 

Overriding config with config/train_mitos.py:
# train a miniature character-level mitos model
# good for debugging and playing on macbooks and such

out_dir = 'out-mitos'
eval_interval = 250 # keep frequent because we'll overfit
eval_iters = 200
log_interval = 10 # don't print too too often

# we expect to overfit on this small dataset, so only save when val improves
always_save_checkpoint = False

wandb_log = False # override via command line if you like
wandb_project = 'mitos'
wandb_run_name = 'mini-gpt'

dataset = 'mitos'
batch_size = 64
block_size = 256 # context of up to 256 previous characters

# baby GPT model :)
n_layer = 6
n_head = 6
n_embd = 384
dropout = 0.2

learning_rate = 1e-3 # with baby networks can afford to go a bit higher
max_iters = 5000
lr_decay_iters = 5000 # make equal to max_iters usually
min_lr = 1e-4 # learning_rate / 10 usually
beta2 = 0.99 # make a bit bigger because number of tokens per iter is small

warmup_iters = 100 # not super necessary potentially

# on macbook also add
device = 'cuda'  # run on cpu only
compile = False # do not torch compile the model

use_lora = False
found vocab_size = 139 (inside data/mitos/meta.pkl)
Initializing a new model from scratch
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
number of parameters: 10.68M
using fused AdamW: True
step 0: train loss 5.0025, val loss 5.0028
iter 0: loss 5.0025, time 40737.26ms, mfu -100.00%
iter 10: loss 3.6716, time 6708.79ms, mfu 2.23%
iter 20: loss 2.9952, time 6703.88ms, mfu 2.23%
iter 30: loss 2.6935, time 6705.07ms, mfu 2.23%
iter 40: loss 2.5150, time 6703.98ms, mfu 2.23%
iter 50: loss 2.4117, time 6717.67ms, mfu 2.23%
iter 60: loss 2.3996, time 6721.03ms, mfu 2.23%
iter 70: loss 2.3485, time 6717.64ms, mfu 2.23%
iter 80: loss 2.2566, time 6718.80ms, mfu 2.23%
iter 90: loss 2.2037, time 6717.81ms, mfu 2.23%
iter 100: loss 2.0694, time 6718.57ms, mfu 2.23%
iter 110: loss 1.9815, time 6716.75ms, mfu 2.23%
iter 120: loss 1.9622, time 6717.01ms, mfu 2.23%
iter 130: loss 1.8122, time 6717.37ms, mfu 2.23%
iter 140: loss 1.6903, time 6721.75ms, mfu 2.23%
iter 150: loss 1.6257, time 6717.90ms, mfu 2.22%
iter 160: loss 1.5085, time 6718.14ms, mfu 2.22%
iter 170: loss 1.4489, time 6718.69ms, mfu 2.22%
iter 180: loss 1.3855, time 6717.38ms, mfu 2.22%
iter 190: loss 1.2516, time 6717.50ms, mfu 2.22%
iter 200: loss 1.1449, time 6717.54ms, mfu 2.22%
iter 210: loss 1.0799, time 6717.84ms, mfu 2.22%
iter 220: loss 1.0807, time 6716.68ms, mfu 2.22%
iter 230: loss 1.0384, time 6721.05ms, mfu 2.22%
iter 240: loss 0.9533, time 6715.90ms, mfu 2.22%
step 250: train loss 0.7471, val loss 0.9479
saving checkpoint to out-mitos
iter 250: loss 0.9043, time 31799.67ms, mfu 2.05%
iter 260: loss 0.8266, time 6716.18ms, mfu 2.07%
iter 270: loss 0.8174, time 6715.48ms, mfu 2.08%
iter 280: loss 0.7563, time 6718.96ms, mfu 2.10%
iter 290: loss 0.6935, time 6715.23ms, mfu 2.11%
iter 300: loss 0.6274, time 6716.12ms, mfu 2.12%
iter 310: loss 0.6251, time 6716.82ms, mfu 2.13%
iter 320: loss 0.6223, time 6717.24ms, mfu 2.14%
iter 330: loss 0.5483, time 6718.06ms, mfu 2.15%
iter 340: loss 0.5376, time 6715.99ms, mfu 2.16%
iter 350: loss 0.4770, time 6716.76ms, mfu 2.16%
iter 360: loss 0.4790, time 6719.92ms, mfu 2.17%
iter 370: loss 0.4299, time 6717.46ms, mfu 2.17%
iter 380: loss 0.3885, time 6717.67ms, mfu 2.18%
iter 390: loss 0.3857, time 6718.04ms, mfu 2.18%
iter 400: loss 0.3525, time 6715.69ms, mfu 2.19%
iter 410: loss 0.3388, time 6716.22ms, mfu 2.19%
iter 420: loss 0.3193, time 6717.46ms, mfu 2.20%
iter 430: loss 0.2806, time 6715.48ms, mfu 2.20%
iter 440: loss 0.2580, time 6718.69ms, mfu 2.20%
iter 450: loss 0.2444, time 6716.95ms, mfu 2.20%
iter 460: loss 0.2155, time 6716.35ms, mfu 2.21%
iter 470: loss 0.2082, time 6718.31ms, mfu 2.21%
iter 480: loss 0.1994, time 6717.20ms, mfu 2.21%
iter 490: loss 0.1900, time 6717.11ms, mfu 2.21%
step 500: train loss 0.0866, val loss 0.6678
saving checkpoint to out-mitos
iter 500: loss 0.1791, time 31834.30ms, mfu 2.04%
iter 510: loss 0.1616, time 6715.98ms, mfu 2.06%
iter 520: loss 0.1593, time 6716.83ms, mfu 2.07%
iter 530: loss 0.1554, time 6716.80ms, mfu 2.09%
iter 540: loss 0.1502, time 6716.91ms, mfu 2.10%
iter 550: loss 0.1326, time 6718.11ms, mfu 2.11%
iter 560: loss 0.1309, time 6715.76ms, mfu 2.12%
iter 570: loss 0.1289, time 6717.23ms, mfu 2.13%
iter 580: loss 0.1303, time 6720.34ms, mfu 2.14%
iter 590: loss 0.1185, time 6711.59ms, mfu 2.15%
iter 600: loss 0.1096, time 6716.90ms, mfu 2.16%
iter 610: loss 0.1151, time 6716.29ms, mfu 2.17%
iter 620: loss 0.1146, time 6717.33ms, mfu 2.17%
iter 630: loss 0.1046, time 6716.19ms, mfu 2.18%
iter 640: loss 0.1047, time 6720.04ms, mfu 2.18%
iter 650: loss 0.0970, time 6718.01ms, mfu 2.19%
iter 660: loss 0.0990, time 6720.55ms, mfu 2.19%
iter 670: loss 0.0949, time 6716.99ms, mfu 2.19%
iter 680: loss 0.0921, time 6718.34ms, mfu 2.20%
iter 690: loss 0.0938, time 6717.38ms, mfu 2.20%
iter 700: loss 0.0926, time 6716.87ms, mfu 2.20%
iter 710: loss 0.0892, time 6716.76ms, mfu 2.20%
iter 720: loss 0.0820, time 6716.27ms, mfu 2.21%
iter 730: loss 0.0800, time 6716.01ms, mfu 2.21%
iter 740: loss 0.0862, time 6718.91ms, mfu 2.21%
step 750: train loss 0.0519, val loss 0.8286
iter 750: loss 0.0833, time 31328.46ms, mfu 2.04%
iter 760: loss 0.0816, time 6717.95ms, mfu 2.05%
iter 770: loss 0.0802, time 6717.85ms, mfu 2.07%
iter 780: loss 0.0770, time 6716.84ms, mfu 2.09%
iter 790: loss 0.0748, time 6719.66ms, mfu 2.10%
iter 800: loss 0.0828, time 6715.99ms, mfu 2.11%
iter 810: loss 0.0766, time 6717.86ms, mfu 2.12%
iter 820: loss 0.0818, time 6716.84ms, mfu 2.13%
iter 830: loss 0.0755, time 6716.00ms, mfu 2.14%
iter 840: loss 0.0726, time 6715.98ms, mfu 2.15%
iter 850: loss 0.0725, time 6710.67ms, mfu 2.16%
iter 860: loss 0.0732, time 6716.67ms, mfu 2.17%
iter 870: loss 0.0717, time 6717.59ms, mfu 2.17%
iter 880: loss 0.0739, time 6717.33ms, mfu 2.18%
iter 890: loss 0.0702, time 6716.71ms, mfu 2.18%
iter 900: loss 0.0699, time 6717.49ms, mfu 2.19%
iter 910: loss 0.0701, time 6716.22ms, mfu 2.19%
iter 920: loss 0.0651, time 6716.98ms, mfu 2.19%
iter 930: loss 0.0665, time 6718.90ms, mfu 2.20%
iter 940: loss 0.0713, time 6718.67ms, mfu 2.20%
iter 950: loss 0.0661, time 6716.75ms, mfu 2.20%
iter 960: loss 0.0690, time 6720.60ms, mfu 2.20%
iter 970: loss 0.0687, time 6718.82ms, mfu 2.21%
iter 980: loss 0.0656, time 6718.16ms, mfu 2.21%
iter 990: loss 0.0701, time 6717.00ms, mfu 2.21%
step 1000: train loss 0.0465, val loss 0.9108
iter 1000: loss 0.0624, time 31330.51ms, mfu 2.04%
iter 1010: loss 0.0644, time 6720.61ms, mfu 2.05%
iter 1020: loss 0.0655, time 6717.34ms, mfu 2.07%
iter 1030: loss 0.0649, time 6717.90ms, mfu 2.09%
iter 1040: loss 0.0633, time 6717.30ms, mfu 2.10%
iter 1050: loss 0.0593, time 6716.54ms, mfu 2.11%
iter 1060: loss 0.0661, time 6716.27ms, mfu 2.12%
iter 1070: loss 0.0599, time 6717.80ms, mfu 2.13%
iter 1080: loss 0.0612, time 6716.19ms, mfu 2.14%
iter 1090: loss 0.0604, time 6719.19ms, mfu 2.15%
iter 1100: loss 0.0614, time 6716.19ms, mfu 2.16%
iter 1110: loss 0.0601, time 6717.08ms, mfu 2.17%
iter 1120: loss 0.0592, time 6717.30ms, mfu 2.17%
iter 1130: loss 0.0592, time 6716.65ms, mfu 2.18%
iter 1140: loss 0.0597, time 6717.80ms, mfu 2.18%
iter 1150: loss 0.0560, time 6716.44ms, mfu 2.19%
iter 1160: loss 0.0594, time 6717.33ms, mfu 2.19%
iter 1170: loss 0.0609, time 6717.64ms, mfu 2.19%
iter 1180: loss 0.0596, time 6716.35ms, mfu 2.20%
iter 1190: loss 0.0575, time 6715.71ms, mfu 2.20%
iter 1200: loss 0.0570, time 6716.33ms, mfu 2.20%
iter 1210: loss 0.0578, time 6717.34ms, mfu 2.20%
iter 1220: loss 0.0582, time 6716.80ms, mfu 2.21%
iter 1230: loss 0.0555, time 6717.38ms, mfu 2.21%
iter 1240: loss 0.0583, time 6717.00ms, mfu 2.21%
step 1250: train loss 0.0439, val loss 0.9974
iter 1250: loss 0.0528, time 31330.43ms, mfu 2.04%
iter 1260: loss 0.0573, time 6716.31ms, mfu 2.05%
iter 1270: loss 0.0600, time 6716.01ms, mfu 2.07%
iter 1280: loss 0.0542, time 6716.76ms, mfu 2.09%
iter 1290: loss 0.0576, time 6717.33ms, mfu 2.10%
iter 1300: loss 0.0552, time 6717.37ms, mfu 2.11%
iter 1310: loss 0.0579, time 6718.85ms, mfu 2.12%
iter 1320: loss 0.0572, time 6715.42ms, mfu 2.13%
iter 1330: loss 0.0563, time 6717.19ms, mfu 2.14%
iter 1340: loss 0.0556, time 6715.81ms, mfu 2.15%
iter 1350: loss 0.0561, time 6717.36ms, mfu 2.16%
iter 1360: loss 0.0555, time 6716.71ms, mfu 2.17%
iter 1370: loss 0.0529, time 6716.99ms, mfu 2.17%
iter 1380: loss 0.0532, time 6717.12ms, mfu 2.18%
iter 1390: loss 0.0539, time 6718.71ms, mfu 2.18%
iter 1400: loss 0.0536, time 6718.12ms, mfu 2.19%
iter 1410: loss 0.0541, time 6715.92ms, mfu 2.19%
iter 1420: loss 0.0497, time 6717.21ms, mfu 2.19%
iter 1430: loss 0.0533, time 6715.47ms, mfu 2.20%
iter 1440: loss 0.0534, time 6715.95ms, mfu 2.20%
iter 1450: loss 0.0501, time 6716.93ms, mfu 2.20%
iter 1460: loss 0.0534, time 6717.01ms, mfu 2.20%
iter 1470: loss 0.0522, time 6716.63ms, mfu 2.21%
iter 1480: loss 0.0519, time 6718.25ms, mfu 2.21%
iter 1490: loss 0.0539, time 6715.66ms, mfu 2.21%
step 1500: train loss 0.0425, val loss 1.0410
iter 1500: loss 0.0507, time 31326.20ms, mfu 2.04%
iter 1510: loss 0.0527, time 6716.54ms, mfu 2.05%
iter 1520: loss 0.0556, time 6718.02ms, mfu 2.07%
iter 1530: loss 0.0521, time 6717.82ms, mfu 2.09%
iter 1540: loss 0.0523, time 6717.15ms, mfu 2.10%
iter 1550: loss 0.0507, time 6715.86ms, mfu 2.11%
iter 1560: loss 0.0520, time 6716.24ms, mfu 2.12%
iter 1570: loss 0.0518, time 6716.10ms, mfu 2.13%
iter 1580: loss 0.0493, time 6717.31ms, mfu 2.14%
iter 1590: loss 0.0528, time 6716.74ms, mfu 2.15%
iter 1600: loss 0.0489, time 6716.54ms, mfu 2.16%
iter 1610: loss 0.0509, time 6719.47ms, mfu 2.17%
iter 1620: loss 0.0492, time 6716.80ms, mfu 2.17%
iter 1630: loss 0.0531, time 6715.45ms, mfu 2.18%
iter 1640: loss 0.0479, time 6716.58ms, mfu 2.18%
iter 1650: loss 0.0521, time 6718.00ms, mfu 2.19%
iter 1660: loss 0.0517, time 6715.89ms, mfu 2.19%
iter 1670: loss 0.0516, time 6715.82ms, mfu 2.19%
iter 1680: loss 0.0510, time 6716.23ms, mfu 2.20%
iter 1690: loss 0.0500, time 6718.06ms, mfu 2.20%
iter 1700: loss 0.0486, time 6715.86ms, mfu 2.20%
iter 1710: loss 0.0495, time 6717.36ms, mfu 2.20%
iter 1720: loss 0.0516, time 6717.04ms, mfu 2.21%
iter 1730: loss 0.0496, time 6715.82ms, mfu 2.21%
iter 1740: loss 0.0522, time 6716.06ms, mfu 2.21%
step 1750: train loss 0.0414, val loss 1.0700
iter 1750: loss 0.0516, time 31327.16ms, mfu 2.04%
iter 1760: loss 0.0527, time 6716.18ms, mfu 2.06%
iter 1770: loss 0.0461, time 6716.28ms, mfu 2.07%
iter 1780: loss 0.0494, time 6715.83ms, mfu 2.09%
iter 1790: loss 0.0518, time 6718.35ms, mfu 2.10%
iter 1800: loss 0.0481, time 6716.25ms, mfu 2.11%
iter 1810: loss 0.0500, time 6716.11ms, mfu 2.12%
iter 1820: loss 0.0487, time 6716.15ms, mfu 2.13%
iter 1830: loss 0.0496, time 6716.65ms, mfu 2.14%
iter 1840: loss 0.0497, time 6716.16ms, mfu 2.15%
iter 1850: loss 0.0472, time 6717.61ms, mfu 2.16%
iter 1860: loss 0.0471, time 6715.04ms, mfu 2.17%
iter 1870: loss 0.0492, time 6716.23ms, mfu 2.17%
iter 1880: loss 0.0488, time 6715.84ms, mfu 2.18%
iter 1890: loss 0.0485, time 6716.40ms, mfu 2.18%
iter 1900: loss 0.0488, time 6716.40ms, mfu 2.19%
iter 1910: loss 0.0476, time 6719.26ms, mfu 2.19%
iter 1920: loss 0.0498, time 6717.46ms, mfu 2.19%
iter 1930: loss 0.0491, time 6716.44ms, mfu 2.20%
iter 1940: loss 0.0498, time 6715.95ms, mfu 2.20%
iter 1950: loss 0.0476, time 6715.99ms, mfu 2.20%
iter 1960: loss 0.0494, time 6715.42ms, mfu 2.20%
iter 1970: loss 0.0477, time 6717.57ms, mfu 2.21%
iter 1980: loss 0.0478, time 6716.29ms, mfu 2.21%
iter 1990: loss 0.0472, time 6718.78ms, mfu 2.21%
step 2000: train loss 0.0406, val loss 1.1150
iter 2000: loss 0.0485, time 31325.90ms, mfu 2.04%
iter 2010: loss 0.0515, time 6717.05ms, mfu 2.05%
iter 2020: loss 0.0488, time 6715.49ms, mfu 2.07%
iter 2030: loss 0.0469, time 6716.43ms, mfu 2.09%
iter 2040: loss 0.0461, time 6718.18ms, mfu 2.10%
iter 2050: loss 0.0499, time 6716.27ms, mfu 2.11%
iter 2060: loss 0.0475, time 6716.79ms, mfu 2.12%
iter 2070: loss 0.0454, time 6716.01ms, mfu 2.13%
iter 2080: loss 0.0477, time 6715.74ms, mfu 2.14%
iter 2090: loss 0.0459, time 6717.06ms, mfu 2.15%
iter 2100: loss 0.0467, time 6712.36ms, mfu 2.16%
iter 2110: loss 0.0463, time 6715.53ms, mfu 2.17%
iter 2120: loss 0.0472, time 6716.38ms, mfu 2.17%
iter 2130: loss 0.0452, time 6717.59ms, mfu 2.18%
iter 2140: loss 0.0463, time 6717.13ms, mfu 2.18%
iter 2150: loss 0.0457, time 6726.35ms, mfu 2.19%
iter 2160: loss 0.0488, time 6716.80ms, mfu 2.19%
iter 2170: loss 0.0461, time 6716.56ms, mfu 2.19%
iter 2180: loss 0.0505, time 6716.32ms, mfu 2.20%
iter 2190: loss 0.0491, time 6716.70ms, mfu 2.20%
iter 2200: loss 0.0461, time 6716.34ms, mfu 2.20%
iter 2210: loss 0.0465, time 6718.96ms, mfu 2.20%
iter 2220: loss 0.0462, time 6716.91ms, mfu 2.21%
iter 2230: loss 0.0470, time 6717.59ms, mfu 2.21%
iter 2240: loss 0.0439, time 6717.60ms, mfu 2.21%
step 2250: train loss 0.0400, val loss 1.1590
iter 2250: loss 0.0453, time 31327.61ms, mfu 2.04%
iter 2260: loss 0.0462, time 6719.33ms, mfu 2.05%
iter 2270: loss 0.0471, time 6717.34ms, mfu 2.07%
iter 2280: loss 0.0471, time 6717.97ms, mfu 2.09%
iter 2290: loss 0.0451, time 6716.08ms, mfu 2.10%
iter 2300: loss 0.0479, time 6716.18ms, mfu 2.11%
iter 2310: loss 0.0462, time 6714.73ms, mfu 2.12%
iter 2320: loss 0.0463, time 6715.33ms, mfu 2.13%
iter 2330: loss 0.0450, time 6717.84ms, mfu 2.14%
iter 2340: loss 0.0483, time 6719.52ms, mfu 2.15%
iter 2350: loss 0.0436, time 6717.46ms, mfu 2.16%
iter 2360: loss 0.0462, time 6707.14ms, mfu 2.17%
iter 2370: loss 0.0471, time 6716.40ms, mfu 2.17%
iter 2380: loss 0.0471, time 6715.92ms, mfu 2.18%
iter 2390: loss 0.0444, time 6715.61ms, mfu 2.18%
iter 2400: loss 0.0455, time 6707.36ms, mfu 2.19%
iter 2410: loss 0.0463, time 6716.48ms, mfu 2.19%
iter 2420: loss 0.0461, time 6716.38ms, mfu 2.19%
iter 2430: loss 0.0457, time 6718.84ms, mfu 2.20%
iter 2440: loss 0.0465, time 6716.62ms, mfu 2.20%
iter 2450: loss 0.0450, time 6718.04ms, mfu 2.20%
iter 2460: loss 0.0468, time 6717.62ms, mfu 2.20%
iter 2470: loss 0.0428, time 6716.95ms, mfu 2.21%
iter 2480: loss 0.0441, time 6717.15ms, mfu 2.21%
iter 2490: loss 0.0464, time 6716.79ms, mfu 2.21%
step 2500: train loss 0.0397, val loss 1.1793
iter 2500: loss 0.0460, time 31329.48ms, mfu 2.04%
iter 2510: loss 0.0439, time 6716.52ms, mfu 2.06%
iter 2520: loss 0.0442, time 6717.12ms, mfu 2.07%
iter 2530: loss 0.0455, time 6715.40ms, mfu 2.09%
iter 2540: loss 0.0450, time 6717.19ms, mfu 2.10%
iter 2550: loss 0.0439, time 6716.68ms, mfu 2.11%
iter 2560: loss 0.0468, time 6718.72ms, mfu 2.12%
iter 2570: loss 0.0430, time 6716.86ms, mfu 2.13%
iter 2580: loss 0.0450, time 6716.85ms, mfu 2.14%
iter 2590: loss 0.0453, time 6715.91ms, mfu 2.15%
iter 2600: loss 0.0437, time 6715.90ms, mfu 2.16%
iter 2610: loss 0.0449, time 6715.38ms, mfu 2.17%
iter 2620: loss 0.0449, time 6717.01ms, mfu 2.17%
iter 2630: loss 0.0433, time 6717.01ms, mfu 2.18%
iter 2640: loss 0.0442, time 6719.55ms, mfu 2.18%
iter 2650: loss 0.0437, time 6716.99ms, mfu 2.19%
iter 2660: loss 0.0437, time 6717.17ms, mfu 2.19%
iter 2670: loss 0.0459, time 6716.50ms, mfu 2.19%
iter 2680: loss 0.0425, time 6718.03ms, mfu 2.20%
iter 2690: loss 0.0436, time 6717.76ms, mfu 2.20%
iter 2700: loss 0.0441, time 6718.53ms, mfu 2.20%
iter 2710: loss 0.0418, time 6717.55ms, mfu 2.20%
iter 2720: loss 0.0440, time 6716.01ms, mfu 2.21%
iter 2730: loss 0.0456, time 6719.21ms, mfu 2.21%
iter 2740: loss 0.0448, time 6716.81ms, mfu 2.21%
step 2750: train loss 0.0391, val loss 1.2175
iter 2750: loss 0.0448, time 31325.10ms, mfu 2.04%
iter 2760: loss 0.0438, time 6715.00ms, mfu 2.05%
iter 2770: loss 0.0426, time 6705.55ms, mfu 2.07%
iter 2780: loss 0.0420, time 6717.54ms, mfu 2.09%
iter 2790: loss 0.0461, time 6714.89ms, mfu 2.10%
iter 2800: loss 0.0454, time 6716.58ms, mfu 2.11%
iter 2810: loss 0.0444, time 6716.52ms, mfu 2.12%
iter 2820: loss 0.0443, time 6714.47ms, mfu 2.13%
iter 2830: loss 0.0431, time 6716.79ms, mfu 2.14%
iter 2840: loss 0.0448, time 6719.07ms, mfu 2.15%
iter 2850: loss 0.0425, time 6717.76ms, mfu 2.16%
iter 2860: loss 0.0443, time 6719.27ms, mfu 2.17%
iter 2870: loss 0.0425, time 6716.77ms, mfu 2.17%
iter 2880: loss 0.0449, time 6716.05ms, mfu 2.18%
iter 2890: loss 0.0449, time 6717.61ms, mfu 2.18%
iter 2900: loss 0.0446, time 6715.99ms, mfu 2.19%
iter 2910: loss 0.0441, time 6716.73ms, mfu 2.19%
iter 2920: loss 0.0436, time 6716.05ms, mfu 2.19%
iter 2930: loss 0.0442, time 6717.56ms, mfu 2.20%
iter 2940: loss 0.0439, time 6720.37ms, mfu 2.20%
iter 2950: loss 0.0428, time 6716.28ms, mfu 2.20%
iter 2960: loss 0.0430, time 6717.48ms, mfu 2.20%
iter 2970: loss 0.0445, time 6717.11ms, mfu 2.21%
iter 2980: loss 0.0406, time 6715.58ms, mfu 2.21%
iter 2990: loss 0.0425, time 6716.23ms, mfu 2.21%
step 3000: train loss 0.0388, val loss 1.2305
iter 3000: loss 0.0436, time 31323.72ms, mfu 2.04%
iter 3010: loss 0.0429, time 6716.28ms, mfu 2.05%
iter 3020: loss 0.0437, time 6717.32ms, mfu 2.07%
iter 3030: loss 0.0424, time 6715.36ms, mfu 2.09%
iter 3040: loss 0.0415, time 6717.15ms, mfu 2.10%
iter 3050: loss 0.0442, time 6717.81ms, mfu 2.11%
iter 3060: loss 0.0435, time 6716.42ms, mfu 2.12%
iter 3070: loss 0.0453, time 6716.93ms, mfu 2.13%
iter 3080: loss 0.0441, time 6717.83ms, mfu 2.14%
iter 3090: loss 0.0408, time 6709.75ms, mfu 2.15%
iter 3100: loss 0.0437, time 6716.89ms, mfu 2.16%
iter 3110: loss 0.0437, time 6715.42ms, mfu 2.17%
iter 3120: loss 0.0408, time 6716.50ms, mfu 2.17%
iter 3130: loss 0.0429, time 6716.86ms, mfu 2.18%
iter 3140: loss 0.0417, time 6716.37ms, mfu 2.18%
iter 3150: loss 0.0418, time 6717.13ms, mfu 2.19%
iter 3160: loss 0.0435, time 6721.01ms, mfu 2.19%
iter 3170: loss 0.0407, time 6715.76ms, mfu 2.19%
iter 3180: loss 0.0410, time 6715.73ms, mfu 2.20%
iter 3190: loss 0.0418, time 6723.90ms, mfu 2.20%
iter 3200: loss 0.0445, time 6720.42ms, mfu 2.20%
iter 3210: loss 0.0424, time 6718.15ms, mfu 2.20%
iter 3220: loss 0.0433, time 6717.74ms, mfu 2.21%
iter 3230: loss 0.0438, time 6717.29ms, mfu 2.21%
iter 3240: loss 0.0410, time 6719.02ms, mfu 2.21%
step 3250: train loss 0.0384, val loss 1.2396
iter 3250: loss 0.0429, time 31325.70ms, mfu 2.04%
iter 3260: loss 0.0426, time 6716.12ms, mfu 2.05%
iter 3270: loss 0.0416, time 6716.48ms, mfu 2.07%
iter 3280: loss 0.0431, time 6717.69ms, mfu 2.09%
iter 3290: loss 0.0413, time 6719.90ms, mfu 2.10%
iter 3300: loss 0.0427, time 6717.43ms, mfu 2.11%
iter 3310: loss 0.0430, time 6717.71ms, mfu 2.12%
iter 3320: loss 0.0406, time 6717.08ms, mfu 2.13%
iter 3330: loss 0.0422, time 6716.13ms, mfu 2.14%
iter 3340: loss 0.0417, time 6716.19ms, mfu 2.15%
iter 3350: loss 0.0422, time 6716.06ms, mfu 2.16%
iter 3360: loss 0.0425, time 6715.91ms, mfu 2.17%
iter 3370: loss 0.0411, time 6716.64ms, mfu 2.17%
iter 3380: loss 0.0414, time 6717.83ms, mfu 2.18%
iter 3390: loss 0.0430, time 6716.47ms, mfu 2.18%
iter 3400: loss 0.0407, time 6716.53ms, mfu 2.19%
iter 3410: loss 0.0416, time 6715.52ms, mfu 2.19%
iter 3420: loss 0.0422, time 6716.32ms, mfu 2.19%
iter 3430: loss 0.0412, time 6715.91ms, mfu 2.20%
iter 3440: loss 0.0414, time 6716.96ms, mfu 2.20%
iter 3450: loss 0.0425, time 6715.43ms, mfu 2.20%
iter 3460: loss 0.0415, time 6718.46ms, mfu 2.20%
iter 3470: loss 0.0413, time 6714.99ms, mfu 2.21%
iter 3480: loss 0.0412, time 6715.55ms, mfu 2.21%
iter 3490: loss 0.0424, time 6715.80ms, mfu 2.21%
step 3500: train loss 0.0381, val loss 1.2625
iter 3500: loss 0.0406, time 31327.11ms, mfu 2.04%
iter 3510: loss 0.0417, time 6713.74ms, mfu 2.06%
iter 3520: loss 0.0417, time 6713.91ms, mfu 2.07%
iter 3530: loss 0.0407, time 6716.77ms, mfu 2.09%
iter 3540: loss 0.0421, time 6715.41ms, mfu 2.10%
iter 3550: loss 0.0404, time 6717.16ms, mfu 2.11%
iter 3560: loss 0.0410, time 6715.85ms, mfu 2.12%
iter 3570: loss 0.0400, time 6715.95ms, mfu 2.13%
iter 3580: loss 0.0424, time 6716.71ms, mfu 2.14%
iter 3590: loss 0.0415, time 6718.28ms, mfu 2.15%
iter 3600: loss 0.0423, time 6716.69ms, mfu 2.16%
iter 3610: loss 0.0430, time 6715.91ms, mfu 2.17%
iter 3620: loss 0.0421, time 6717.22ms, mfu 2.17%
iter 3630: loss 0.0417, time 6715.18ms, mfu 2.18%
iter 3640: loss 0.0427, time 6715.76ms, mfu 2.18%
iter 3650: loss 0.0409, time 6716.10ms, mfu 2.19%
iter 3660: loss 0.0402, time 6715.76ms, mfu 2.19%
iter 3670: loss 0.0405, time 6716.05ms, mfu 2.19%
iter 3680: loss 0.0422, time 6717.74ms, mfu 2.20%
iter 3690: loss 0.0410, time 6710.30ms, mfu 2.20%
iter 3700: loss 0.0410, time 6716.64ms, mfu 2.20%
iter 3710: loss 0.0416, time 6716.04ms, mfu 2.20%
iter 3720: loss 0.0425, time 6715.61ms, mfu 2.21%
iter 3730: loss 0.0407, time 6715.08ms, mfu 2.21%
iter 3740: loss 0.0414, time 6716.76ms, mfu 2.21%
step 3750: train loss 0.0378, val loss 1.3078
iter 3750: loss 0.0397, time 31328.20ms, mfu 2.04%
iter 3760: loss 0.0421, time 6716.12ms, mfu 2.06%
iter 3770: loss 0.0416, time 6716.22ms, mfu 2.07%
iter 3780: loss 0.0405, time 6715.12ms, mfu 2.09%
iter 3790: loss 0.0412, time 6718.15ms, mfu 2.10%
iter 3800: loss 0.0407, time 6717.14ms, mfu 2.11%
iter 3810: loss 0.0419, time 6719.08ms, mfu 2.12%
iter 3820: loss 0.0404, time 6716.10ms, mfu 2.13%
iter 3830: loss 0.0411, time 6715.74ms, mfu 2.14%
iter 3840: loss 0.0399, time 6716.03ms, mfu 2.15%
iter 3850: loss 0.0420, time 6717.55ms, mfu 2.16%
iter 3860: loss 0.0414, time 6716.87ms, mfu 2.17%
iter 3870: loss 0.0416, time 6715.63ms, mfu 2.17%
iter 3880: loss 0.0412, time 6716.98ms, mfu 2.18%
iter 3890: loss 0.0417, time 6717.61ms, mfu 2.18%
iter 3900: loss 0.0393, time 6717.54ms, mfu 2.19%
iter 3910: loss 0.0403, time 6717.34ms, mfu 2.19%
iter 3920: loss 0.0420, time 6715.01ms, mfu 2.19%
iter 3930: loss 0.0399, time 6717.68ms, mfu 2.20%
iter 3940: loss 0.0412, time 6717.80ms, mfu 2.20%
iter 3950: loss 0.0425, time 6717.02ms, mfu 2.20%
iter 3960: loss 0.0397, time 6716.56ms, mfu 2.20%
iter 3970: loss 0.0402, time 6717.14ms, mfu 2.21%
iter 3980: loss 0.0398, time 6718.70ms, mfu 2.21%
iter 3990: loss 0.0410, time 6715.63ms, mfu 2.21%
step 4000: train loss 0.0376, val loss 1.2991
iter 4000: loss 0.0396, time 31326.38ms, mfu 2.04%
iter 4010: loss 0.0415, time 6716.06ms, mfu 2.05%
iter 4020: loss 0.0409, time 6715.92ms, mfu 2.07%
iter 4030: loss 0.0405, time 6718.28ms, mfu 2.09%
iter 4040: loss 0.0408, time 6716.20ms, mfu 2.10%
iter 4050: loss 0.0397, time 6715.60ms, mfu 2.11%
iter 4060: loss 0.0411, time 6716.59ms, mfu 2.12%
iter 4070: loss 0.0414, time 6716.08ms, mfu 2.13%
iter 4080: loss 0.0397, time 6716.33ms, mfu 2.14%
iter 4090: loss 0.0399, time 6716.76ms, mfu 2.15%
iter 4100: loss 0.0411, time 6715.52ms, mfu 2.16%
iter 4110: loss 0.0404, time 6718.19ms, mfu 2.17%
iter 4120: loss 0.0379, time 6716.51ms, mfu 2.17%
iter 4130: loss 0.0398, time 6717.30ms, mfu 2.18%
iter 4140: loss 0.0409, time 6716.31ms, mfu 2.18%
iter 4150: loss 0.0401, time 6715.51ms, mfu 2.19%
iter 4160: loss 0.0409, time 6715.75ms, mfu 2.19%
iter 4170: loss 0.0396, time 6715.59ms, mfu 2.19%
iter 4180: loss 0.0393, time 6717.50ms, mfu 2.20%
iter 4190: loss 0.0413, time 6718.13ms, mfu 2.20%
iter 4200: loss 0.0400, time 6717.46ms, mfu 2.20%
iter 4210: loss 0.0416, time 6716.15ms, mfu 2.20%
iter 4220: loss 0.0411, time 6716.66ms, mfu 2.21%
iter 4230: loss 0.0401, time 6716.02ms, mfu 2.21%
iter 4240: loss 0.0406, time 6716.23ms, mfu 2.21%
step 4250: train loss 0.0374, val loss 1.3105
iter 4250: loss 0.0403, time 31326.34ms, mfu 2.04%
iter 4260: loss 0.0412, time 6715.89ms, mfu 2.06%
iter 4270: loss 0.0404, time 6715.74ms, mfu 2.07%
iter 4280: loss 0.0396, time 6714.95ms, mfu 2.09%
iter 4290: loss 0.0407, time 6716.07ms, mfu 2.10%
iter 4300: loss 0.0405, time 6715.42ms, mfu 2.11%
iter 4310: loss 0.0406, time 6716.68ms, mfu 2.12%
iter 4320: loss 0.0401, time 6716.55ms, mfu 2.13%
iter 4330: loss 0.0400, time 6718.88ms, mfu 2.14%
iter 4340: loss 0.0403, time 6715.22ms, mfu 2.15%
iter 4350: loss 0.0414, time 6716.45ms, mfu 2.16%
iter 4360: loss 0.0406, time 6716.07ms, mfu 2.17%
iter 4370: loss 0.0394, time 6715.90ms, mfu 2.17%
iter 4380: loss 0.0404, time 6715.41ms, mfu 2.18%
iter 4390: loss 0.0409, time 6715.84ms, mfu 2.18%
iter 4400: loss 0.0405, time 6716.06ms, mfu 2.19%
iter 4410: loss 0.0417, time 6718.34ms, mfu 2.19%
iter 4420: loss 0.0388, time 6716.51ms, mfu 2.19%
iter 4430: loss 0.0417, time 6716.87ms, mfu 2.20%
iter 4440: loss 0.0407, time 6717.53ms, mfu 2.20%
iter 4450: loss 0.0397, time 6717.68ms, mfu 2.20%
iter 4460: loss 0.0399, time 6715.75ms, mfu 2.20%
iter 4470: loss 0.0400, time 6716.21ms, mfu 2.21%
iter 4480: loss 0.0405, time 6716.07ms, mfu 2.21%
iter 4490: loss 0.0399, time 6720.37ms, mfu 2.21%
step 4500: train loss 0.0374, val loss 1.3399
iter 4500: loss 0.0408, time 31321.43ms, mfu 2.04%
iter 4510: loss 0.0394, time 6714.57ms, mfu 2.06%
iter 4520: loss 0.0396, time 6716.87ms, mfu 2.07%
iter 4530: loss 0.0381, time 6717.75ms, mfu 2.09%
iter 4540: loss 0.0407, time 6717.91ms, mfu 2.10%
iter 4550: loss 0.0399, time 6715.10ms, mfu 2.11%
iter 4560: loss 0.0408, time 6714.90ms, mfu 2.12%
iter 4570: loss 0.0395, time 6715.94ms, mfu 2.13%
iter 4580: loss 0.0404, time 6715.79ms, mfu 2.14%
iter 4590: loss 0.0386, time 6715.99ms, mfu 2.15%
iter 4600: loss 0.0399, time 6716.84ms, mfu 2.16%
iter 4610: loss 0.0406, time 6716.01ms, mfu 2.17%
iter 4620: loss 0.0400, time 6717.30ms, mfu 2.17%
iter 4630: loss 0.0389, time 6721.01ms, mfu 2.18%
iter 4640: loss 0.0391, time 6714.90ms, mfu 2.18%
iter 4650: loss 0.0407, time 6716.53ms, mfu 2.19%
iter 4660: loss 0.0408, time 6714.60ms, mfu 2.19%
iter 4670: loss 0.0396, time 6717.04ms, mfu 2.19%
iter 4680: loss 0.0402, time 6715.22ms, mfu 2.20%
iter 4690: loss 0.0404, time 6716.74ms, mfu 2.20%
iter 4700: loss 0.0399, time 6716.87ms, mfu 2.20%
iter 4710: loss 0.0397, time 6718.33ms, mfu 2.20%
iter 4720: loss 0.0395, time 6716.57ms, mfu 2.21%
iter 4730: loss 0.0403, time 6716.80ms, mfu 2.21%
iter 4740: loss 0.0406, time 6716.92ms, mfu 2.21%
step 4750: train loss 0.0372, val loss 1.3419
iter 4750: loss 0.0406, time 31327.88ms, mfu 2.04%
iter 4760: loss 0.0409, time 6717.48ms, mfu 2.05%
iter 4770: loss 0.0404, time 6717.24ms, mfu 2.07%
iter 4780: loss 0.0388, time 6716.84ms, mfu 2.09%
iter 4790: loss 0.0395, time 6716.81ms, mfu 2.10%
iter 4800: loss 0.0396, time 6716.76ms, mfu 2.11%
iter 4810: loss 0.0394, time 6719.02ms, mfu 2.12%
iter 4820: loss 0.0405, time 6716.57ms, mfu 2.13%
iter 4830: loss 0.0389, time 6715.20ms, mfu 2.14%
iter 4840: loss 0.0379, time 6719.37ms, mfu 2.15%
iter 4850: loss 0.0396, time 6715.92ms, mfu 2.16%
iter 4860: loss 0.0399, time 6717.95ms, mfu 2.17%
iter 4870: loss 0.0403, time 6717.23ms, mfu 2.17%
iter 4880: loss 0.0382, time 6716.93ms, mfu 2.18%
iter 4890: loss 0.0383, time 6717.51ms, mfu 2.18%
iter 4900: loss 0.0398, time 6715.96ms, mfu 2.19%
iter 4910: loss 0.0378, time 6716.51ms, mfu 2.19%
iter 4920: loss 0.0388, time 6715.62ms, mfu 2.19%
iter 4930: loss 0.0408, time 6718.02ms, mfu 2.20%
iter 4940: loss 0.0395, time 6715.92ms, mfu 2.20%
iter 4950: loss 0.0393, time 6716.81ms, mfu 2.20%
iter 4960: loss 0.0406, time 6715.71ms, mfu 2.20%
iter 4970: loss 0.0401, time 6717.12ms, mfu 2.21%
iter 4980: loss 0.0401, time 6717.45ms, mfu 2.21%
iter 4990: loss 0.0398, time 6716.72ms, mfu 2.21%
step 5000: train loss 0.0373, val loss 1.3391
iter 5000: loss 0.0402, time 31346.27ms, mfu 2.04% 


# - python sample.py --out_dir=out-mitos
Overriding: out_dir = out-mitos
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
WARNING: using slow attention. Flash Attention atm needs PyTorch nightly and dropout=0.0
number of parameters: 10.68M
Loading meta from data/mitos/meta.pkl...



Ποια είναι τα βήματα της διαδικασίας ανάκλησης πράξης παραχώρησης χρήσης ακινήτων;
1. Παραλαβή αίτησης από τον αιτούντα και έλεγχο των με το προϋποθέσεων.
2. Έκδοση του προεδρικού Διατάγματος, δημοσίευση σε ΦΕΚ και γνωστοποίηση δημοσίευσης.
3. Ταυτοποίηση του χρήστη με τον δικαιολογητικό έλεγχο των καταστατών κωδικών Taxisnet.
4. Εξαγωγή της δήλωσης στις ψηφιακές υπηρεσίες του ΥΠΑΑΤ.
5. Προώθηση του εντύπου - πιστοποιητικού ελεύθερης διακίνησης ζωοτροφής.
6. Έκδοση πιστοποιητικού ελεύθερης δ
---------------

ήματα της διαδικασίας παροχής συμβουλευτικών υπηρεσιών προς επιχειρήσεις (ΔΥΠΑ) ;
1. Εκκίνηση της διαδικασίας: Ο εργοδότης επιλέγει τον τρόπο με τον οποίο επιθυμεί να κλείσει ραντεβού με εργασιακό σύμβουλο εργοδότη μέσω της επικροών.
2. Πρωτοκόλληση της αίτησης και πρωτοκόλληση (με ψηφιακό τρόπο)
3. Αποστολή της αρμόδιας της αρμόδιας ΔΑΠ
4. Ολοκλήρωση της αίτησης
6. Γνωμοδότηση της Κ.Ε.Ο.Ε.Φ.
7. Απόφαση από τη Διεύθυνση Εκπαίδευσης και Ανάπτυξης Ανθρώπινων Πόρων του Αρχηγείου Ελληνικής Αστυνομί
---------------



Ποια είναι τα βήματα της διαδικασίας απονομής πολεμικής σύνταξης;
Τα βήματα περιλαμβάνουν την παραλαβή και πρωτοκόλληση αίτησης, τον έλεγχο πληρότητας δικαιολογητικών, τη σύνταξη πρότασης και απορρίπτεται και ο ενδιαφερόμενος ενημερώνεται για την προθεσμία των δέκα (10) ημέρωσης παρέλθει άπρακτη ή αν τα συμπληρωματικά δικαιολογητικά είναι ανεπαρκή.


Ποια είναι τα βήματα της διαδικασίας παρακολούθησης εσόδων από μερίσματα μετοχικών τίτλων κυριότητας Ελληνικού Δημοσίου;

1. Λήψη απόφασης της
---------------


Τι αφορά η διαδικασία ανάλυσης καταβολής ασφαλιστικών εισφορών ΕΛΓΑ;
Η διαδικασία αφορά την έκδοση ανάλυσης καταβολής ασφαλιστικών εισφορών του Οργανισμού Ελληνικών Γεωργικών Ασφαλίσεων (ΕΛΓΑ).


Ποιες είναι οι προϋποθέσεις για τη διαδικασία αναβολής ασφαλιστικών εισφορών εισφορών ΕΛΓΑ;
1. Ασφαλιστικές: Να είναι ο χρήστης ασφαλισμένος του Οργανισμού Ελληνικών Γεωργικών Ασφαλίσεων (ΕΛΓΑ).
2. Οικονομικές: Να έχει καταβληθεί αποζημίωση ΕΛΓΑ / ΚΟΕ στον χρήστη.
3. Κατοχής κωδικών για είσοδο σε λογ
---------------


Ποια είναι τα βήματα της διαδικασίας Δήλωση Ε9 / ΕΝΦΙΑΗ;
1. Είσοδος στον δικτυακό τόπο της Ανεξάρτητης Αρχής Δημοσίων Εσόδων.
2. Επιλογή "Πολίτες" -> "Ακίνητα" -> "Δήλωση Ε9/ΕΝΦΙΑ".
3. Είσοδος στην εφαρμογή Δήλωση Ε9/ΕΝΦΙΑ.
4. Επιλογή Έτους δήλωσης Ε9.
5. Δημιουργία δήλωσης Ε9.
6. Δημοσίευση Ε9.
7. Δημοσίευση Δελτίου Τύπου δήλωσης Ε9.
9. Ολοκλήρωση διαδικασίας.
10. Υποβολή δήλωσης Ε9 εκ μεταφοράς στο επόμενο έτος.
11. Υποβολή δήλωσης Ε9.
10. Υποβολή δήλωσης εκ μεταφοράς στ
---------------



Ποια είναι τα βήματα της διαδικασίας έκδοσης βεβαίωσης αυτασφάλισης;
Τα βήματα περιλαμβάνουν τη διενέργεια επίσημων ελέγχων, τη διαπίστωση μη συμμόρφωσης, την έκθεση ελέγχου, τη διαβίβαση επιβολή διοικητικών κυρώσεων, την κοινοποίηση αποφάσεων στοιχείων και την ελληνική ιθαγένεια ή καταδικό πληροφορίες επιτροπών.


Τι αφορά η διαδικασία της Ετήσιας Θεώρησης Καταγραφής Επιβαινόντων Πλοίων;
Η διαδικασία αφορά στην ετήσια θεώρηση και επικαιροποίηση της Ετήσιας Ετήσιας Θεώρησης Βεβαίωσης ΗΣΚΘΕΕΑ
---------------

Τι αφορά η διαδικασία της Χορήγησης Αριθμού Καταχώρισης σε Αλιευτικό Σκάφος;
Η διαδικασία αφορά στην καταχώριση σε μητρώο των αλιευτικών σκαφών που δραστηριοποιούνται στην πρωτογενή παραγωγή και τηρούν το καταστατικό πρακτικό ταχυδρομείο (e-mail).


Ποιες είναι οι προϋποθέσεις για τη διαδικασία αυτή;
Προϋπόθεση είναι η κατοχή προσωπικών κωδικών πρόσβασης στο TAXISnet και web banking, καθώς και η πιστοποίηση ενός αριθμού κινητού τηλεφώνου.


Ποια είναι τα βήματα της διαδικασίας του Έλεγχου Σ
---------------

gov.gr
4. Επιλογή έκδοσης βεβαίωσης και εκκαθάριση για την εκπαίδευση της Επιθεωρητών Ασφάλειας Πλοίων Αναψυχής από το Μητρώο Ν.Ε.Π.ΑΗ;
Η διαδικασία αφορά στη διερεύνηση των ιατρικών συνεταιρισμών και τη διαθεσιμών ποσουδαστικών στη διαδικασία επιλογής εκπαιδευτικού προσωπικού από τις Σχολές Λιμενικού Σώματος - Ελληνικής Ακτοφυλακής.


Ποιες είναι οι συνθήκες της διαδικασίας των περιοδικών ελέγχων των οργάνων μέτρησης;
Οι συνθήκες περιλαμβάνουν την αποστολή εγκυκλίου από την αρμόδια θεσμική
---------------



Ποιες είναι οι προϋποθέσεις για τη διαδικασία αυτή;
1. Κατοχής κωδικών για είσοδο σε λογισμικό: Για την ψηφιακή υποβολή της αίτησης, απαιτείται η κατοχή προσωπικών κωδικών taxisnet.
2. Πρωτοκόλληση αίτησης έγγραφης.
3. Απόρριψη της αίτησης από τον επίσημο κτηνίατρο.
4. Έγκριση της αίτησης έναρξης εκμετάλλευσης από τον επίσημο κτηνίατρο.
5. Καταχώρηση της βεβαίωσης των στοιχείων της εγκεκριμένης αίτησης στο ΟΠΣ-Κ από τον επίσημο κτηνίατρο.
6. Καταχώριση των στοιχείων της εταιρείας πλοία και στ
---------------

Ποιες είναι οι προϋποθέσεις για τη διαδικασία έκδοσης Βεβαίωσης Καταμέτρησης Επιβαινόντων Πλοίων;
Αφορά σε επιβατηγό πλοίο ή ταχύπλοο σκάφος που μεταφέρει περισσότερους από 12 επιβάτες, με συγκεκριμένες εξαιρέσεις.


Ποια είναι τα βήματα της διαδικασίας έκδοσης Βεβαίωσης Κατάθεσης Δικαιολογητικών για Σκαλωσιές, κατασκευής χώρας μέλους της Ε.Ε.;
Τα βήματα περιλαμβάνουν την είσοδο στην Ενιαία Ψηφιακή Πύλη gov.gr, τη δακτυλοσκόπηση της αίτησης, τη δακτυλοσκόπηση του ατόμου με livescanner, τη δακτ
---------------