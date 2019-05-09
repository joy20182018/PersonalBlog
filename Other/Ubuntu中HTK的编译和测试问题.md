# 以下为官方的安装指导
Installing HTK on Linux or Unix
Please note that from version 3.3, HTK uses Autoconf to facilitate the installation process.

If you have a particular reason to install an older version of HTK (3.2.1 or earlier), please refer to this document.

Prerequisites
A C compiler. All Linux distributions suitable for developers will have a copy of gcc installed, but you can use other compilers such as the Intel compiler icc. If in doubt, please ask your system administrator.
For testing, you will require a Perl Interpreter. Most modern Linux/Unix systems include one by default.
You will need either tar and gzip (if you download the sources via ftp or http) or CVS (if you download from our CVS server). These tools are usually included by default with Linux distributions. Many other modern UNIX variants also supply them, as optional packages if not by default.
If compiling on Apple Macintosh OS X, you must have the XCode and XOrg-devel products installed. These are available for no cost from the Apple Developer Connection. Registration with Apple is required.
Register on this site by accepting the HTK End User Licence Agreement, then download the latest HTK source code.
Some experience of working with one of the Unix shells (e.g. bash, csh, tcsh). You will need to know which shell you are using, if unsure type:
> echo $SHELL
You will also need to know how to edit files and how to set environment variables.
If you require assistance...
If you are unfamiliar with installing software from source on Linux or Unix, you may resolve any queries more quickly and reliably if you ask a knowledgeable colleague or your local technical support for assistance in the first instance.

If that option is unavailable to you, please try the following sources of assistance:

Search the archives of the htk-users mailing list
If you don't find what you're looking for in the search, subscribe to the htk-users list and post your question there.
Compilation and installation
After unpacking the sources, cd to the htk-3.3 directory. Decide where you wish the binaries to be installed (default is /usr/local which will put the tools in /usr/local/bin.linux) then type ./configure --prefix=/path/to/your/installation

Then running make all will build and install HTK.

<
Installation example
This example shows an installation of HTK on a linux workstation. User entered commands are shown in bold.


> tar xzf HTK-3.3.tar.gz

> cd htk

> ./configure --prefix=/tmp

checking for gawk... gawk

checking for gcc... gcc

checking for C compiler default output file name... a.out

checking whether the C compiler works... yes

[*** multiple lines deleted ***]

checking for strtol... yes

checking build system type... i686-pc-linux-gnu

checking host system type... i686-pc-linux-gnu

configure: creating ./config.status

config.status: creating HTKLib/Makefile

config.status: creating HTKTools/Makefile

config.status: creating HLMLib/Makefile

config.status: creating HLMTools/Makefile

config.status: creating Makefile

> make all

make[1]: Entering directory `/home/cabinet1/jal58/htk/release-3.3/htk/HTKLib'
gcc -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="linux"' -Wall -Wno-switch -g -O2 
 -I. -c -o HShell.o HShell.c
gcc -ansi -D_SVID_SOURCE -DOSS_AUDIO -D'ARCH="linux"' -Wall -Wno-switch -g -O2 
 -I. -c -o HMath.o HMath.c
[*** multiple lines deleted ***]
for program in Cluster HLMCopy LAdapt LBuild LFoF LGCopy LGList LGPrep LLink
 LMerge LNewMap LNorm LPlex LSubset  ; do /usr/bin/install -c -m 755 ${program} 
 /tmp/bin.linux ; done
make[1]: Leaving directory `/home/cabinet1/jal58/htk/release-3.3/htk/HLMTools'
> ls /tmp/bin.linux

Cluster   HDistance  HLEd       HParse    HSLab    LFoF    LMerge
HBuild    HDMan      HList      HQuant    HSmooth  LGCopy  LNewMap
HCluster  HERest     HLMCopy    HRest     HVite    LGList  LNorm
HCompV    HHEd       HLRescore  HResults  LAdapt   LGPrep  LPlex
HCopy     HInit      HLStats    HSGen     LBuild   LLink   LSubset
> 

Testing
Among the samples on the HTK website you'll find the HTK-samples package that can be used to test your installation.

As an initial test of the installation please run the HTK demonstration using the configuration file HTKDemo/configs/monPlainM1S1.dcf. There is a README file in the HTKDemo directory explaining the operation of the demonstration in detail but, in short, you need to run the demonstration script passing it the configuration file configs/monPlainM1S1.dcf as input. To test the language modelling tools you should follow the tutorial in the HTK book, using the files in the LMTutorial/ directory.

Before running the demo make sure you have compiled all the HTK tools and the executables are in your PATH, i.e. just typing 'HInit' at the commandline prints a short usage summary. To run the demonstration type:

cd HTKDemo
perl runDemo.pl configs/monPlainM1S1.dcf
The recognition results obtained should match the following.

On the training set:

 
------------------------ Overall Results --------------------------

SENT: %Correct=0.00 [H=0, S=7, N=7]

WORD: %Corr=77.63, Acc=74.89 [H=170, D=37, S=12, I=6, N=219]

===================================================================

On the test set:

 
------------------------ Overall Results --------------------------

SENT: %Correct=0.00 [H=0, S=3, N=3]

WORD: %Corr=63.91, Acc=59.40 [H=85, D=35, S=13, I=6, N=133]

===================================================================



