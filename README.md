# SSD-6D
본 챌린지는 물체의 6D포즈 추정 (SSD-style detector for 3D instance detection and full 6D pose estimation) 하는 태스크입니다.
* SSD-6D: Making RGB-based 3D detection and 6D pose estimation great again
* https://arxiv.org/abs/1711.10006
* 논문 설명 링크
* https://youtu.be/vlEdPjwdg6Q
* DATA SET
* https://bop.felk.cvut.cz/datasets/

## DATA SET 사용법
#### Hinterstoisser DATASET
```bash
export SRC=http://ptak.felk.cvut.cz/6DB/public/bop_datasets
wget $SRC/lm_base.zip         # Base archive with dataset info, camera parameters, etc.
wget $SRC/lm_models.zip       # 3D object models.
wget $SRC/lm_test_all.zip     # All test images ("_bop19" for a subset used in the BOP Challenge 2019/2020).
wget $SRC/lm_train_pbr.zip    # PBR training images (rendered with BlenderProc4BOP).

unzip lm_base.zip             # Contains folder "lm".
unzip lm_models.zip -d lm     # Unpacks to "lm".
unzip lm_test_all.zip -d lm   # Unpacks to "lm".
unzip lm_train_pbr.zip -d lm  # Unpacks to "lm".
```
#### Tejani DATASET
```bash
export SRC=http://ptak.felk.cvut.cz/6DB/public/bop_datasets
wget $SRC/icmi_base.zip       
wget $SRC/icmi_models.zip    
wget $SRC/icmi_train.zip   
wget $SRC//icmi_test_all.zip  

unzip icmi_base.zip   
unzip icmi_models.zip -d icmi   
unzip icmi_train.zip -d icmi  
unzip icmi_test_all.zip -d icmi  
```
데이터셋의 구조는 다음과 같습니다.
```
DATASET_NAME
├─ camera[_TYPE].json
├─ dataset_info.json
├─ test_targets_bop19.json
├─ models[_MODELTYPE][_eval]
│  ├─ models_info.json
│  ├─ obj_OBJ_ID.ply
├─ train|val|test[_TYPE]
│  ├─ SCENE_ID|OBJ_ID
│  │  ├─ scene_camera.json
│  │  ├─ scene_gt.json
│  │  ├─ scene_gt_info.json
│  │  ├─ depth
│  │  ├─ mask
│  │  ├─ mask_visib
│  │  ├─ rgb|gray
```
.json파일을 .yml파일로 변경해.
(json_to_yml.bat 폴더에 넣고 실행하면 자동으로 변경)

## 코드 사용법

기존의 학습된 네트워크를 다음의 링크에서 받으면 됩니다.

* https://drive.google.com/file/d/1xSCv2KLYMWftQzjrdAO1_mmef76otCYt/view?usp=sharing

제가 직접 구현하진 못하여서 기존의 파일에서 DATASET format 변경 및 실행이 가능하도록 수정을 하였습니다.

### Single detecition
```
benchmark.py -d "data set 경로" -n "네트워크 경로" -s "sequence 번호" -i "in-planes"
```

#### Hinterstoisser DATASET 의 4번 으로 수행 하시면 됩니다.
csv 파일로 mean_rot_error 1 저장하셔서 제출하시면 됩니다.
