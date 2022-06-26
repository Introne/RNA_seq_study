
# 清空工作历史的所有变量，确保干净的 R 环境
rm(list=ls())
# 设置当前工作目录（注意双引号）
setwd("~/project/rat/output/HTseq")

# 得到文件样本编号

# list.files(".", "*.count")：列出当前目录里所有以.count结尾的文件
files <- list.files(".", "*.count")
# list()：创建列表
f_lists <- list()
for(i in files){
    prefix = gsub("(_\\w+)?\\.count", "", i, perl=TRUE)
    f_lists[[prefix]] = i
}

id_list <- names(f_lists)
data <- list()
count <- 0
for(i in id_list){
  count <- count + 1
  a <- read.table(f_lists[[i]], sep="\t", col.names = c("gene_id",i))
  data[[count]] <- a
}

# 合并文件
data_merge <- data[[1]]
for(i in seq(2, length(id_list))){
    data_merge <- merge(data_merge, data[[i]],by="gene_id")
}

write.csv(data_merge, "merge.csv", quote = FALSE, row.names = FALSE)
