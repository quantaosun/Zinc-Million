# Zinc-Million
Millions of small molecules will be downloaded from the ZINC database in 3D SDF file format, serving for docking based virtual screening purposes. Most of these molecules could be purchased.

# ZINC-Download

#### Introduction

https://zinc20.docking.org/tranches/home/

ZINC is one of the largest databases for small molecules entities, many of them are commercially available, at least in the west, maybe also available in China.

The filters I have set to reduce the number is as shown in the image, drop-down selection is lead-like.

![image](https://user-images.githubusercontent.com/75652473/149165029-5726b57b-ee6d-4340-9c6b-a5ad72fa3613.png)


select file type as SDF and download format as wget

![image](https://user-images.githubusercontent.com/75652473/149164049-7e0dcd10-f4fa-4198-84e8-029d4dc8e008.png)



Head to your Linux terminal and copy the wget file to a new file called download.sh


```
cat ZINC-downloader-3D-sdf.gz.wget download.sh
```

If you look at the sh file, it is a full crazy list of downloading commands inside, and that is how we get to millions of chemicals.


```
mkdir -pv CA/AARN && wget http://files.docking.org/3D/CA/AARN/CAAARN.xaa.sdf.gz -O CA/AARN/CAAARN.xaa.sdf.gz
mkdir -pv CA/ABRN && wget http://files.docking.org/3D/CA/ABRN/CAABRN.xaa.sdf.gz -O CA/ABRN/CAABRN.xaa.sdf.gz
mkdir -pv CA/BARN && wget http://files.docking.org/3D/CA/BARN/CABARN.xaa.sdf.gz -O CA/BARN/CABARN.xaa.sdf.gz
....
```
Start the download 

```
sh download.sh
```
It now should start the process 


```
CA/AARN/CAAARN.xaa.sdf.gz          21%[============>                                               ] 189.18K  11.2KB/s    etCA/AARN/CAAARN.xaa.sdf.gz          21%[============>                                               ] 190.50K  10.3KB/s    etCA/AARN/CAAARN.xaa.sdf.gz          83%[================================================>           ] 724.96K  12.8KB/s    eta 14s  
```



After finishing downloading, we already have them but spread across multiple folders instead of one, but for the sake of virtual screening, we hope it could be in one folder as one file.

# The method here used to extract the .sdf.gz file is not perfect, since we have to go to each folder called "CA" or "CB" first, then run the code below.

Go to each of the folders, extract all the SDF files

```
for D in ./*; do
    if [ -d "$D" ]; then
        cd "$D"
        gunzip *.sdf.gz
        cd ..
    fi
done
```
Go to each of the folders, copy out all the SDF files

```
for D in ./*; do
    if [ -d "$D" ]; then
        cd "$D"
        cp *sdf /path/you/want/copy
        cd ..
    fi
done
```
Finally, use concatenate to combine all of them

```
cat *.sdf > zinc.sdf
```

# Alternatively, it is also possible to download in Windows PowerShell, this could be useful for people who have no Linux system, but the method is not discussed here.

