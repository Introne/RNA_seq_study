# some biosoft
## conda
  Conda是一种开源的软件包和环境管理软件，有两个主要的版本，Anaconda和Miniconda，前者包含一些常用软件包，后者是精简版，根据需要安装软件包。
  Miniconda 是一个 Anaconda 的轻量级替代，默认只包含了 python 和 conda，但是可以通过 pip 和 conda 来安装所需要的包。


## sratoolkit
sratoolkit 是NCBI提供的用于处理来自SRA数据库测序数据的一个工具包。注：SRA是NIH的高通量测序数据的主要档案，存档来自各种高通量测序平台的原始测序数据和比对信息，比如Illumina。
sratoolkit是NCBI上将.sra文件转换为 .fstaq.gz文件的工具。
sra是二进制文件，在Linux下如果用less去查看，它会显示这是个二进制文件，你是否确定打开它。一般我们分析测序数据，是用fastq文件打开分析，所以就需要转格式。


## fastqc
高通量测序数据的高级质控工具
输入FastQ，SAM，BAM文件，输出对测序数据评估的网页报告

fastqc -t 12 -o out_path sample1_1.fq sample1_2.fq
-o --outdir:输出路径 --extract：结果文件解压缩 --noextract：结果文件压缩 -f --format:输入文件格式.支持bam,sam,fastq文件格式 -t --threads:线程数 -c --contaminants：制定污染序列。文件格式 name[tab]sequence -a --adapters：指定接头序列。文件格式name[tab]sequence -k --kmers：指定kmers长度（2-10bp,默认7bp） -q --quiet： 安静模式





内容参考
conda介绍：https://blog.csdn.net/invalidsyntax/article/details/120743789
