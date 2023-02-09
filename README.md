# windows_comand

## Git cledentials

git config --global credential.helper manager

git config --global credential.useHttpPath true

## Conda Visual Studio Code

add conda on path

### terminal comand

conda init

conda activate enviroment

## Reconstruir partição de boot do Windows

Pelo Pen Drive boot do Windows verificar as partições, clicar "X" fechar, na tela seguinte: Reparar Computador - Opções Avançadas ou Solução de Problemas - Prompt de Comando, então:

~~~
diskpart
list disk
~~~

Qual o disco de inicialização? chamo de 0 mas deve ser verificado

~~~
select disk 0
lis vol
list partition
~~~

qual a partição EFI? cosiderarei 1 mas deve ser verificado
considerei tamanho da partição 100mB

~~~
select partition 1
delete partition override
create partition efi size=100
format quick fs=fat32
assign letter=p
exit
~~~

copiar os arquivos de boot: qual a unidade da pasta do windows? cosiderarei C mas deve ser verificado

~~~
bcdboot c:\windows /f UEFI /s p:
exit
~~~

https://sayrodigital.com/hardware/reconstrua-particoes-reservadas-pelo-sistema-efi/

Se for dual boot linux, deve-se inicializar o pc com o super-grub2, montar a partição EFI para isso verificar uuid no discs e ajustar o fstab:

~~~
sudo nano /etc/fstab
sudo mount -a
~~~

verificar se a partição EFI foi montada e reinstar o grub:

iniciando com o super grub2

~~~
sudo grub-install --boot-directory=/boot /dev/sdX
~~~

iniciando com o super grub2

~~~
sudo grub-install --boot-directory=/mnt/boot /dev/sdX
~~~






