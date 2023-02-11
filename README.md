# Zinc-Million
Millions of small molecules will be downloaded from the ZINC database in 3D SDF file format, serving for docking based virtual screening purposes. Most of these molecules could be purchased.

# ZINC-Download

#### Introduction

https://zinc20.docking.org/tranches/home/

ZINC is one of the largest databases for small molecules entities, many of them are commercially available, at least in the west, maybe also available in China.

The filters I have set to reduce the number is as shown in the image, drop-down selection is lead-like.

![image](https://user-images.githubusercontent.com/75652473/149165174-2a61a5e8-295a-4dfc-b417-ecb81e3b6158.png)

select file type as SDF and download format as wget,note the image below showed the wrong selection.

![image](https://user-images.githubusercontent.com/75652473/149164049-7e0dcd10-f4fa-4198-84e8-029d4dc8e008.png)

## The current notebook can work well, but the next code is more simplified. This block is for process the downloaded database.

```
#!/bin/bash

# 进入每个子文件夹
for dir in */; do
  cd "$dir"
  # 进入内部文件夹
  for inner_dir in */; do
    cd "$inner_dir"
    # 解压所有.gz文件
    for file in *.gz; do
      gunzip "$file"
    done
    # 复制所有解压后的文件到上层文件夹
    cp ./* ../../
    cd ../
  done
  cd ../
done

# 合并所有文件
cat ./* > all_unzipped_files.txt
```

