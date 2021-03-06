# OC
Лабораторная работа №1  
Номер группы: 728111  
Номер зачетки: 1800189  
## Что нужно уметь
1. монтировать/размонтировать файловую систему
2. выводить информацию о подмонтированных дисках (чтобы было видно тип файловой системы)
3. создавать файловые системы (форматирование)
4. создавать разделы
5. проверять файловые системы
## В своей виртуальной машине сделать
1. создать виртуальный диск (скриншот доступных дисков в отчет)  
`dd if=/dev/zero of=v.img bs=1M count=1024`  
`fdisk v.img`  
`g`  
`n`  
`w`  
`mkfs.ext4 v.img`  
`sudo losetup -Pf --show v.img`  
2. на этом диске создать 8 разделов (размером N Мбайт, N-последние три цифры в номере зачетки) используя MBR запись (не GPT) (скриншот доступных разделов на диске в отчет)  
`sudo fdisk /dev/loop5`  
`p`  
`n`  
`189M`
3. на одном из разделов создать файловую систему NTFS (размер блока (байт) (256) 1024, 2048, 4096 (65536) самый близкий размер к последней цифре в номере зачетки) (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.ntfs -s 4096 /dev/loop10p5`  
`sudo lsblk -f`  
4. на одном из разделов создать файловую систему FAT32  (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.fat -F32 /dev/loop10p6`  
`sudo lsblk -f`  
5. на одном из разделов создать файловую систему EXT2 (размер блока (байт) 1024, 2048, 4096 самый близкий размер к последней цифре в номере зачетки) (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.ext2 -s 4096 /dev/loop10p7`  
`sudo lsblk -f`  
6. на одном из разделов создать файловую систему EXT3, включить журналирование данных (не только метаданных) (размер блока (байт) 1024, 2048, 4096 самый близкий размер к последней цифре в номере зачетки) (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.ext3 -s 4096 /dev/loop10p8`  
`sudo lsblk -f`  
`sudo tune2fs -O has_journal -o journal_data /dev/loop10p8`  
`sudo tune2fs -l /dev/loop10p8 | grep features`    
7. на одном из разделов создать файловую систему EXT4, включить журналирование данных (не только метаданных) (размер блока (байт) 1024, 2048, 4096 самый близкий размер к последней цифре в номере зачетки) (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.ext4 -s 4096 /dev/loop10p9`  
`sudo lsblk -f`  
`sudo tune2fs -l /dev/loop10p8 | grep features`  
8. на одном из разделов создать файловую систему Btrfs (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.btrfs /dev/loop10p10`  
`sudo lsblk -f`  
9. на одном из разделов создать файловую систему xfs (скриншоты команды форматирования и информации о файловой системе в отчет)  
`sudo mkfs.xfs /dev/loop10p11`  
`sudo lsblk -f`  
10. монтировать все разделы в подкаталоги каталога /mnt/фамилия/название файловой системы (скриншот подмонтированных разделов с колонкой "тип файловой системы" в отчет)  
`sudo mkdir /mnt/khisamov`  
`sudo mkdir /mnt/khisamov/ntfs`  
`sudo mkdir -t ntfs /dev/loop10p5 /mnt/khisamov/ntfs`  
`lsblk -f`  
11. сделать автоматическое монтирование при загрузке, используя UUID дисков (скриншот fstab в отчет)  
`UUID=id /mnt/khisamov/ntfs ntfs defaults 0 0`  
`UUID=id /mnt/khisamov/vfat fat32 defaults 0 0`  
`UUID=id /mnt/khisamov/ext2 ext2 defaults 0 0`  
`UUID=id /mnt/khisamov/ext3 ext3 defaults 0 0`  
`UUID=id /mnt/khisamov/ext4 ext4 defaults 0 0`  
`UUID=id /mnt/khisamov/btrfs btrfs defaults 0 0`  
`UUID=id /mnt/khisamov/xfs xfs defaults 0 0`  
12. на одном из разделов создать файловую систему для SWAP (скриншот разделов на диске в отчет)  
`sudo mkswap /dev/loop10p12`  
`sudo swapon /dev/loop10p12`  
`sudo swapon -s`  
`lsblk`  
13. выполните проверку раздела с файловой системой EXT2  (скриншот результата проверки в отчет)  
`sudo umount /dev/loop10p7`  
`sudo fsck /dev/loop10p7`  
## Что надо изучить
1. диски
2. файловые системы
3. сектор
4. MBR
5. разделы
6. блоки
7. кластеры
8. суперблок
9. процесс загрузки системы