# 安装
## 安装g++、libx11

sudo apt-get install libc6-dev g++ gccsudo apt-get install libx11-dev

## 安装HTK

下面的安装步骤很简单，按照前假定你已经按照好g++和libx11

> tar xzf HTK-3.4.1.tar.gz 
> cd htk 
> sudo ./configure --prefix=/usr/local 
> sudo make all
> sudo make install
> ls /usr/local/bin
Cluster  HERest  HLMCopy    HQuant    HSmooth  LGCopy  LNewMap
HBuild   HHEd    HLRescore  HRest     HVite    LGList  LNorm
HCompV   HInit   HLStats    HResults  LAdapt   LGPrep  LPlex
HCopy    HLEd    HMMIRest   HSGen     LBuild   LLink   LSubset
HDMan    HList   HParse     HSLab     LFoF     LMerge

现在用命令HInit来测试下
HInit: command not found则没有安装好。
如果出现
USAGE: HInit [options] hmmFile trainFiles...

    Option                                       Default

    -e f    Set convergence factor epsilon       1.0E-4
    -i N    Set max iterations to N              20
    -l s    Set segment label to s               none
    -m N    Set min segments needed              3
    -n      Update hmm (suppress uniform seg)    off
    -o fn   Store new hmm def in fn (name only)  outDir/srcfn
    -u mvwt Update m)eans v)ars w)ghts t)rans    mvwt
    -v f    Set minimum variance to f            1.0E-2
    -w f    set mix wt/disc prob floor to f      0.0
    -A      Print command line arguments         off
    -B      Save HMMs/transforms as binary       off
    -C cf   Set config file to cf                default
    -D      Display configuration variables      off
    -F fmt  Set source data format to fmt        as config
    -G fmt  Set source label format to fmt       as config
    -H mmf  Load HMM macro file mmf
    -I mlf  Load master label file mlf
    -L dir  Set input label (or net) dir         current
    -M dir  Dir to write HMM macro files         current
    -S f    Set script file to f                 none
    -T N    Set trace flags to N                 0
    -V      Print version information            off
    -X ext  Set input label (or net) file ext    lab

则成功安装。

四、例子测试

> tar xzf HTK-samples-3.4.1.tar.gz 

> cd samples 

>  cd HTKDemo

> mkdir -p hmms/{tmp,hmm.{0,1,2,3}} proto acc test 

> perl runDemo configs/monPlainM1S1.dcf 

出现下面结果，测试成功

------------------------ Overall Results --------------------------

SENT: %Correct=0.00 [H=0, S=3, N=3]

WORD: %Corr=63.91, Acc=59.40 [H=85, D=35, S=13, I=6, N=133]

==================================================

# 遇到的问题
1.找不到头文件 sys/cdefs.h

Ubuntu的cdefs.h在目录/usr/include/x86_64-linux-gnu/sys/cdefs.h中，在/usr/include目录下建个符号链接sys指向/usr/include/x86_64-linux-gnu/sys/

之后还有一些头文件找不到，也用此方法解决

修改环境变量C_INCLUDE_PATH，把/usr/include/x86_64-linux-gnu添加进去


2.找不到头文件gnu/stubs-32.h


gnu目录下有stubs-64.h但没有32位的，apt-get安装libc6-dev-i386

 

3.找不到头文件X11/Xlib.h


安装X11的开发包libx11-dev

 

4.链接找不到-lX11

编译的HTK是32位的，所以不能用64位的X11库，搜索到http://aravindev.blogspot.com/2013/08/installing-htk-34-on-ubuntu-64-bit-os.html
但我用他的方法还是不行，所以只好重新configure --without-x --disable-hslab，这样能编译通过

 

使用：

在HTKDemo目录下执行如下命令

[HTKDemo]$ perl runDemo.pl configs/monPlainM1S1.dcf

 

5.提示“Must be in directory HTKDemo to run this script”，但当前目录就是HTKDemo目录

打开runDemo.pl，找到出错位置

 

    $NT_dir = `cd`;

    $NT_dir =~ tr/a-z/A-Z/;

    chomp($NT_dir);


    $dir_pos = index($NT_dir, "HTKDEMO");


    $get_dir = substr($NT_dir, $dir_pos, 7);


    ($get_dir =~ "HTKDEMO") || die "Must be in directory HTKDemo to run this script\n";

把$NT_dir打印出来发现是空的，把$NT_dir = `cd`;改成$NT_dir = `pwd`;，然后这里就OK了


6.安装HDecode

需要额外安装一个HDencode，这个包的下载地址为

http://htk.eng.cam.ac.uk/ftp/software/hdecode/HDecode-3.4.1.tar.gz

使用tar解压可以看到内部内容实际上是htk目录下的一部分

把它拷到对应的目录下

即可在HTK目录下继续执行

make hdecode

make install –hdecode

7.1. make all

Makefile:77: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.

Makefile:111: recipe for target 'hlmtools' failed

solution:


find the file named 'makefile' in hmltools,replace the 8 spaces with a TAB in line 77.

7.2.

/usr/bin/ld: i386 architecture of input file `../HTKLib/HTKLib.a(HLabel.o)' is incompatible with i386:x86-64 output .etc

solution:

in the same file, replace the line 58 to: $(CC) -m32 -o $@ $(CFLAGS) $^ $(LDFLAGS)

