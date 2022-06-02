# some biosoft
## conda
  Conda是一种开源的软件包和环境管理软件，有两个主要的版本，Anaconda和Miniconda，前者包含一些常用软件包，后者是精简版，根据需要安装软件包。
  Miniconda 是一个 Anaconda 的轻量级替代，默认只包含了 python 和 conda，但是可以通过 pip 和 conda 来安装所需要的包。


## sratoolkit
sratoolkit 是NCBI提供的用于处理来自SRA数据库测序数据的一个工具包。

sratoolkit可以将.sra文件转换为 .fstaq.gz文件的工具。

注：sra是二进制文件，在Linux下如果用less去查看，它会显示这是个二进制文件，你是否确定打开它。一般我们分析测序数据，是用fastq文件打开分析，所以就需要转格式。

此外，可以利用prefetch命令从NCBI网站下载SRA accession no.的列表文件

注：SRA是NIH的高通量测序数据的主要档案，存档来自各种高通量测序平台的原始测序数据和比对信息，比如Illumina。

### prefetch命令

```bash
Usage:
  prefetch [options] <SRA accession | kart file> [...]
  Download SRA or dbGaP files and their dependencies
  
  prefetch [options] <SRA file> [...]
  Check SRA file for missed dependencies and download them

  prefetch --list <kart file> [...]
  List the content of a kart file
```


prefetch相关参数：(需要将prefetch -o参数改为-O，因为下载的是多个文件)

  -o|--output-file <file>          Write file to <file> when downloading single file
  -0--output-directory <directory) Save files to <directory>



## fastqc
高通量测序数据的高级质控工具
输入FastQ，SAM，BAM文件，输出对测序数据评估的网页报告
```bash
fastqc -t 12 -o out_path sample1_1.fq sample1_2.fq
```
-o --outdir:输出路径 --extract：结果文件解压缩 --noextract：结果文件压缩 -f --format:输入文件格式.支持bam,sam,fastq文件格式 -t --threads:线程数 -c --contaminants：制定污染序列。文件格式 name[tab]sequence -a --adapters：指定接头序列。文件格式name[tab]sequence -k --kmers：指定kmers长度（2-10bp,默认7bp） -q --quiet： 安静模式

注：
SAM(Sequence Alignment/Map)格式是一种通用的比对格式，用来存储reads到参考序列的比对信息。
SAM是一种序列比对格式标准，由sanger制定，是以TAB为分割符的文本格式。主要应用于测序序列mapping到基因组上的结果表示，当然也可以表示任意的多重比对结果。
SAM分为两部分，注释信息（header section）和比对结果部分（alignment section）。

BAM文件是SAM文件的二进制形式


## multiqc
将fastqc的统计结果汇聚成一个网页可视化文件，便于查看


## cutadapt
用于去除测序接头

## Trim Galore
使用perl脚本编写的工具，是对cutapater和fastqc命令的封装。可以自动检测接头并调用cutapater进行

## hisat2: 基因组比对工具
由于测序仪机器读长的限制，在构建文库的过程中首先需要将DNA片段化，测序得到的序列只是基因组上的部分序列。为了确定测序reads在基因组上的位置，需要将reads比对回参考基因组上，这个步骤叫做mapping。

##  Ensembl
Ensembl是一个脊椎动物基因组的基因组浏览器，支持比较基因组的研究，进化，序列变异和转录调控。Ensembl可以注释基因，计算多重比对，预测调节功能和收集疾病数据。Ensembl工具集合包括BLAST、BLAT、BioMart和变异效应预测器(VEP)(支持所有物种)。

有许多个模块可供搜索，分别是Gene、Transcript、Variant、Phenotype、Stuctural Variation等。

gtf文件即基因组注释文件

## 一般在三个网站下载参考基因组：Ensembl、NCBI和UCSC：
参考基因组：对于人类来说，目前比较常用的参考基因组有hg19、hg38、GRCh37、GRCh38。hg系列是UCSC的叫法，GRCh系列是NCBI和Ensembl的叫法。同一版本的序列是一样的，hg19对应GRCh37，hg38对应GRCh38。

注释文件：三个来源同一版本的DNA序列虽然相同，但是它们的注释是不同的，更新频率也不一样。

NCBI 的注释是refseq数据集，UCSC 和 Ensembl 注释都将其作为自己的一个子集，如UCSC 的refGene。

而UCSC 的注释比较混乱，同样ID的基因会出现在不同链或不同染色体位置上。Ensembl的注释通常比UCSC更多（例如snRNA、miRNA、假基因，所以噪音更多一点），但是ID处理比较好，所以ID更容易进行转换。

Ensembl还经常更新它的注释，更新一次作为一个版本发布。不同的来源的基因组序列名称不一样，1号染色体在 UCSC 中是 chr1，而在 Ensembl的基因组和GTF文件中是1。

使用时序列和注释要统一，UCSC的基因组序列需要对应使用UCSC的gtf/gff3注释文件，Ensembl则对应使用其同一版本对应的gtf/gff3注释文件。
GeneCode（http://www.gencodegenes.org/）也可以下载人类和小鼠的基因注释文件。

选择注释资源应遵循的原则：当进行强调可重复性和稳健的基因表达估计的研究时，优先选较为简单的基因组注释，如 RefGene。当进行更具探索性的研究时，更全面的注释更优，比如选择Ensembl。而UCSC则不太建议使用。


#### 总结

Gene model会影响基因表达量乃至差异表达基因的筛选，尤其是不同gene model对某些基因的长度、junction位点注释有出入；

Ensembl的注释相对更加准确，基因更多；

推荐人鼠用GENCODE，谁让它出自最权威的ENCODE呢，其他物种用Ensembl。


内容参考
conda介绍：https://blog.csdn.net/invalidsyntax/article/details/120743789
SAM文件：https://www.jianshu.com/p/9c99e09630da
RNA-seq tips：https://www.51xxziyuan.com/54/539.html
Ensembl、NCBI和UCSC：https://www.jianshu.com/p/017e5a565070
sratoolkit配置网站：https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit
