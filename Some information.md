# Some information
## parallel and so on
```bash
parallel -j 4 "
    fastq-dump --split-3 --gzip {1}
" ::: $(ls *.sra)
```
### parallel命令
并发执行命令，提高数据分析效率.  
-j nun表示最多num个并发进程，比如-j 4表示并发执行4个进程.

### fastq-dump命令
参数

--gzip 将转换出的fastq文件以gz格式输出，可以节省空间
--split-3 把pair-end测序分成两个文件输出
-X 拆分出指定的reads数目，默认拆分所有reads，一个read就是fastq的四行数据（老师为了上课测试，设置25000条reads，真实数据不需要加这个参数！！！）
-O 输出文件夹名


## 黑箱
指一个只知道输入输出关系而不知道 内部结构 的 系统 或 设备 。

## SRA (Sequence Read Archive)
可以理解为测序fastq文件的压缩
测序fastq文件很大，至少也有5G左右，双端测序，加起来一个样本也要8G左右，SRA就是将该大文件压缩至至2~3G。

## nohup命令
英文全称 no hang up（不挂起），表示让程序在终端因人为原因或网络原因断开后不挂断，适用于运行时间比较长的命令，一般与&连用

在默认情况下（非重定向时），会输出一个名叫 nohup.out 的文件到当前目录下，如果当前目录的 nohup.out 文件不可写，输出重定向到 $HOME/nohup.out 文件中。

使用：nohup Command [ Arg … ] [　& ]

参数说明：
Command：要执行的命令。

Arg：一些参数，可以指定输出文件。

&：让命令在后台执行，终端退出后命令仍旧执行。

## gzip命令参数
-d或--decompress或----uncompress 　解开压缩文件。
-c或--stdout或--to-stdout 　把压缩后的文件输出到标准输出设备，不去更动原始文件。



## Reference:
nohup：https://www.jianshu.com/p/d3d6d012917d
fastq-dump：https://www.jianshu.com/p/bdfa8f7e5a61
