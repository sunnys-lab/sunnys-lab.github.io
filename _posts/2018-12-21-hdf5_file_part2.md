---
title: HDF 포맷 Part 2: HDF5를 이용한 데이터 학습
categories:
  - keras
tags:
  - hdf5
  - h5py
  - keras
---

### HDF5를 이용한 데이터 학습
- HDF5 포맷은 대용량 데이터를 처리하기 위한 파일 형식
- 많은 양의 데이터를 안정적으로 저장가능
- Random Access 및 빠른 검색 등을 지원
- Python에서 HDF5를 다루기 위해서는 h5py 라는 모듈 설치가 필요

>## 01. h5py를 이용해 데이터셋 만드는 방법 

    import numpy as np
    import h5py
 
    with h5py.File(filename, 'w') as f:
        f.create_dataset('image', (1000, 32, 32, 3), dtype='float32')    # 1000개의 32x32 RGB 이미지를 담는 데이터 공간을 생성
        f.create_dataset('label', (1000,), dtype='float32')              # 1000개의 float을 담는 데이터 공간을 생성
        image_set = f['image']    # 실 데이터 공간에 접근할 변수를 할당한다. 
        label_set = f['label']


위 샘플은 filename 경로에 .hdf5 파일을 생성하고, 그 파일에 자료를 저장할 데이터셋을 생성하는 코드이다. 
filename 은  "path/data/hdf5file/name.hdf5"  과 같은 형식으로 저장된다 
데이터셋은 key와 value 형태로 HDF5 파일 내부에 세부 경로를 만들고 그 경로에 주어진 데이터가 들어가는 형식
즉, 경로를 key로, 데이터를 value로 가지는 대용량의 딕셔너리로 간주하여도 됨다. 


>## 02. 데이터셋 생성한 뒤, 인덱스에 값을 대입하는 방법 

    labels = label_set[:]    # 이미지 데이터 전체를 반환하지만, 메모리에 올리지는 않는다. 값에 접근할 때 메모리에 올린다. 
    array = label_set[:50]   # 데이터셋을 numpy array 와 비슷한 형태로 불러올 수 있다. 역시 이 명령으로 메모리에 올라가지는 않는다. 
    label_set[0] = 3.0       # dataset에 값을 대입할 수 있다. 
    label_set[10:20] = np.arange(10.)       # 배열을 직접 대입할 수도 있다.  


위와 같이 HDF5 파일의 자료는 원하는 양 만큼 잘라낸 후 numpy array 와 유사하게 사용할 수 있다. 
이 때, HDF5 파일은 실제 데이터 값에 접근하기 전까지는 메모리로 올라오지 않고, 데이터에 접근할 때도 메모리 제한 내에서 load와 close 를 반복하기 때문에 데이터 양과 무관하게 마음껏 사용할 수 있게 된다. 

>## 03.keras 에서 HDF5 파일을 학습 데이터로 사용하는 법  

keras.utils.io_utils.HDF5Matrix  를 이용하면 Keras에서 HDF5 포맷을 학습데이터로 사용할 수 있다.
이 클래스를 이용하면 Keras 내에서 자동으로 처리가 되기 때문에 학습용 데이터를 넣어줄 때 별다른 처리 없이 넣어줘도 된다. 

    from keras.utils.io_utils import HDF5Matrix
 
    n_epoch = 1000
    batch_size = 32
    split_pos = 800
 
    x_data = HDF5Matrix(filename, 'image')    # 위에서 생성한 HDF5 파일의 image 경로의 데이터를 가져오게 된다. 
    x_train = HDF5Matrix(filename, 'image', end=split_pos)    # HDF5 파일의 데이터 중 일부만 가져오는 것도 가능하다. 
    x_test = HDF5Matrix(filename, 'image', start=split_pos)
    y_train = HDF5Matrix(filename, 'label', end=split_pos)
    y_test = HDF5Matrix(filename, 'label', start=split_pos)
    
    # model이 이미 .compile() 이 된 모델이라고 가정하면 
    model.fit (x_train, y_train, epochs=n_epoch, batch_size=batch_size, validation_data=(x_test, y_test)) 
    
위와 같이 numpy array 를 쓰듯이 사용하면 된다.
HDF5포맷을 파일로 저장하고, keras의 HDF5Matrix를 이용하면 복잡한 처리 없이 대용량 데이터를 쉽게 학습할 수 있다.

참고로 위의 내용들은 아래의 레퍼런스들을 참고로 만든 내용입니다.
reference 1 = http://nuxlear.tistory.com/4?category=280392
reference 2 = https://www.christopherlovell.co.uk/blog/2016/04/27/h5py-intro.html


